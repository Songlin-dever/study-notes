# SQL

- ## DDL 

  - 数据定义语言
  - CREATE 创建
  - ALTER  修改 
  - DROP 删除 
  - TRUNCATE 删除，如：TRUNCATE TABLE [Table Name]。 
  - COMMENT 注释 
  - GRANT 授权
  - REVOKE 收回已经授予的权限

- ## DCL

  - 数据控制语言
  - COMMIT 提交
  - ROLLBACK 回滚
  - SET TRANSACTION 设置当前事务的特性，它对后面的事务没有影响

- ## DML

  - 数据操作语言
  - SELECT   查询 
  - INSERT    添加 
  - UPDATE     更新 
  - DELETE    删除 

- ## DQL 

  - 数据查询语言
  - SELECT     select_list [ INTOnew_table ]
    FROM       table_source
    [ WHERE     search_condition ]
    [ GROUPBY   group_by_expression ]
    [ HAVING      search_condition ]
    [ ORDER BY   order_expression  [ ASC | DESC ] ]

## 通用命令

\#启动mysql服务器 

- net start mysql  

#关闭  

- net stop mysql   

#进入 

- mysql -h 主机地址 -u 用户名 －p 用户密码  

#退出

- exit

status;显示当前mysql的version的各种信息。



\#格式:

- **grant 权限 on 数据库.* to 用户名@登录主机 identified by '密码'**

- 如，增加一个用户user1密码为password1，让其可以在本机上登录， 并对所有数据库有查询、插入、修改、删除的权限。首先用以root用户连入mysql，然后键入以下命令： 
  - grant select,insert,update,delete on *.\* to user1@localhost Identified by "password1"; 

- 如果希望该用户能够在任何机器上登陆mysql，则将localhost改为"%"。 

- 如果你不想user1有密码，可以再打一个命令将密码去掉。 
  - grant select,insert,update,delete on mydb.* to user1@localhost identified by "";

- grant all privileges on wpj1105.* to sunxiao@localhost identified by '123';   #all privileges 所有权限

## 索引有关
