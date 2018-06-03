# Template Nginx
在 Zabbix 中监控 MySQL 状态

# 版本
- Zabbix Server 3.0
- Zabbix Agent 3.0

# 安装
Zabbix安装在 `/etc/zabbix/` 目录下

## 添加MySQL用户

```shell
MariaDB [(none)]> GRANT USAGE ON *.* TO 'zabbix'@'localhost' IDENTIFIED BY '123456';
MariaDB [(none)]> FLUSH PRIVILEGES;
```

## 添加.my.cnf 配置文件
- [.my.cnf](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_mysql/.my.cnf)

```shell
# vim /etc/zabbix/.my.cnf
[mysql]
host=localhost
user=zabbix
password=123456
[mysqladmin]
host=localhost
user=zabbix
password=123456
```

## 添加User Parameter
- [userparameter_mysql.conf](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_mysql/userparameter_mysql.conf)

将 `userparameter_mysql.conf` 复制到 `/etc/zabbix/zabbix_agentd.d` 目录下。
重新启动`zabbix-agent`服务。

## 导入模板
- [template_mysql.xml](https://github.com/kangvcar/zabbix_monitoring_devices/blob/master/monitoring_mysql/template_mysql.xml)

在 Zabbix WEB 管理页面中导入模板文件 `template_mysql.xml` ,并将其链接到主机。