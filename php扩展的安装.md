### phpredis的安装

下载源码包，[github](https://github.com/phpredis/phpredis/releases)

```
wget https://github.com/phpredis/phpredis/archive/4.3.0.tar.gz
```
解压

```
tar -zxvf 4.3.0.tar.gz
cd  phpredis-4.3.0
```

生成 configure 配置文件

```
/usr/bin/phpize7.2  //根据需要安装扩展的php版本，使用对应phpize，我使用的是7.2

./configure --with-php-config=/usr/bin/php-config7.2 //这里也需要选择对应版本配置
```

编译安装

```
make && sudo make install
```

最后在php.ini加载phpredis扩展

```
extension=redis.so
```

### swoole的安装

[github地址](https://github.com/swoole/swoole-src/blob/master/README-CN.md)

下载源码包，[github](https://github.com/swoole/swoole-src/releases)

```
wget https://github.com/swoole/swoole-src/archive/v4.3.5.tar.gz
```
解压

```
tar -zxvf v4.3.5.tar.gz

cd  swoole-src-4.3.5

```

生成 configure 配置文件

```
/usr/bin/phpize7.2  //根据需要安装扩展的php版本，使用对应phpize，我使用的是7.2

./configure --with-php-config=/usr/bin/php-config7.2 //这里也需要选择对应版本
```

编译安装

```
make && sudo make install
```

最后在php.ini加载phpredis扩展

```
extension=swoole.so
```

额外编译参数

![](https://raw.githubusercontent.com/jianpantx/Pics/master/img/20190621221344.png)

