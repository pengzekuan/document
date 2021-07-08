## zabbix监控PHP-FPM

1. 修改`php-fpm`配置文件

   查找以下配置，取消注释，保存配置

   ```shell
   >sudo vim /etc/php/7.3/fpm/pool.d/www.conf
   
   ;pm.status_path = /status
   ;ping.path = /ping
   ```

2. 验证配置

   ```shell
   >sudo php-fpm7 -t
   ```

3. 重启服务

   ```shell
   >sudo systemctl restart php-fpm7		
   ```

4. 配置nginx服务

   在nginx主服务中配置如下内容：

   ```shell
   server {
   	listen 80 default_server;
       listen [::]:80 default_server;
   	...
   	location ~ ^/(status|ping)$ {
   		access_log off;
   		allow 127.0.0.1; // 只允许本机访问
   		deny all;
   		fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           fastcgi_index index.php;
           include fastcgi_params;
           ## Now the port or socket of the php-fpm pool we want the status of
           # fastcgi_pass 127.0.0.1:9000;
           fastcgi_pass unix:/run/php-fpm/your_socket.sock;
   	}
   }
   ```

   

5. 检查nginx配置

   ```shell
   >sudo nginx -t
   ```

   

6. 重启nginx服务

   ```shell
   >sudo systemctl restart nginx
   ```

   

7. 验证配置

   ```shell
   >curl http://127.0.0.1/status
   pool:                 www
   process manager:      dynamic
   start time:           08/Jul/2021:18:00:39 +0800
   start since:          1321
   accepted conn:        79
   listen queue:         0
   max listen queue:     0
   listen queue len:     0
   idle processes:       1
   active processes:     1
   total processes:      2
   max active processes: 1
   max children reached: 0
   slow requests:        0
   ```

   