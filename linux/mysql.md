## 安装

```
sudo apt install mysql-server
```

## 配置

- 字符集配置

```
sudo vi /etc/mysql/conf.d/mysql.cnf

[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]

default-character-set = utf8mb4

[client]
default-character-set = utf8mb4
```

## 修改root密码

```
#切换mysql数据库
use mysql;
#修改root账号密码
update user set authentication_string = password('你的密码'), password_expired = 'N', password_last_changed = now() where user = 'root';
#不限制root账户登录来源（任意地址都能登录）
update user set host='%' where user='root';
#使用原生密码验证登录
update user set  plugin="mysql_native_password";
#刷新权限
flush privileges;
#退出
exit;

```

## 远程登录配置

```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address 127.0.0.1 #修改访问IP，或直接注释
```
