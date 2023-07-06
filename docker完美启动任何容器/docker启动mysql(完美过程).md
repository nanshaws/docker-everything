# docker启动mysql

## 第一步拉镜像

```bash
docker pull mysql:8.0
```

## 第二步完美的创建容器

```bash
1.创建挂载目录
mkdir mysql-conf
mkdir mysql-data
2.创建容器，这个mysql的容器启动的时候需要指定root密码
docker run -d -p 3310:3306 -v /root/mysql-conf:/etc/mysql/conf.d -v /root/mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:8.0
```

## 第三步检测

root:~/mysql-data# docker ps
CONTAINER ID   IMAGE       COMMAND                  CREATED         STATUS         PORTS                               NAMES
0e01088fcc50   mysql:8.0   "docker-entrypoint.s…"   4 minutes ago   Up 4 minutes   33060/tcp, 0.0.0.0:3310->3306/tcp   mysql01

用DBeaver测试一下

![image-20230706140116188](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230706140116188.png)