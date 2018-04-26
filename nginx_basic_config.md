## nginx文件服务配置
```
location / {
	root /usr/share/nginx/html;
	autoindex on;# 显示目录
	autoindex_exact_size on;# 显示文件大小
	autoindex_localtime on;# 显示文件时间
}
```
## nginx简单用户认证配置
### nginx配置
```
location / {
	auth_basic "secret";
	auth_basic_user_file /etc/nginx/users/users.db;
	proxy_pass http://localhost:8000;
}
```
### 加密密码命令
```{sh}	
openssl passwd -crypt 123456
```

### users.db
```
admin:hmQ.ZJWkch8aY
```
## nginx https配置
```
ssl                  on;
ssl_certificate      /etc/nginx/keys/fullchain.pem; # 证书
ssl_certificate_key  /etc/nginx/keys/privkey.pem;   # 私钥
```
## 常用日志格式
```
log_format  main  '$http_x_forwarded_for [$time_local] "$request" '
                  '$status $body_bytes_sent "$http_referer" '
                  '"$http_user_agent" "$upstream_addr" '
                  '$request_time "$upstream_response_time"';
```
