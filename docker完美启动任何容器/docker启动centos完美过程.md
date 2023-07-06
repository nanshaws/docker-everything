# docker启动centos

## 第一步拉取镜像

```java
docker pull centos:7
```

这里要注意的是，7版本和8版本的yum地址不一样

如果用centos7版本的就可以不用换yum镜像了

## 第二步创建容器

```bash
docker run -it -d --name centos001 centos /bin/bash
```

## 第三步进入容器

```bash
docker exec -it centos001 /bin/bash
```

## 第四步测试yum镜像

```bash
yum install vim
```

## 第五步查看结果

```bash
Installed:
  vim-enhanced.x86_64 2:7.4.629-8.el7_9

Dependency Installed:
  gpm-libs.x86_64 0:1.20.7-6.el7                               groff-base.x86_64 0:1.22.2-8.el7
  perl.x86_64 4:5.16.3-299.el7_9                               perl-Carp.noarch 0:1.26-244.el7
  perl-Encode.x86_64 0:2.51-7.el7                              perl-Exporter.noarch 0:5.68-3.el7
  perl-File-Path.noarch 0:2.09-2.el7                           perl-File-Temp.noarch 0:0.23.01-3.el7
  perl-Filter.x86_64 0:1.49-3.el7                              perl-Getopt-Long.noarch 0:2.40-3.el7
  perl-HTTP-Tiny.noarch 0:0.033-3.el7                          perl-PathTools.x86_64 0:3.40-5.el7
  perl-Pod-Escapes.noarch 1:1.04-299.el7_9                     perl-Pod-Perldoc.noarch 0:3.20-4.el7
  perl-Pod-Simple.noarch 1:3.28-4.el7                          perl-Pod-Usage.noarch 0:1.63-3.el7
  perl-Scalar-List-Utils.x86_64 0:1.27-248.el7                 perl-Socket.x86_64 0:2.010-5.el7
  perl-Storable.x86_64 0:2.45-3.el7                            perl-Text-ParseWords.noarch 0:3.29-4.el7
  perl-Time-HiRes.x86_64 4:1.9725-3.el7                        perl-Time-Local.noarch 0:1.2300-2.el7
  perl-constant.noarch 0:1.27-2.el7                            perl-libs.x86_64 4:5.16.3-299.el7_9
  perl-macros.x86_64 4:5.16.3-299.el7_9                        perl-parent.noarch 1:0.225-244.el7
  perl-podlators.noarch 0:2.5.1-3.el7                          perl-threads.x86_64 0:1.87-4.el7
  perl-threads-shared.x86_64 0:1.43-6.el7                      vim-common.x86_64 2:7.4.629-8.el7_9
  vim-filesystem.x86_64 2:7.4.629-8.el7_9                      which.x86_64 0:2.20-7.el7

Complete!
```

## 关于centos8的换源方案

本人极其不推荐centos8版本的，但为了保持完美这里我还是说一下如何更换centos8的镜像(这里的centos001是8版本的)

```bash
1.在宿主机上创建文件夹centos8Test

2.将容器/etc/yum.repos.d/   这个目录里面的东西全部移动到bak里面
cd /etc/yum.repos.d/
mkdir bak
mv * bak/

3.下载阿里云的文件
wget https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo -O /root/centos8Test/Centos-vault-8.5.2111.repo
wget https://mirrors.aliyun.com/repo/epel-archive-8.repo -O /root/centos8Test/epel-archive-8.repo

4.docker的拷贝到容器的yum那边
docker cp ./Centos-vault-8.5.2111.repo centos001:/etc/yum.repos.d/Centos-vault-8.5.2111.repo
docker cp ./epel-archive-8.repo centos001:/etc/yum.repos.d/epel-archive-8.repo

5.进入容器
docker exec -it centos001 /bin/bash

6.执行命令清空缓存
yum clean all && yum makecache
```

