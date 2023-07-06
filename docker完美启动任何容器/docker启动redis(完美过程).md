# docker启动redis

## 第一步拉镜像：docker pull redis:版本号

## 第二步完美的创建容器：

```bash
1. 创建挂载目录
mkdir -p redis/data 
mkdir -p redis/conf
2.从redis官网下载redis配置文件，好像是说docker里面的redis没有这个配置文件
3.修改配置文件，并上传到redis/conf目录
#bind 127.0.0.1             #注释掉这部分,使redis可以外部访问
protected-mode no           #修改为no,去掉保护模式,让外网可以访问
daemonize no                #修改为no,不用守护线程的方式启动
requirepass 123456          #密码
appendonly yes              #redis持久化,默认是no
4.创建并运行容器
docker run -d -p 6379:6379 --name myredis -v /root/redis/conf/redis.conf :/etc/redis/redis.conf -v /root/redis/data:/data redis:7.0 redis-server /etc/redis/redis.conf --appendonly yes                         
```

## 第三步测试

这里用的是redis桌面版

![image-20230706105929291](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230706105929291.png)

![image-20230706110005970](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230706110005970.png)

成功！！！！！！