# Linux Study

## vim      

默认为一般模式，按 i 进入编辑模式，按 esc 退回一般模式，按 ：或者 /  进入命令行模式， 再esc回到一般模式

一般模式下 G 到最后一行， gg 到第一行， u 撤销动作， 20 + shift + g 快速定位到第 20 行

一般模式下，yy拷贝当前行，p黏贴，nyy表示拷贝n行， dd删除当前行，ndd删除 n行

在文件中查找某个单词，/+单词  再回车，n表示查找下一个

命令行模式下， set nu 显示行号， set nonu 取消行号，

## 关机 & 重启 & 用户

shutdown -h now      立刻进行关机    shutdown -h 2  “Hello 两分钟后关机”         shutdown  -r  now 现在重启计算机

halt  关机   reboot  重启   sync 把内存的数据同步到磁盘 

su + 用户名  可切换用户;    useradd  + 用户名     添加用户;   useradd -d 指定目录  用户名 :  

passwd  用户名 ： 给用户设置密码；  

userdel  用户名  ：删除用户 ， 保留家目录；  userdel -r 用户名 ：删除用户以及家目录

id + 用户名  ： 查询用户信息；who am i ：查看当前用户信息

useradd -g 用户组 用户名  ：添加用户时指定用户组

### 用户组：

类似于角色，系统可以对多个具有共性的用户进行统一管理  增加用户组： groupadd 组名  删除用户组 ： groupdel 组名

修改用户的用户组：usermod -g 用户组  用户名

## 帮助指令

man [命令或配置文件] 功能：获得帮助信息

help 命令 获得shell内置命令的帮助信息

## 文件&目录

### 文件

cat [选项] 要查看的文件 查看文件内容

​	-n 显示行号

rm [选项] 要移除的文件或目录

​	-r 递归删除整个文件夹

​	-f 强制删除不提示

mv 移动文件或目录或重命名

​	mv oldFileName newFileName 重命名

​	mv movedFile targetFolder 移动文件 

pwd 显示当前工作目录的绝对路径

ls [选项] [目录或文件] 

​	-a 显示当前目录所有的文件和目录，包括隐藏的

​	-l 以列表的形式显示信息

cd 或者 cd ~ 回到自己的家目录

cd .. 回到当前目录的上一级目录

more 基于VI编辑器的文本过滤器，它以全屏幕的方式按页显示文件内容

​	空白键(space) 向下翻页

​	Enter 向下翻一行

​	q 立刻离开more 不再显示该文件内容

​	ctrl + F 向下滚动一屏

​	ctrl + B 返回上一屏

​	= 输出当前行的行号

​	:f  输出文件名和当前行的行号

less 分屏查看文件内容

​	q 离开less整个程序

​	/字串 向下搜寻字串的功能； n 向下查找； N 向上查找 (n表示next，直接在键盘输入)

​	?字串 向上搜寻字串的功能； n 向上查找； N 向下查找

​	[pagrdown] 向下翻一页

​	[pageup] 向下翻一页

echo [选项] [输出内容] 输出内容到控制台

​	如 echo $HOSTNAME

head 用于显示文件的开头部分内容 默认显示前十行

​	head -n 5 文件 显示前五行

tail 输出文件中尾部的内容 默认尾10行

​	tail -n 5 fileName 尾5行

​	tail -f 文件 实时追踪该文档的有所更新

\> 输出重定向 、>> 追加

​	ls -l > a.txt  列表内容写入到文件a.txt中 覆盖写

​	ls -al >> a.txt 列表内容追加到文件a.txt末尾

​	cat 文件1 > 文件2 文件1的内容覆盖文件2      echo "内容" >> 文件……

### 目录

mkdir [选项] 要创建的目录

​	-p 创建多级目录

rmdir 删除空目录，如果下面有内容则无法删除

rm -rf 要删除的目录  强制删除非空目录

touch 创建空文件 比如 touch hello.txt

ln 软连接也称为符号链接，类似于windows里的快捷方式，主要存放了连接其他文件的路径

ln -s [原文件目录] [软连接名] 给原文件创建一个软连接 （pwd仍然是软连接所在目录   rm [软连接名] 删除软连接

history 查看已经执行过历史命令，也可以执行历史指令， !5 重新执行第5号指令

### 拷贝指令

cp [选项] 目标文件 目标地址

