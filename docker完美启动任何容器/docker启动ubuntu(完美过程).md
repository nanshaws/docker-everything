# docker启动ubuntu

## 第一步拉镜像

```bash
docker pull ubuntu:版本号
```

## 第二步创建容器

```bash
docker run -it -d --name ubuntu001 ubuntu /bin/bash
```

## 第三步进入容器

```bash
docker exec -it ubuntu001 /bin/bash
```

## 第四步给ubuntu容器换源

```bash
1.进入容器内部(前题)

2.执行这两行指令,更改镜像
sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
sed -i s@/security.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list

3.执行apt的清空缓存和更新
apt-get clean            
apt-get update
```

注意：

如果执行到apt的清除的时候这条执行后出现了E: Could not get lock /var/lib/apt/lists/lock. It is held by process 21 (apt)  这种错误的话，就执行rm  /var/lib/apt/lists/lock 

## 第五步测试

```bash
1.执行apt install vim

Need to get 14.5 MB of archives.
After this operation, 61.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 libexpat1 amd64 2.4.7-1ubuntu0.2 [91.0 kB]
Get:2 http://mirrors.aliyun.com/ubuntu jammy/main amd64 libmpdec3 amd64 2.5.1-2build2 [86.8 kB]
Get:3 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 libpython3.10-minimal amd64 3.10.6-1~22.04.2ubuntu1.1 [810 kB]
Get:4 http://mirrors.aliyun.com/ubuntu jammy/main amd64 media-types all 7.0.0 [25.5 kB]
Get:5 http://mirrors.aliyun.com/ubuntu jammy/main amd64 readline-common all 8.1.2-1 [53.5 kB]
Get:6 http://mirrors.aliyun.com/ubuntu jammy/main amd64 libreadline8 amd64 8.1.2-1 [153 kB]
Get:7 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 libsqlite3-0 amd64 3.37.2-2ubuntu0.1 [641 kB]
Get:8 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 libpython3.10-stdlib amd64 3.10.6-1~22.04.2ubuntu1.1 [1832 kB]
Get:9 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 xxd amd64 2:8.2.3995-1ubuntu2.9 [53.8 kB]
Get:10 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 vim-common all 2:8.2.3995-1ubuntu2.9 [81.5 kB]
Get:11 http://mirrors.aliyun.com/ubuntu jammy/main amd64 libgpm2 amd64 1.20.7-10build1 [15.3 kB]
Get:12 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 libpython3.10 amd64 3.10.6-1~22.04.2ubuntu1.1 [1955 kB]
Get:13 http://mirrors.aliyun.com/ubuntu jammy/main amd64 libsodium23 amd64 1.0.18-1build2 [164 kB]
Get:14 http://mirrors.aliyun.com/ubuntu jammy-updates/main amd64 vim-runtime all 2:8.2.3995-1ubuntu2.9 [6827 kB]
Get:15 http://mirrors.aliyun.com/ubuntu jammy-updates/main am
```

成功！！！！
