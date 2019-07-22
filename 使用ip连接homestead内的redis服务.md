### 使用ip连接homestead内的redis服务
	修改redis配置文件（默认路径/etc/redis/redis.conf）
	```
	bind 127.0.0.1 //修改为 bind 0.0.0.0；
	```
	重启redis服务