### 安装shadowscoks
```
apt-get install python-pip
pip install shadowsocks
```
配置shadowsocks文件，一般放在/etc文件夹：
```
sudo vi /etc/shadowsocks.json
```
也可以根据自己的习惯，方便以后修改，我的存放路径：
```
vi /home/xx/Software/ShadowsocksConfig/shadowsocks.json
```
配置信息：
```
{
  "server":"my_server_ip",
  "server_port":my_server_port,
  "local_address": "127.0.0.1",
  "local_port":1080,
  "password":"my_password",
  "timeout":300,
  "method":"aes-256-cfb"
}
```
测试启动：

- 前端启动 `sslocal -c /home/xx/Software/ShadowsocksConfig/shadowsocks.json`
- 后端启动：`sslocal -c /home/xx/Software/ShadowsocksConfig/shadowsocks.json -d start`
- 后端停止：`sslocal -c /home/xx/Software/ShadowsocksConfig/shadowsocks.json -d stop`
- 重启(修改配置要重启才生效)：`sslocal -c /home/xx/Software/ShadowsocksConfig/shadowsocks.json -d restart`

[sslocal失败解决方法](http://blog.hhzzer.com/posts/b9302e86/)

### 配置shadowsocks开机启动

使用systemd实现，创建shadowsocks文件：
```
sudo vim /etc/systemd/system/shadowsocks.service
```
在里面填写如下内容：
```
[Unit]
Description=Shadowsocks Client Service
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/sslocal -c /home/jianpan/software/ShadowsocksConfig/shadowsocks.json

[Install]
WantedBy=multi-user.target
```
注意：根据sslocal实际位置填写，可以通过`whereis sslocal`查看

配置生效，输入密码确认即可：
```
systemctl enable /etc/systemd/system/shadowsocks.service
```

### 配置终端代理，详细查看[这里](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/6-linux-setup-guide-cn.md)

终端内使用，需安裝 proxychains

```
sudo apt-get install proxychains
```

编辑 /etc/proxychains.conf，修改最后一行：

```
socks5 127.0.0.1 1080
```

接着我们就可以直接 用 proxychains + 命令的方式使用代理，例如

```
proxychains curl xxxx
proxychains wget xxxx

sudo proxychains apt-get xxxx
```
给 proxychains 设置别名，编辑.bashrc文件，尾部增加一行：
```
alias pc="proxychains"
```
生效配置：
```
source .bashrc
```

### 使用 Proxy SwitchyOmega 扩展，实现游览器代理
详情点 ，[这里](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/7-2-chrome-setup-guide-cn.md)