​	-r 递归复制整个文件夹

\cp 强制覆盖

## 时间日期

date 显示当前时间  "+"号不能省略

date +%Y 显示当前年份

date +%m 显示当前月份

date +%d 显示当前是哪一天   时分秒：%H %M %S

date -s 字符串时间  可设置系统时间 如 date -s "2020- 11- 20 20: 02: 20"

cal [选项] 不加选项显示本月日历

## 搜索查找类

find 从指定目录向下递归遍历其各个子目录，将满足条件的目录或文件显示在终端

find [搜索范围] [选项]

​	-name<查询方式> 按照指定的文件名查找文件

​	-user<用户名> 查找属于指定用户名所有文件

​	-size<文件大小> 按照指定的文件大小查找文件 +n 大于 -n小于 n等于 如 +200M 是查找大于200M的文件

locate 搜索文件  快速定位文件路径  由于基于数据库查询，第一次使用前使用updatedb指令创建数据库

which 指令 查看某个指令在哪个目录下

grep [选项] 查找内容 源文件  | 管道符 将前一个指令的处理结果输出传递给后面的指令处理

​	-n 显示匹配行以及行号

​	-i 忽略字母大小写

## 压缩和解压

zip [选项] XXX.zip 将要压缩的内容 可以压缩文件和目录  

​	-r 递归压缩，即压缩目录

unzip [选项] XXX.zip 解压缩文件

​	-d<目录> 指定解压后文件的存放目录

gzip 文件 压缩文件，只能将文件压缩为*.gz文件

gunzip 文件.gz 解压缩文件

tar [选项] XXX.tar.gz 打包的内容 打包目录，压缩后的文件格式为.tar.gz

​	-c 产生.tar打包文件

​	-v 显示详细信息

​	-f 指定压缩后的文件名

​	-z 打包同时压缩

​	-x 解压.tar文件

## 所有者 组 & 权限

ls -ahl 查看文件所有者

chown 用户名 文件名 可以改变文件所有者

chown newOwner:newGroup 文件或目录 改变文件的所有者和所在组

​	-R 如果是目录、则使其下所有子文件和目录递归生效

chgrp newGroup 文件或目录 改变文件或目录的所有组 (也由-R选项 同上)  chgrp -R new Group 文件或目录

ls -l 内容如下

​	-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc  (1 文件的硬链接数或目录的子目录数， root1用户，root2 组，1213表示文件大小(字节)，如果是文件显示4096字节，"Feb 2 09:39"表示最后修改日期 abc表示文件名)

0~9位：第0位确定类型(d, -, l, c, b)  第1~3位确定所有者拥有该文件的权限(User)……往后依次 Group Other  r=4,w=2,x=1

​	l是连接，相当于windows的快捷方式

​	d是目录，相当于windows的文件夹

​	c是字符设备文件，相当于鼠标，键盘

​	b是块设备，比如硬盘

​	-就是普通文件

chmod 可以修改文件或目录的权限  u:所有者 g:组 o:其他人  a:所有人(u,g,o的总和) +、-、=、变更权限

​	chmod u=rwx,g=rw,o=x 文件或目录

​	chmod o+w 文件或目录 

​	chmod a-x 文件或目录

chmod 751 文件或目录 (给所有者rwx，给组rx，给其他人x)

## 任务调度

任务调度：系统在某个时间执行的特定任务或程序

crontab [选项]

​	-e 编辑crontab定时任务

​	-l 查询crontab任务

​	-r 删除当前用户所有的crontab任务

设置定时任务，先执行crontab -e进入编辑

*/1**** ls -l /etc/ > /tmp/to.txt  （/1表示每一分钟）

​	第一个* 一小时当中的第几分钟 0~59

​	第二个* 一天当中第几小时 0~23

​	第三个* 一个月当中第几天 1~31

​	第四个* 一年当中的第几个月 1~12

​	第五个* 一周当中星期几 0~7 (0和7都代表星期日)

特殊符号：

- \* 代表任何时间，比如第一个"*"代表一小时每分钟都执行一次
- ,  代表不连续时间，比如"0 8,12,16***"代表每天8点12点16点都执行一次
- \- 代表连续的时间范围 "0 5 * * 1-6"代表周一到周六凌晨5点执行命令
- */n 代表每隔多久执行一次 比如"\*/10 * * * *"代表每隔十分钟执行一遍命令

