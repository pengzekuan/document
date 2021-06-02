## Windows

### 工具下载


下载服务注册工具[WinSW](https://github.com/winsw/winsw)

下载PHP进程管理工具[xxfpm](https://github.com/78/xxfpm)

### 工具迁移

拷贝服务注册工具`WinSW`到`PHP`根目录下，可为其重命名，如 `winsw.exe`

拷贝PHP进程管理工具中以下两个文件 `xxfpm.exe` 和 `pthreadGC2.dll`到`php`根目录；

### 配置文件

根目录新建配置文件，名称与`winsw`可执行文件名称一致，如 `winsw.xml`，文件内容如下，其中服务名称，php-cgi执行文件目录和启动端口号自行修改：

```xml
<service>
    <id>php-cgi-9000</id>
    <name>php-cgi-9000</name>
    <description>php-cgi-9000</description>
    <executable>D:/tools/php-7.3.24-Win32-VC15-x64/php-cgi.exe</executable>
    <startargument>-n</startargument>
    <startargument>1</startargument>
    <startargument>-i</startargument>
    <startargument>127.0.0.1</startargument>
    <startargument>-p</startargument>
    <startargument>9000</startargument>
    <stopexecutable>taskkill</stopexecutable>
    <stopargument>/F</stopargument>
    <stopargument>/IM</stopargument>
    <stopargument>xxfpm.exe</stopargument>
    <logpath>logs</logpath>
</service>
```

### 注册服务

```
cd PHP_ROOT
winsw install|uninstall
```

### 启动服务

```
net start winsw
```