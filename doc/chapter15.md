# 环境 - 数据库初始化

让 mysql 和 redis 开机自启

```shell
sudo docker update redis --restart=always
sudo docker update mysql --restart=always
```

重启虚拟机

```shell
vagrant reload
```