如果使用nodejs 编写可以运行在Greengrass上的Lambda函数，必须使用`nodev6.10`版本，其他版本暂不支持。
网上大部分的教程是安装LTS版本的node,或者使用`n`或者`nvm`安装，这里使用的是直接在`Raspberry Pi 3B`
上使用编译好的文件进行安装。


**下载 nodejs 6.10**
```bash
cd ~/Downloads
wget https://nodejs.org/dist/v6.10.0/node-v6.10.0-linux-armv7l.tar.xz
```

解压 nodejs 6.10
```bash
tar -xvf node-v6.10.0-linux-armv7l.tar.xz
cd node-v6.10.0-linux-armv7l/
rm CHANGELOG.md
rm LICENSE
rm README.md
```

更换可执行文件的用户和用户组
```bash
sudo chown root:root *
```

拷贝到`/usr`下面
```bash
sudo cp -R * /usr/
```

检查node版本是否是v6.10
```
node -v
```

由于*greengrass*是检测$PATH下是否有`nodejs6.10`这个可执行文件，所以我们这里创建一个symbolic link.

```bash
cd /usr/bin
sudo ln -s /usr/bin/node nodejs6.10
```

# TroubleShooting

**Memory cgroup: Disabled**

如果你按照[Environment Setup for Greengrass](https://docs.aws.amazon.com/greengrass/latest/developerguide/module1.html)
但显示 `Memory cgroup: Disabled`, 请在`/boot/cmdline.txt` 中增加 `cgroup_enable=memory`和`cgroup_memory=1`，并且重启设备。



