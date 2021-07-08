## zabbix监控nginx

1. 检查是否开启`Stub Status`模块

   检查是存在`--with-http_stub_status_module`

   ```shell
   >nginx -V
   configure arguments: --with-cc-opt='-g -O2 -fdebug-prefix-map=/build/nginx-KTLRnK/nginx-1.18.0=. -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -fPIC' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-debug --with-compat --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --with-http_addition_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_image_filter_module=dynamic --with-http_sub_module --with-http_xslt_module=dynamic --with-stream=dynamic --with-stream_ssl_module --with-mail=dynamic --with-mail_ssl_module
   ```

   

2. 配置nginx代理服务

   在nginx主服务中配置如下内容：

   ```shell
   server {
   	listen 80 default_server;
       listen [::]:80 default_server;
   	...
   	location /nginx_status {
   		stub_status on; // 启用模块
   		access_log off;
   		allow 127.0.0.1; // 只允许本机访问
   		deny all;
   	}
   }
   ```

   

3. 重启nginx服务

   ```shell
   >sudo nginx -t 
   >sudo systemctl restart nginx
   ```

   

4. 测试服务

   ```shell
   >curl http://127.0.0.1/status
   Active connections: 979 
   server accepts handled requests
    756072922 756072922 1136799890 
   Reading: 0 Writing: 4 Waiting: 975
   ```

   备注：

   Active connections –当前活跃的连接数量 
   server accepts handled requests — 总共处理了756072922个连接 , 成功创建 756072922次握手, 总共处理了1136799890个请求
   reading — 读取客户端的连接数.
   writing — 响应数据到客户端的数量
   waiting — 开启 keep-alive 的情况下,这个值等于 active – (reading+writing), 意思就是 Nginx 已经处理完正在等候下一次请求指令的驻留连接.



5. zabbix配置

   ```shell
   >cp /etc/zabbix/zabbix_agentd.d/userparameter_mysql.conf /etc/zabbix/zabbix_agentd.d/userparameter_nginx.conf
   >vim /etc/zabbix/zabbix_agentd.d/userparameter_mysql.conf 
   
   # 替换
   UserParameter=nginx.active,curl -s http://127.0.0.1/nginx_status  2>/dev/null| grep 'Active' | awk '{print $NF}'
   UserParameter=nginx.reading,curl -s http://127.0.0.1/nginx_status 2>/dev/null| grep 'Reading' | awk '{print $2}'
   UserParameter=nginx.writing,curl -s http://127.0.0.1/nginx_status 2>/dev/null| grep 'Writing' | awk '{print $4}'
   UserParameter=nginx.waiting,curl -s http://127.0.0.1/nginx_status 2>/dev/null| grep 'Waiting' | awk '{print $6}'
   UserParameter=nginx.accepts,curl -s http://127.0.0.1/nginx_status 2>/dev/null| awk NR==3 | awk '{print $1}'
   UserParameter=nginx.handled,curl -s http://127.0.0.1/nginx_status 2>/dev/null| awk NR==3 | awk '{print $2}'
   UserParameter=nginx.requests,curl -s http://127.0.0.1/nginx_status 2>/dev/null| awk NR==3 | awk '{print $3}'
   ```

6. 重启zabbix服务

   ```shell
   >sudo systemctl restart zabbix-agent
   ```

7. 监控项配置

8. 图形配置
