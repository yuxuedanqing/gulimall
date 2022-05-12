# 环境 - docker 安装 redis

**下载 redis 镜像**

> 切换到 root 用户进行安装

```shell
docker pull redis
```

**创建配置目录**

```shell
mkdir -p /mydata/redis/conf
touch /mydata/redis/conf/redis.conf
```

**启动 redis 实例**

```shell
docker run -p 6379:6379 --name redis -v /mydata/redis/data:/data \
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf
```

**查看运行中的容器**

```shell
docker ps
```

**进 redis 客户端查看**

```shell
docker exec -it redis redis-cli
```

由于 redis 默认配置是没有持久化的，redis 所有数据都存在内存中，所以重启 redis 再重新连接，之前保存的数据就没了

**重启 redis**

```shell
docker restart redis
```

想要持久化保存那就要修改 `/mydata/redis/conf/redis.conf` 配置文件，加入下面一行：

> 启用 AOF 的持久化方式

```shell
appendonly yes
```

