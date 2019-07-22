挂载共享文件夹
1. virtualbox安装增强功能
2. 进入VBox_GAs，安装VBoxLinuxAdditions.run
3. 设置virtuabox共享文件夹
4. 再linux中挂载
```
sudo mount -t vboxsf code /code
```
5. 编辑/etc/fstab文件，添加一行下面的代码，设置开机自动挂载
```
code /code vboxsf rw,gid=110,uid=1100,auto 0
```



