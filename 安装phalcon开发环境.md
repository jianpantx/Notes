安装phalcon开发环境
1. 下载[cphalcon](https://github.com/phalcon/cphalcon)，根据自己需要的版本切换版本分支安装，
2. 如果在多版本php环境，指定php版本编译安装phalcon扩展

```

git clone https://github.com/phalcon/cphalcon
cd cphalcon/build
sudo ./install --phpize /usr/bin/phpize7.3 --php-config /usr/bin/php-config7.3

```

如果使用的是homestead环境，在添加phalcon.ini的时候会分发号码前缀，这时候需要选择较大的数字（例如:50-phalcon.ini)。在Phalcon v4.0.0-alpha1版本说明中有记录，在安装4版本之前，需要安装psr扩展，具体信息看[这里](https://blog.phalconphp.com/post/upgrading-to-v4-alpha-1)

3. 安装好扩展之后，就可以安装 开发工具[phalcon-devtools](https://github.com/phalcon/phalcon-devtools)，安装步骤请看github。
注意：composer 安装，这里注意安装composer使用的php版本需要有phalcon扩展，否则无法安装。



