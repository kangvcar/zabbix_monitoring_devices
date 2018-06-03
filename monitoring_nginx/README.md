# Template Nginx
在 Zabbix 中监控 Nginx 状态

# 版本
- Zabbix Server 3.0
- Zabbix Agent 3.0

# 安装
Zabbix安装在 `/etc/zabbix/` 目录下

## Nginx HttpStubStatusModule
Nginx需要使用`HttpStubStatusModule`构建，即编译时加入选项`--with-http_stub_status_module`。您可以使用nginx -V来检查当前的二进制文件是否包含此模块。

## 添加配置
- [nginx.conf]()
将以下内容添加到Nginx配置中：
```shell
server {
    listen       80;
    server_name  localhost;
    location /nginx_status {
        stub_status on;
        access_log off;
        allow 127.0.0.1;
        deny all;
    }
}
```
重新加载Nginx，并访问`curl http://127.0.0.1/nginx_status`获取统计信息。

## 安装脚本znginx.sh 
- [znginx.sh]()
创建目录 /etc/zabbix/scripts 并将 znginx.sh 脚本复制到该目录下。
赋予脚本执行权限。

## 添加User Parameter
- [userparameter_nginx.conf]()
将 userparameter_nginx.conf 复制到 /etc/zabbix/zabbix_agentd.d 目录下。
重新启动`zabbix-agent`服务。

## 导入模板
- [template_nginx.xml]()
在 Zabbix WEB 管理页面中导入模板文件 template_nginx.xml ,并将其链接到主机。如果需要，请设置主机宏{$ NGINX_STATUS_URL}。




