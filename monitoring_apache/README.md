# Template Nginx
在 Zabbix 中监控 Apache 状态

# 版本
- Zabbix Server 3.0
- Zabbix Agent 3.0

# 安装
Zabbix安装在 `/etc/zabbix/` 目录下

## 配置apache支持server-status
- [httpd.conf](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/httpd.conf)

```shell
## 在apache主配置文件下加入如下配置
ExtendedStatus On  
<location /server-status>  
   SetHandler server-status  
   Order allow,deny  
   Allow from 127.0.0.1
</location>  
```
重新加载 Apache ，并访问`curl http://127.0.0.1/server-status`获取统计信息。

## 安装脚本zapache.sh 
- [zapache.sh](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/zapache.sh)

创建目录 `/etc/zabbix/scripts` 并将 `zapache.sh` 脚本复制到该目录下。
赋予脚本执行权限。

## 添加User Parameter
- [userparameter_apache.conf](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/userparameter_apache.conf.md)

将 `userparameter_apache.conf` 复制到 `/etc/zabbix/zabbix_agentd.d` 目录下。
重新启动`zabbix-agent`服务。

## 导入模板
- [Template_Apache_Stats.xml](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/Template_Apache_Stats.xml)

在 Zabbix WEB 管理页面中导入模板文件 `Template_Apache_Stats.xml` ,并将其链接到主机。