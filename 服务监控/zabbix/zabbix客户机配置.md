## zabbix agent 配置

1. 修改客户端配置项

   ```shell
   >sudo vim /etc/zabbix/zabbix_agentd.conf
   
   # 监控服务器IP地址
   Server=
   # 监控服务器IP地址
   ServerActive=
   # 客户机名称
   Hostname=
   ```

2. 重启客户端监控程序

   ```shell
   >sudo systemctl restart zabbix-agent
   ```

   

3. 新增监控主机