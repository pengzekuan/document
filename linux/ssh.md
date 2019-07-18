## ssh

**新增ssh用户**

- 添加用户
- 用户配置权限

```shell
sudo chmod +w /etc/sudoers
sudo vim /etc/sudoers

user ALL=(ALL:ALL) ALL    // 这一行为新添加的代码

sudo chmod -w /etc/sudoers
```

- ssh配置

```shell
vim /etc/ssh/sshd_config
Port xxx
PermitRootLogin        no  #禁止 ROOT 登陆
AllowUsers user
```

- 重启ssh

```shell
service sshd restart
```

