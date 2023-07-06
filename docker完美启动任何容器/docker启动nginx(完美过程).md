# docker启动nginx

## 第一步拉镜像

这个版本号不写就是最新的

```bash
docker pull nginx:版本号
```

## 第二步完美启动nginx容器

```bash
1.随便创建并运行一个nginx容器
docker run --name mynginx -p 80:80 -d --restart=always nginx:latest

2.创建对应的挂载目录
mkdir -p /data/nginx
mkdir -p /data/nginx/html/dist
mkdir -p /data/nginx/logs

3.复制nginx容器内的配置文件到对应的挂载目录下
1.首先复制nginx配置文件地址
docker cp mynginx:/etc/nginx /data/nginx
2.再复制nginx网页文件地址
docker cp mynginx:/usr/share/nginx/html /data/nginx/html/dist
3.最后复制nginx日志文件地址
docker cp mynginx:/var/log/nginx /data/nginx/logs

4.创建启动容器

5.检查nginx配置挂载目录成功！！！
docker run --name nginx01 -p 8001:80 -v /data/nginx/html/dist:/usr/share/nginx/html -v      /data/nginx/nginx/nginx.conf:/etc/nginx/ningx.conf -v /data/nginx/nginx/conf.d:/etc/nginx/conf.d -d nginx

6.把一开始的mynginx容器删了，接下来开始检测
7.经过本人测试，需要将/data/nginx/html/dist里面的html文件夹里面的index.html之类的移到外面(dist目录)，再将dist里面的html文件夹删除
```

## 第三步，检测

```bash
root# curl 127.0.0.1:8001
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

![image-20230706151616341](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230706151616341.png)