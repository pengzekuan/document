1. 创建用户

```sql
create user 'userName' identified by 'password';
```

2. 用户授权

  **host说明**
  - `%` 任意IP访问
  - `localhost` 本地访问
  - `ip` 指定IP访问

```sql
grant all privileges on 'database'.'table' to 'userName'@'host' identified by 'password' with grant option;
```

3. 刷新配置

```sql
flush privileges;
```

4. 修改配置

```shell
注释以下配置
#bind-address = 127.0.0.1
```

5. 重启服务