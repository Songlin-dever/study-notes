# Mysql

## 数据类型

### 数值类型

- TINYINT
  - 1 byte
  - 范围：
    - 有符号：(-128, 127)
    - 无符号：(0, 255)
- SMALLINT
  - 2 bytes
- MEDIUMINT
  - 3 bytes
- INT或者INTEGER
  - 4 bytes
- BIGINT
  - 8 bytes
- FLOAT
  - 4 bytes
- DOUBLE
  - 8 bytes
- DECIMAL
  - 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2

### 日期和时间类型

- DATE
  - 3 bytes
  - YYYY-MM-DD
- TIME
  - 3 bytes
  -  HH:MM:SS
- YEAR
  - 1 byte
  - YYYY
- DATETIME
  - 8 bytes
  - YYYY-MM-DD hh:mm:ss （'1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'
- TIMESTAMP
  - 4 bytes
  - YYYY-MM-DD hh:mm:ss （ '1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07' UTC，结束时间第2^31 - 1秒

### 字符串类型

- CHAR （BINARY
  -  0-255 bytes
  - 定长字符串
- VARCHAR（VARBINARY
  -  0-65535 bytes
  - 变长字符串
- TINYBLOB
  -  0-255 bytes
  - 不超过 255 个字符的**二进制**字符串
- TINYTEXT
  -  0-255 bytes	
  - 短**文本**字符串
- BLOB
  -  0-65535 bytes
- TEXT
  -  0-65535 bytes
- MEDIUMBLOB
- MEDIUMTEXT
- LONGBLOG
- LONGTEXT

## 索引优化

### 前缀索引优化

前缀索引就是使用字段中的**字符串的前几个字符来**作为索引

优点 ：

- 可以减小索引字段的大小，可以增加一个索引页中的索引数量，提高查询速度

缺点：

- order by无法使用前缀索引
- 无法把前缀索引用作覆盖索引

### 覆盖索引优化

假设要查询商品的名称，价格

可以建立一个联合索引，包括 商品ID，名称，价格，



使用覆盖索引的好处：

- 不需要查询出整行记录的所有信息，减少了大量的I/O操作

### 主键索引最好自增

Innodb创建主键索引默认是聚簇索引，如果使用自增键作为主键，每次添加记录都会按照顺序添加到当前索引节点的位置，不需要移动已有的数据，当页面写满，会自动开辟一个新页面，因为每次插入一条新纪录，都是追加操作，不需要重新移动数据，这种写法效率非常高

### 索引最好设置为 NOT NULL

原因：

- 优化器在做索引选择时，优化器难以选择，难以优化，更加复杂
- NULL值没有意义，但是会占用物理空间

### 防止索引失效