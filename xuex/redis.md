### linux安装redis

必须安装gcc   redis 是基于gcc开发的

```
yum -y install gcc
yum -y install gcc-c++
```

```
$ wget http://download.redis.io/releases/redis-5.0.5.tar.gz
$ tar zxzf redis-5.0.5.tar.gz
$ cd redis-5.0.5
$ make MALLOC=libc

//安装后编译的文件目录
$ make PREFIX=/usr/local/redis install
```

```
cd /usr/local/redis
cd bin
./redis-server   //启动
./resis-cli     // 启动客户端
```

在解压文件里有个 redis.conf 配置文件

把解压文件的配置文件复制到 安装后编译的文件目录(/usr/local/redis/)  bin  目录里

Redis默认不是以守护方式运行 可以通过该配置修改 使用yes启用守护进程

```
daemonize no  //改为 yes
```

当Redis以守护进程