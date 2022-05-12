#### 环境-使用 vagrant 快速创建 Linux 虚拟机

1.下载安装 vagrant 和 virtualbox

vagrant 下载地址：https://www.vagrantup.com/downloads

vagrant 镜像仓库：https://app.vagrantup.com/boxes/search

virtualbox 下载地址：https://www.virtualbox.org/wiki/Downloads

2.初始化一个 centos7 系统

win + R 输入 cmd 回车,进入存放 Vagrantfile 文件的目录（eg: D:\vagrant）,输入如下语句，然后回车，会在D:\vagrant 下生成一个 Vagrantfile 文件

这里使用中科大的镜像

> 注意： 在当前这个小例子中，下面所有的 vagrant 命令都需要在 Vagrantfile 所在的目录（D:\vagrant）下执行。

```shell
vagrant init centos7 http://mirrors.ustc.edu.cn/centos-cloud/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box
```

3.启动虚拟环境

```shell
vagrant up
```

4.连接虚拟机

```shell
vagrant ssh
```

5.查看虚拟机状态

```shell
vagrant status
```

6.强制关闭虚拟机

```shell
vagrant halt
```

7.挂起虚拟机

> 挂起，相当于物理机中的休眠，会将内存中的数据全部存放到对应的休眠文件中，占用的空间为内存大小，并且会对虚拟机执行关机操作。休眠后的虚拟机不占任何CPU、内存。

> 可以使用挂起和恢复功能保存虚拟机的当前状态。在恢复虚拟机时，在挂起之前运行的应用程序将恢复运行状态，而不更改其内容。

> 执行恢复操作的速度取决于虚拟机的活跃程度。虚拟机越活跃，恢复所需的时间就越长。这还取决于虚拟机挂起状态（.vmss 或 .vmem）文件集是否已位于主机系统的物理内存中。如果是，虚拟机的恢复速度要快得多。

```shell
vagrant suspend
```

8.将挂起状态恢复运行

```shell
vagrant resume
```

9.重启虚拟机

```shell
vagrant reload
```

10.彻底删除虚拟机

```shell
vagrant destroy
```