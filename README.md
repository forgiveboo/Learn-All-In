## Arch下安装MySQL
`sudo pacman -S mysql`
## 初始化MySQL
- `sudo mysqld --initialize --user=mysql --basedir=/usr --datadir=/var/lib/mysql`
- 执行结果：
```
2021-12-14T05:14:35.606101Z 0 [Warning] [MY-010915] [Server] 'NO_ZERO_DATE', 'NO_ZERO_IN_DATE' and 'ERROR_FOR_DIVISION_BY_ZERO' sql modes should be used with strict mode. They will be merged with strict mode in a future release.
2021-12-14T05:14:35.606432Z 0 [System] [MY-013169] [Server] /usr/bin/mysqld (mysqld 8.0.11) initializing of server in progress as process 12937
2021-12-14T05:14:37.530922Z 5 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: sdfhuc0of.u
```
- 结果表示：
   - 默认创建了一个用户
   - 用户名：root@localhost
   - 密码：sdfhuc0of.u
### 开机自启动
`sudo systemctl enable mysqld.service`
### 启动MySQL服务
`systemctl start mysqld`
### 连接MySQL
- `mysql -u root -p`
> 密码是初始化时显示的密码
- 解决`ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using passwor)`
> 找到MySQL的配置文件my.cnf，然后在里面找到`[mysqld]`这一项，然后在该配置项下添加`skip-grant-tables`
### 修改默认密码
- `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';`
- 解决`ERROR 1290 (HY000): The MySQL server is running with the --skip-grant-tables option so it cannot execute this statement`
> 执行`flush privileges;`命令
### 添加用户
`create user 'username' identified by 'password';`
### 创建数据库
`create database database_name;`
### 给用户授权
`grant select,insert,update,delete,create on database_name.* to username@'%';`
## 使用MySQL
- 安装MySQL命令行客户端`pip install mycli`
- 以root用户连接数据库`mycli -u root`
### 查询所有数据库
`show databases;`

![所有库](https://github.com/forgiveboo/MySQL-Learn/blob/main/screenshots/%E6%89%80%E6%9C%89%E5%BA%93.png)
### 创建数据库
`create database database_name;`
### 使用数据库
`use 数据库名;`
### 查询所有用户
`select user from mysql.user`

![所有用户](https://github.com/forgiveboo/MySQL-Learn/blob/main/screenshots/%E6%9F%A5%E8%AF%A2%E7%94%A8%E6%88%B7.png)
### 创建表
- 以普通用户连接数据库`mycli -u username;`
- 选择要创建表的数据库`use database_name;`
- 在该数据库中创建表`create table table_name (column_name column_type);`
### 查询表结构
`desc table_name;`

![表结构](https://github.com/forgiveboo/MySQL-Learn/blob/main/screenshots/%E6%9F%A5%E7%9C%8B%E8%A1%A8%E7%BB%93%E6%9E%84.png)
### 查看当前数据库中所有表
`show tables`

![所有表](https://github.com/forgiveboo/MySQL-Learn/blob/main/screenshots/%E6%9F%A5%E7%9C%8B%E6%89%80%E6%9C%89%E8%A1%A8.png)
