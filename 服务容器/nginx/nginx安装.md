## Windows安装

1. 下载安装包

    浏览器打开[下载地址](http://nginx.org/en/download.html)，选择需要下载的版本，下载软件包；

2. 安装包解压

    找到下载好的软件包，解压到系统软件安装位置

3. 启动服务

    start nginx

4. 检查服务进程

    检测命令如下：

    ```
    tasklist /fi "imagename eq nginx.exe"
    ```

    如服务已启动，会看到至少2个nginx服务进程，其中一个为服务主进程，其余为工作进程。

5. 服务日志

    - `access_log` 
        
        访问日志，默认文件位置 `logs\error.log`

    - `error_log` 
    
        错误日志，默认文件位置 `logs\access.log`


6. 服务操作

    ```
    # 暂停服务
    nginx -s stop
    # 退出服务
    nginx -s quit
    # 重启服务
    nginx -s reload
    # 重新打开服务（日志归档）
    nginx -s reopen
    ```

7. 注册服务


    1. 下载服务注册工具[WinSW](https://github.com/winsw/winsw)
    2. 拷贝服务注册工具`WinSW`到`nginx`根目录下，可为其重命名
    3. 在`nginx`根目录新建与工具名称同名的`xml`配置文件，如工具名称为`winsw.exe`,则新建文件名称为`winsw.xml`
    4. 配置文件内容如下：

    ```
    <service>
        <id>nginx</id>
        <name>nginx</name>
        <description>nginx</description>
        <logpath>D:\tools\nginx-1.18.0\logs</logpath>
        <logmode>roll</logmode>
        <depend></depend>
        <executable>D:\tools\nginx-1.18.0\nginx.exe</executable>
        <stopexecutable>D:\tools\nginx-1.18.0\nginx.exe -s quit</stopexecutable>
    </service>
    ```
    5. 注册服务

        ```
        winsw install
        ```
    6. 卸载服务

        ```
        winsw uninstall
        ```
    7. 服务控制

        ```
        winsw start|stop|restart|status
        ```