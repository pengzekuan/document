# Zabbix

## 安装



​	前置条件

​	php php-bcmath php-gd2 php7.3-ldap nginx mysql



1. 安装zabbix库

   ```shell
   # wget https://repo.zabbix.com/zabbix/5.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.2-1+ubuntu18.04_all.deb
   # dpkg -i zabbix-release_5.2-1+ubuntu18.04_all.deb
   # apt update
   ```

   

2. 安装zabbix服务

   ```shell
   # apt install zabbix-server-mysql zabbix-frontend-php zabbix-nginx-conf zabbix-agent
   ```

   

3. 数据库初始化配置

   ```shell
   # mysql -uroot -p
   password
   mysql> create database zabbix character set utf8 collate utf8_bin;
   mysql> create user zabbix@localhost identified by 'password';
   mysql> grant all privileges on zabbix.* to zabbix@localhost;
   mysql> quit;
   ```

   

4. 配置zabbix服务数据库连接密码

   编辑文件 /etc/zabbix/zabbix_server.conf

   ```
   DBPassword=password
   ```

5. 配置zabbix服务监听口

   编辑文件/etc/zabbix/nginx.conf

   ```
   server {
           listen          80;
           server_name     server.example.com;
   
           root    /usr/share/zabbix;
   
           index   index.php;
   
           location = /favicon.ico {
                   log_not_found   off;
           }
   
           location / {
                   try_files       $uri $uri/ =404;
           }
   
           location /assets {
                   access_log      off;
                   expires         10d;
           }
   
           location ~ /\.ht {
                   deny            all;
           }
   
           location ~ /(api\/|conf[^\.]|include|locale) {
                   deny            all;
                   return          404;
           }
   
           location ~ [^/]\.php(/|$) {
                   fastcgi_pass    unix:/var/run/php/zabbix.sock;
                   fastcgi_split_path_info ^(.+\.php)(/.+)$;
                   fastcgi_index   index.php;
   
                   fastcgi_param   DOCUMENT_ROOT   /usr/share/zabbix;
                   fastcgi_param   SCRIPT_FILENAME /usr/share/zabbix$fastcgi_script_name;
                   fastcgi_param   PATH_TRANSLATED /usr/share/zabbix$fastcgi_script_name;
   
                   include fastcgi_params;
                   fastcgi_param   QUERY_STRING    $query_string;
                   fastcgi_param   REQUEST_METHOD  $request_method;
                   fastcgi_param   CONTENT_TYPE    $content_type;
                   fastcgi_param   CONTENT_LENGTH  $content_length;
   
                   fastcgi_intercept_errors        on;
                   fastcgi_ignore_client_abort     off;
                   fastcgi_connect_timeout         60;
                   fastcgi_send_timeout            180;
                   fastcgi_read_timeout            180;
                   fastcgi_buffer_size             128k;
                   fastcgi_buffers                 4 256k;
                   fastcgi_busy_buffers_size       256k;
                   fastcgi_temp_file_write_size    256k;
           }
   }
   
   ```

6. 启动服务

   ```
   # systemctl restart zabbix-server zabbix-agent nginx php7.3-fpm
   # systemctl enable zabbix-server zabbix-agent nginx php7.3-fpm
   ```

   

