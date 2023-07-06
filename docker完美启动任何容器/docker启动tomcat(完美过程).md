# docker启动tomcat

## 第一步拉镜像

这里用9.0版本作为演示

```bash
docker pull tomcat:9.0
```

## 第二步完美的创建容器

```bash
1.先简单运行一下tomcat
docker run -d -p 3355:8080 --name tomcat01 tomcat

2.创建挂载目录
mkdir -p /root/tomcat/conf
mkdir -p /root/tomcat/logs
mkdir -p /root/tomcat/webapps

3.拷贝
docker cp tomcat01:/usr/local/tomcat/conf /root/tomcat/   #docker的复制是把整个conf文件夹复制过来
docker cp tomcat01:/usr/local/tomcat/webapps /root/tomcat/   
docker cp tomcat01:/usr/local/tomcat/logs /root/tomcat/ 

4.关闭一开始创建的容器
docker stop tomcat01

5.重新创建一个完美容器
docker run --name tomcat -p 8080:8080 -v /root/tomcat/logs:/usr/local/tomcat/logs   -v /root/tomcat/webapps:/usr/local/tomcat/webapps -v /root/tomcat/conf:/usr/local/tomcat/conf -d tomcat:9.0
```

## 第三步检测

```bash
 curl 127.0.0.1:8080
<!doctype html><html lang="en"><head><title>HTTP Status 404 – Not Found</title><style type="text/css">body {font-family:Tahoma,Arial,sans-serif;} h1, h2, h3, b {color:white;background-color:#525D76;} h1 {font-size:22px;} h2 {font-size:16px;} h3 {font-size:14px;} p {font-size:12px;} a {color:black;} .line {height:1px;background-color:#525D76;border:none;}</style></head><body><h1>HTTP Status 404 – Not Found</h1><hr class="line" /><p><b>Type</b> Status Report</p><p><b>Description</b> The origin server did not find a current representation for the target resource or is not willing to disclose that one exists.</p><hr class="line" /><h3>Apache Tomcat/9.0.76</h3></body></html>
```

出现这个是成功的标志，因为在docker里面的tomcat是没有基本的页面的，不信的话，各位可以去webapps里面查看一下