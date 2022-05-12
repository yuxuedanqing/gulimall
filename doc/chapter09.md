# 环境-配置 docker 阿里云镜像加速

登录阿里云，搜索容器镜像服务，左侧菜单栏找到镜像工具->镜像加速器

找到 CentOS 的配置：

1. 安装／升级Docker客户端
   推荐安装1.10.0以上版本的Docker客户端，参考文档docker-ce

2. 配置镜像加速器
   针对Docker客户端版本大于 1.10.0 的用户

您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
"registry-mirrors": ["https://自己的特码.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

将以上语句挨个在虚拟机上执行