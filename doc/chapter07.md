# 环境-虚拟机网络设置

1.默认虚拟机的 ip 是不固定的，开发不方便，可以通过修改 Vagrantfile 文件内容的方式来设置固定ip

```shell
config.vm.network "private_network", ip: "192.168.56.10"
```

2.重启虚拟机

```shell
vagrant reload
```

3.进入虚拟机查看 ip 地址

```shell
vagrant ssh

ip addr
```

4.Windows ping 虚拟机

```shell
ping 192.168.56.10
```

5.虚拟机 ping Windows

```shell
ping -c 4 192.168.31.41 
```