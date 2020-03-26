# 安装

```
sudo apt-get update
sudo apt-get install openssh-client openssh-server openssh-sftp-server
```

检测安装

```
dpkg --get-selections | grep openssh
```

# 建立用户组和用户

```
sudo groupadd sftp-users
sudo useradd -g sftp-users -m admin
passwd admin

# 已创建用户添加到组
usermod –g sftp_users admin
```

# 配置

- 配置文件 `/etc/ssh/sshd_config`
- X11Forwarding no
- AllowTcpForwarding no 
- Subsystem sftp internal-sftp 使用ssh自带sftp
- 配置sftp定位文件

  ```
  Match Group sftp-users # 指定用户组
    ChrootDirectory %h # 指定ftp根目录，指定目录为`root`用户，root可读写执行，其他用户可读；用户目录
    ForceCommand internal-sftp
  ```
- AllowUsers 如果原先设置了此参数，则需要把sftp用户加入其中
