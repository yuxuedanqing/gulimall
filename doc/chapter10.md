# 环境 - docker 安装 MySQL

**从 docker 仓库下载 mysql**

```shell
sudo docker pull mysql:5.7 
```

**启动容器**

```shell
sudo docker run -p 3306:3306 --name mysql \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7
```

**参数说明**

+ -p 3306:3306 将容器的 3306 端口映射到主机的 3306 端口
+ --name 为当前容器起一个名字  
+ -v /mydata/mysql/log:/var/log/mysql 将日志文件挂载到主机
+ -v /mydata/mysql/data:/var/lib/mysql 将数据文件夹挂载到主机
+ -v /mydata/mysql/conf:/etc/mysql 将配置文件挂载到主机
+ -e MYSQL_ROOT_PASSWORD=root 初始化 root 用户的密码
+ -d mysql:5.7 以后台运行，使用 mysql:5.7 镜像启动

vagrant 安装的虚拟机可以通过 `su root` 的方式切换到 root 用户，默认密码为 vagrant

**查看正在运行中的容器**

```shell
sudo docker ps
```

**进入 mysql 容器内部**

```shell
sudo docker exec -it 容器ID/容器名字 /bin/bash
```

**进入容器后查看容器结构**

```shell
ls /
```

可以看到是一个 linux 结构，所以一个容器可以认为就是一个小型的 linux。

**查看 mysql 安装到了哪里**

```shell
whereis mysql
```

**创建 mysql 配置文件**

回到 linux 虚拟机，在 `/mydata/mysql/conf` 新建一个 mysql 配置文件 my.cnf，配置内容如下:

> **Note\:** 这里需要切换到 root 用户进行操作

```shell
vi my.cnf
```

my.cnf 文件内容如下

```text
[client]
default-character-set=utf8mb4

[mysql]

# 设置mysql客户端默认字符集
default-character-set=utf8mb4

[mysqld]
init_connect='SET collation_connection = utf8mb4_unicode_ci'
init_connect='SET NAMES = utf8mb4'

max_connections=200

# 服务端使用的字符集默认为8比特编码的latin1字符集
skip-character-set-client-handshake
skip-name-resolve
character-set-server=utf8mb4
collation-server = utf8mb4_unicode_ci

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

**重启容器**

```shell
sudo docker restart mysql
```

**进入容器内部查看 mysql 配置**

```shell
sudo docker exec -it 容器ID/容器名字 /bin/bash
```

通过最上面的容器运行参数我们可以知道配置文件应当对于容器里的 `/etc/mysql/my.cnf`

查看 my.cnf 中的内容，预期结果和 linux 虚拟机中 `/mydata/mysql/conf/my.cnf` 内容一致

```shell
cat /etc/mysql/my.cnf
```
