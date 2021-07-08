1. zabbix客户端创建MySQL监控配置文件

   ```shell
   >sudo cp /usr/share/doc/zabbix-agent/userparameter_mysql.conf /etc/zabbix/zabbix_agentd.d/
   ```

   监控配置内容如下：

   ```shell
   #template_db_mysql.conf created by Zabbix for "Template DB MySQL" and Zabbix 4.2
   #For OS Linux: You need create .my.cnf in zabbix-agent home directory (/var/lib/zabbix by default) 
   #For OS Windows: You need add PATH to mysql and mysqladmin and create my.cnf in %WINDIR%\my.cnf,C:\my.cnf,BASEDIR\my.cnf https://dev.mysql.com/doc/refman/5.7/en/option-files.html
   #The file must have three strings:
   #[client]
   #user='zbx_monitor'
   #password='<password>'
   #
   UserParameter=mysql.ping[*], mysqladmin -h"$1" -P"$2" ping
   UserParameter=mysql.get_status_variables[*], mysql -h"$1" -P"$2" -sNX -e "show global status"
   UserParameter=mysql.version[*], mysqladmin -s -h"$1" -P"$2" version
   UserParameter=mysql.db.discovery[*], mysql -h"$1" -P"$2" -sN -e "show databases"
   UserParameter=mysql.dbsize[*], mysql -h"$1" -P"$2" -sN -e "SELECT COALESCE(SUM(DATA_LENGTH + INDEX_LENGTH),0) FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA='$3'"
   UserParameter=mysql.replication.discovery[*], mysql -h"$1" -P"$2" -sNX -e "show slave status"
   UserParameter=mysql.slave_status[*], mysql -h"$1" -P"$2" -sNX -e "show slave status"
   ```

   

2. 重启zabbix客户端服务

   ```shell
   sudo systemctl restart zabbix-agent
   ```

3. 新建MySQL监控用户

   ```shell
   CREATE USER 'zbx_monitor'@'%' IDENTIFIED BY '<password>';
   GRANT REPLICATION CLIENT,PROCESS,SHOW DATABASES,SHOW VIEW ON *.* TO 'zbx_monitor'@'%';
   ```

4. 新建MySQL监控用户配置文件`.my.cnf`

   配置文件位置：`/var/lib/zabbix/.my.cnf`

   配置里替换为新建的用户、密码

   ```shell
   [client]
   user='zbx_monitor'
   password='<password>'
   ```

   

/usr/share/doc/zabbix-agent/userparameter_mysql.conf