at是一次性定时任务，at的守护进程atd会以后台模式进行，检查作业队列来运行，默认情况下，atd守护进程每60秒检查作业队列，有作业时会检查作业运行时间，如果时间与当前时间匹配，则运行此作业。at执行完一个任务不再执行此任务，使用at命令时要保证atd在运行

at [选项] [时间] Ctrl + D 结束 at 命令输入

| 选项          | 含义                                                         |
| ------------- | ------------------------------------------------------------ |
| -m            | 当 at 工作完成后，无论命令是否输出，都用 E-mail 通知执行 at 命令的用户。 |
| -c 工作标识号 | 显示该 at 工作的实际内容。                                   |
| -t 时间       | 在指定时间提交工作并执行，时间格式为 [[CC]YY]MMDDhhmm。      |
| -d            | 删除某个工作，需要提供相应的工作标识号（ID），同 atrm 命令的作用相同。 |
| -l            | 列出当前所有等待运行的工作，和 atq 命令具有相同的额作用。    |
| -f 脚本文件   | 指定所要提交的脚本文件。                                     |

## 磁盘 & 分区

lsblk 或者 lsblk -f 查看所有设备挂载情况

给虚拟机分配硬盘

给硬盘分区:

fdisk /dev/sdb  (两次enter默认剩余全部空间)

- m 显示命令列表
- p 显示磁盘分区，同 fdisk -l
- n 新增分区
- d 删除分区
- w 写入并退出

格式化磁盘 

挂载 mount 分区 文件

卸除挂载 umount

每次启动自动挂载 修改/etc/fstab

### 磁盘情况查询

df -h 查询系统整体磁盘使用情况

du [选项] -h 查询指定目录的磁盘占用情况 

- -s 指定目录的大小汇总
- -h 带计量单位
- -a 含文件
- --max-depth=1 子目录深度
- -c 列出明细的同时，增加汇总值

比如：

du -h   --max-depth=1 /opt

du -ha --max-depth=1 /opt

### 磁盘实用指令

tree 目录 以树状结构显示目录(如果没有tree，使用yum install tree安装)

ls -l /opt | grep "^-" | wc -l 统计opt文件夹下文件的个数

ls -l /opt | grep "^d" | wc -l 统计opt文件夹下目录的个数

ls -lR /opt | grep "^-" | wc -l 统计opt文件夹及其子文件夹下文件的个数

## 网络配置

ipconfig 查看windows环境中VMnet8网络配置

ifconfig 查看Linux的网络配置 (ens33 inet 后面是ip地址)

ping 目的主机 测试当前服务器是否可以连接到目标主机，如www.baidu.com

指定ip(把ip地址改为静态)

- BOOTPROTO="static"
- IPADDR=192.168.200.130
- GATEWAY=192.168.200.2
- DNS1=192.168.200.2

编辑虚拟机的网段vmnet8

然后重启网络服务或者重启系统生效 service network restart，reboot

### 主机名和hosts映射

为了方便。可以给Linux系统设置主机名，也可以根据需要修改主机名 修改文件在/etc/hostname指定

hostname 可以查看主机名

修改后重启生效

hosts映射可以通过主机名找到（比如ping）某个Linux系统

windows在C:\Windows\System32\drivers\etc\hosts 文件中指定即可 如 192.168.200.130 lwh0302

Linux 在/etc/hosts 文件中指定 如 192.168.200.1 ThinkPad-PC

## 进程管理

进程有两种方式存在。前台和后台

- 前台指显示在屏幕上用户可以进行操作的
- 后台指实际在运行但是没有显示在屏幕上，在后台运行，如mysql tomcat

ps 可以查看系统中有哪些进程在运行  

(TIME进程使用CPU的总时间，VSZ 进程占用的虚拟内存大小，RSS 占用的物理内存大小)

​	-a 显示当前终端的所有进程信息

​	-u 以用户的格式显示进程信息

​	-x 显示后台进程运行的参数

ps -ef 以全格式显示当前所有进程 -e 显示所有进程 -f 全格式

kill [选项] 进程号 通过进程号杀死进程

​	-9 强迫进程立即停止

killall 进程名称 通过进程名杀死进程，支持通配符

pstree [选项] 可以更加直观的查看进程信息

​	-p 显示进程的ID

​	-u 显示进程的所属用户

## 服务管理（守护进程

