### 添加APT源
1. 打开下载安装源地址

    下载地址：https://dev.mysql.com/downloads/repo/apt/

2. 根据系统类型选择需要下载的源

3. 安装源

```
sudo dpkg -i /path/xxx.deb
```

4. 更新系统源信息

```
sudo apt update
```

### 安装 `mysql-server`

```
sudo apt install mysql-server
```

### `mysql` 服务管理

```
systemctl status|start|stop|restart mysql
or
service mysql status|start|stop|restart
or
/etc/init.d/mysql status|start|stop|restart
```

