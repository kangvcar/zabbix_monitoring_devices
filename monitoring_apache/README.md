# 步骤概述：
- 使apache支持server-status
- 编写监控脚本
- 创建监控模板
- 创建图表

# 具体步骤：
1. 配置apache支持server-status
- apache配置文件所添加的内容[httpd.conf](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/httpd.conf)
```
## 在apache主配置文件下加入如下配置
ExtendedStatus On  
<location /server-status>  
   SetHandler server-status  
   Order allow,deny  
   Allow from 127.0.0.1
</location>  
```

2. 编写监控脚本
- 监控脚本：[zapache.sh](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/zapache.sh)
- 把脚本文件zapache放入 /etc/zabbix/scripts/目录下
- 赋予脚本zapache执行权限
```
chmod a+x zapache.sh
```

3. 修改zabbix-agent配置文件以支持自定义key
- zabbix-agent配置文件所添加的内容[userparameter_apache.conf](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/userparameter_apache.conf.md)
```
vim /etc/zabbix/zabbix_agentd.d/userparameter_apache.conf 
UserParameter=apache[*],/etc/zabbix/scripts/zapache.sh \$1
```

4. 在zabbix WEB 中导入apache监控模板，并link到运行apache的主机上
- 监控模板：[Template_Apache_Stats.xml](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_apache/Template_Apache_Stats.xml)

5. 重启Apache、zabbix-agent
```
service httpd restart
service zabbix-agent restart
```