### service指令

服务的本质就是一个运行在后台的进程，通常会监听某个端口，等待其他程序的请求，比如mysql，sshd，防火墙，因此我们又称为守护进程

service 服务名 [start | stop | restart | reload | status] 

CentOS7.0之后，很多服务不再使用service，而是systemctl

service指令管理的服务在 /etc/init.d中查看

 setup 可以查看所有系统服务 （前面有  *  表示自动启动

### 运行级别

Linux有7种运行级别（runlevel 最常用3和5 ）运行级别说明在/etc/inittab 下

- 运行级别0 ：系统停机（启动马上关机）状态，系统默认运行级别不能设为0，否则不能正常启动
- 运行级别1 ：单用户工作状态，root权限，用于系统维护，禁止远程登录
- 运行级别2 ：多用户状态(没有NFS，network file system 网络文件系统)，不支持网络
- 运行级别3 ：完全的多用户状态(有NFS)，登录后进入控制台命令行模式
- 运行级别4 ：系统未使用，保留
- 运行级别5 ：X11控制台，登录后进入图形GUI 模式
- 运行级别6 ：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动

Linux开机流程 ：开机 -> BIOS -> /boot -> systemd进程1 -> 运行级别 -> 运行级别对应的服务

system get-default 查看当前运行级别

chkconfig 给服务的各个运行级别设置自 启动 | 关闭，其管理的服务在/etc/init.d查看

chkconfig --list 查看服务

chkconfig --level 5 服务名 on/off 在5级别对某服务设置自启动或关闭  重新设置后需要reboot才能生效

### systemctl指令

systemctl [start | stop | restart | status] 服务名 （对运行级别3和5都生效）

systemctl 管理的服务在 /usr/lib/systemd/system 查看

systemctl list-unit-files 查看服务开机启动状态

systemctl enable 服务名 设置服务开机启动

systemctl disable 服务名 关闭服务开机启动

systemctl is-enabled 服务名 查询某个服务是否开机启动

### firewall指令

firewall-cmd --permanent --add-port=端口号/协议  (如8080/tcp) 打开端口 

firewall-cmd --permanent --remove-port=端口号/协议 关闭端口

以上两条命令重新载入才能生效 firewall-cmd --reload

firewall-cmd --query-port=端口/协议 查询端口是否开放

### 监控

#### 监控进程

top [选项]  top和ps很像，但是top执行一段时间可以更新正在运行的进程

- -d 秒数 指定top命令每隔几秒更新，默认是3秒
- -i 使top不显示任何闲置或僵死进程
- -p 通过指定监控进程ID来仅仅监控某个进程的状态

交互操作:  (直接在键盘输入)

- P 以CPU使用率排序，默认此项
- M 以内存的使用率排序
- N 以PID排序
- q 退出top
- u 输入完后回车，再输入用户名，监控指定用户
- k 再输入要结束的进程ID，结束指定的进程

#### 监控网络

netstat [选项]     （proto：协议，Local Address: 本机地址，Foreign Address：外部地址

- -an 按一定顺序排列输出
- -p 显示哪个进程在调用

ping 对方ip地址，检测远程主机是否正常，或是两部主机之间的网线或网卡故障

比如 查看服务名为sshd的信息：netstat -anp | grep sshd

## RPM & YUM

rpm用于互联网下载包的打包和安装工具，包含在某些Linux分发版中，它生成具有.RPM扩展名的文件，

rpm -qa  查询已安装的rpm列表

比如一个包名：firefox-60.2.2.1-1.el7.centos.x86_64

- 名称 ：firefox
- 版本号 ：60.2.2.1
- 适用操作系统 ：el7.centos.x86_64  (i686，i386表示32位系统，noarch表示通用)

rpm -q 软件包名 查询软件包是否安装

rpm -qi 软件包名 查询软件包信息

rpm -ql 软件包名 查询软件包中的文件

rpm -qf 文件全路径名 查询文件所属于的软件包

rpm -e 软件包的名称 （如果其它软件包依赖于您卸载的软件包，会产生错误信息

rpm [选项] RPM包全路径名称

- -i install安装
- -verbose 提示
- -h hash 进度条

yum是一个Shell前段软件包管理器，基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次性安装所有依赖的软件包

yum list | grep XXX 查询yum服务器是否有需要安装的软件

yum install XXX 下载安装
