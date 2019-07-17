## ubuntu 常用命令



### 用户/组

*`useradd` 添加用户*  

```shell
Usage: useradd [option] USER
```

- `-m`  `--create-home` 同时创建用户`home`目录
- `-g` `--gid`  指定用户组
- `-s` `--shell` 指定用户`shell` 
- `-p` `--password` 用户密码

```shell
useradd -m user -s /bin/bash
```

*`groupadd` 添加组* 

```
Usage: groupadd [option] GROUP
```

*`passwd` 用户密码*

```
Usage: passwd USER
```



### 权限

*`chmod` 文件授权*

```shell
Usage: chmod [option] MODE FILE
eg: 
sudo chmod -R 775 /var/www/html
```



- `-R` `--recursive`  递归

*`chown` 角色分配*

```shell
Usage: chown [option] [OWNER]:[GROUP] FILE
eg: 
sudo chown -R user:group /var/www/html
```

- `-R` `--recursive` 递归

### 文件/目录

*`ls` 文件列表*

- `-a` 列出所有文件
- `-l` 文件详细信息

```shell
eg:
ls 列当前目录下所有文件或目录（不包含隐藏文件）
ls -a 列出当前目录下所有文件（显示隐藏文件）
ls -l 显示文件详细信息
ls -al /var/www
```

*`cd` 切换当前目录*

```shell
cd ~ 回到home目录
cd .. 回到上级目录
```

*`mkdir` 创建目录*

*`rmdir` 删除空目录*

*`rm` 删除文件/目录*

- `-r` `--recursive` 递归
- `-f` `--force` 强制

```shell
rm -rf /var/www/html
```

*`cp` 复制文件/目录*

- `-R` `--recursive`
- `-f` `--force`

```shell
cp -R ~/a /var/www/a
```

*`mv` 移动/重命名文件/目录*

```shell
mv ~/a ~/b
mv ~/c /var/www/c
```



### 压缩

*`tar`*

- `-c` 压缩
- `-t` 查看内容
- `-u` 更新压缩包内容
- `-x` 解压
- `-r` 压缩文件追加文件
- `-z` `gzip`
- `-j` `bz2`
- `-Z` `compress`
- `-v` 详情
- `-O` 输出`stdout`
- `-C` 指定目录

```shell
压缩
tar -cvf *.tar * 
tar -cvzf *.tar.gz *
tar -cvjf *.tar.bz2 *
tar -cvZf *.tar.Z * compress压缩

解压
tar -xvf *.tar 
tar -xzvf *.tar.gz
tar -xjvf file.tar.bz2 解压 tar.bz2
tar -xZvf file.tar.Z 解压tar.Z
tar -xvf file.tar -C /var/www 指定目录解压
```

*`zip`*



### 系统版本

- `cat /proc/version`
- `uname -a`
- `lsb_release -a`
- `cat /etc/issue`

### 磁盘

*`fdisk` 磁盘列表*

```shell
fdisk -l
```

*`df` 磁盘使用情况*

```shell
df -h
```



*`du` 目录占用*

- `-s` 非递归展示
- `-h` 根据大小展示 eg: 1k 256M 2G
- `-m` 展示单位M
- `-k` 展示单位K



### 进程



`ps`

```shell
ps -ef
```



### 软件

*`apt`*

```shell
sudo apt-get install software 安装
sudo apt-cache search software 搜索
```

```
软件默认安装目录：/var/lib/
启动脚本目录：/etc/init.d
```







