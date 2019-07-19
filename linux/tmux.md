## tmux 快捷键



- 安装

```shell
sudo apt-get install tmux
```

- 新建会话

```shell
tmux [new -s sessionName [-n windowName]]
```

```shell
eg:
tmux
tmux -s session1
tmux -s session1 -n window1
```

- 进入会话

```shell
tmux at [-t sessionName]
```

- 会话列表

```shell
tmux ls
```

- 关闭会话

```shell
tmux kill-session -t sessionName
```



**会话内部操作**(加前置操作ctrl+b)

- 新建会话

```
:new
```

- 会话列表

```
ctrl+b+s
```

- 会话命名

```
ctrl+b+$
```

- 新窗口

```
ctrl+b+c
```

- 列窗口

```
ctrl+b+w
```

- 窗口切换

```
ctrl+b+p 前一个窗口
ctrl+b+n 后一个窗口
ctrl+b+N(1,2,3...) 指定窗口切换
```

- 窗口命名

```
ctrl+b+,
```

- 关闭窗口

```
ctrl+b+&
```

- 窗口风格

```
ctrl+b+% 垂直分割
ctrl+b+" 水平分割
ctrl+b+x 关闭窗格
ctrl+b+o 切换窗格
ctrl+b+q 展示窗格数字 按下数字切换
```

- 推出会话

```
ctrl+b+d
```

- 命令查询

```
ctrl+b+?
```



