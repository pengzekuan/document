server {
        listen 80;
        server_name www.test.com;
        location / {
                proxy_pass http://abc.com;
                proxy_set_header    Host             $host;#保留代理之前的host
                proxy_set_header    X-Real-IP        $remote_addr;#保留代理之前的真实客户端ip
                proxy_set_header    X-Forwarded-For  $proxy_add_x_forwarded_for;
                proxy_set_header    HTTP_X_FORWARDED_FOR $remote_addr;#在多级代理的情况下，记录每次代理之前的客户端真实ip
                proxy_redirect      default;#指定修改被代理服务器返回的响应头中的location头域跟refresh头域数值
        }
}