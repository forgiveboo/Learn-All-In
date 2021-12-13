## MySQL学习记录
### Arch下安装MySQL
`sudo pacman -S mysql`
### 初始化MySQL
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
- `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';`
- 解决`ERROR 1290 (HY000): The MySQL server is running with the --skip-grant-tables option so it cannot execute this statement`
> 执行`flush privileges;`命令
### 添加用户
`create user '新用户名' identified by '新用户密码';`
