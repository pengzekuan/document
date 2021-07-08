# 速率限制



```
# 一秒一个请求
http {
    limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;
    limit_conn_log_level error;
    limit_conn_status 503;
}

# 使用，配置5个等待队列，超出直接退出
server {
	limit_req zone=one burst=5 nodelay;
}

```



# 并发限制



```
# 并发上限5个
limit_conn_zone $server_name zone=perserver:10m;  
limit_conn perserver 5; 
```



