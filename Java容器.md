# Java容器

## Collection

- 独立元素序列，这些元素服从一条或者多条规则

- ### Set

  - #### SortedSet<interface>

    - ##### NavigableSet<interface>

      - ###### TreeSet （里面有TreeMap，适配器模式）

  - #### HashSet

    - ##### LinkedHashSet

- ### LinkedHashSet和TreeSet和HashSet

  - 相同点：
    - 不存在重复元素
    - 非线程安全
    - Fail-Fast迭代器

  - 不同点：
    - 处理速度：HashSet   > LinkedHashSet > TreeSet；前两个速度几乎相同，后者插入时需要排序，前两个的`add`，`remove`，`contains` 时间复杂度均为O(1)，TreeSet均为O(logN)
    - 元素顺序：
      - HashSet不维持元素顺序
      - LinkedHashSet元素顺序遵循插入顺序
      - TreeSet元素顺序遵循排序顺序

    - 内部实现：
      - HashSet 基于 HashMap
      - LinkedHashSet 基于 HashSet和LinkedList
      - TreeSet 基于 TreeMap

    - 是否允许为null
      - HashSet 和 LinkedHashSet 都允许 null 元素，但 TreeSet 不允许 null 元素，而且当向 TreeSet 插入 null 元素时，TreeSet 使用 compareTo 方法与 null 元素进行比较，将会出现 [java.lang.NullPointerException](https://xie.infoq.cn/link?target=http%3A%2F%2Fjavarevisited.blogspot.sg%2F2012%2F06%2Fcommon-cause-of-javalangnullpointerexce.html)。

    - 比较：
      - HashSet和LinkedHashSet使用equals方法进行比较，而TreeMap使用compareTo，这就是为什么 compareTo 方法需要与 equals 方法实现保持一致的原因。当 compareTo 方法与 equals 方法实现不一致时，这违反了实现 Set 的特点（不允许元素重复）

- ### List

  - #### ArrayList

    - 使用**动态数组**实现

    - `1.5`倍扩容

    - `get(int index)` O(1)
    - `add(E e)` 如果不扩容，O(1)，如果不是第一次扩容（`oldCapacity > 0`），使用`Arrays.copyOf()` ，把原有数组中的元素复制到扩容后的新数组当中，O(n)
    - `add(int index, E element)` 不管需要不需要扩容，`System.arraycopy()` 肯定要执行 O(n)
    - `remove(int index)` O(n) 可能使用 `System.arraycopy()`

  - #### LinkedList

    - 使用**双向链表**实现
    - `get(int index)` O(n) 循环遍历整个链表
    - `add(E e)` O(1)
    - `add(int index, E element)` 先遍历找到插入的位置，O(n)
    - `remove(int index)` 需要遍历查找需要删除的元素，O(n)

  - #### CopyOnWriteArrayList

  - #### Vector

    - #### Stack 

      - 线程安全，保留类，不建议使用
      - 使用**数组**实现

- ### Queue

  - #### LinkedList

  - #### PriorityQueue

  - #### Deque<interface>

    - ##### LinkedList

    - ##### ArrayDeque

    - ##### BlockingDeque<interface>

  - #### BlockingQueue<interface>

## Map

- ### SortedMap<interface>

  - #### NavigableMap<interface>

    - ##### ConcurrentNavigableMap<interface>

    - ##### TreeMap

- ### HashMap

  - #### LinkedHashMap

- ### HashTable

- ### EnumMap

- ### IdentityHashMap

- ### ConcurrentMap

## TreeSet

- 常用方法：（这些方法`set`接口里没有）
  - ceiling(E e) 返回大于等于e的最小元素
  - lower(E e) 返回大于e的最大元素

## TreeMap

- `key`不能为`null`，`value`可以为`null`

- 基于红黑树实现，即`containsKey(), put(), get(), remove()` 都有log(n)时间复杂度
- 在多线程环境下需要同步
  - 程序员手动同步
  - 包装TreeMap，`SortedMap m = Collections.synchronizedSortedMap(new TreeMap(...));`
- **红黑树是一种近似平衡的二叉查找树，它能够确保任何一个节点的左右子树的高度差不会超过二者中较低那个的一倍**：
  - 每个节点要么是红色，要么是黑色。
  - 根节点必须是黑色
  - 红色节点不能连续(也即是，红色节点的孩子和父亲都不能是红色)。
  - 对于每个节点，从该点至`null`(树尾端)的任何路径，都含有相同个数的黑色节点。

- 红黑树的约束条件被破坏时，需要进行调整：
  - 改变节点的颜色
  - 左旋：当前节点变为右子树的左子树，当前节点的右子树变为原右子树的左子树
  - 右旋：当前节点变为左子树的右子树，当前节点的左子树变为原左子树的右子树

- 节点后继，给定节点t
  - 如果t的右子树不为空，则t的后继节点为右子树中最小的那个元素
  - 如果t的右子树为空，则t的后继是其第一个向左走的祖先。

## HashMap

- `key`和`value`都可以为`null`
- `2`倍扩容
- 结构：数组 + 链表 + 红黑树
  - 链表长度大于8 && 数组大小 < 64 ：重新hash
  - 链表长度大于8 && 数组大小 > 64 ：转换为红黑树
  - 红黑树的节点数 < 6 ：转换为链表
- 确保实现`hashcode()`和`equals()`方法，否则不能作为hashmap的键值，equals返回true时，hashcode必须相同
- 有两个参数很影响hashmap的性能：
  - `initial capacity` 初始容量：指定初始`table`大小，对于插入元素较多的场景，将初始容量设大可以减少重新hash的次数，默认为`16`，若传入初始化大小为`k`，则初始化为大于`k`的`2`的整数次方，如`k`为`10`，则初始化为`16`
  - `load factor` 负载系数：`entry`的数量超过`capacity*load_factor`时，容器将自动扩容并重新哈希。
- 常用方法：
  - `get()` ：该方法调用了`getEntry(Object key)`得到相应的`entry`，然后返回`entry.getValue()`。因此`getEntry()`是算法的核心。 算法思想是首先通过`hash()`函数得到对应`bucket`的下标，然后依次遍历冲突链表，通过`key.equals(k)`方法来判断是否是要找的那个`entry`。
  - `put()` ：先判断是否存在对应entry，若不存在调用`addEntry()`进行头插，1.8后改为尾插
- `JDK1.8`的优化：
  - 数组 + 链表 => 数组 + 链表 + 红黑树：
    - 防止发生 hash 冲突导致链表长度过长，将时间复杂度由`O(n)`降为`O(logn)`;
  - 头插法 => 尾插法：
    - 多线程环境下会产生环，A 线程在插入节点 B，B 线程也在插入，遇到容量不够开始扩容，重新 hash，放置元素，采用头插法，后遍历到的 B 节点放入了头部，这样形成了环
  - 1.7在扩容时需要重新hash，1.8则位置不变或索引 + 旧容量大小
  - 插入时，1.7先判断是否扩容再插入，1.8先插入，再判断是否扩容

