# docker启动elasticsearch

## 第一步拉镜像

```bash
docker pull elasticsearch:版本号
```

## 第二步完美的创建容器

```bash
1.创建挂载目录
mkdir es-data
mkdir es-plugs

2.将es-data设置为可以被写入的，因为es创建和启动的时候需要在里面写入一些东西
chmod 777 es-data

3.从github上下载ik和pinyin的分词器插件(可以不选，注意一定要和版本匹配)

4.创建网络
因为我还需要部署kibana容器，需要让es和kibana容器互联。这里先创建一个网络
docker network create es-net

5.创建容器,这里我使用的是elasticsearch:7.12.1
docker run -d \
    --name esTest \
    -e "ES_JAVA_OPTS=-Xms512m -Xmx521m" \
    -e "discovery.type=single-node" \
    -v es-data:/usr/share/elasticsearch/data \
    -v es-plugins:/usr/share/elasticsearch/plugins \
    --privileged \
    --network es-net \
    -p 9200:9200 \
    -p 9300:9300 \
elasticsearch:7.12.1
```

## 第三步，检测

```bash
root:~# docker run -d \
>     --name esTest \
>     -e "ES_JAVA_OPTS=-Xms512m -Xmx521m" \
>     -e "discovery.type=single-node" \
>     -v es-data:/usr/share/elasticsearch/data \
   -v es>     -v es-plugins:/usr/share/elasticsearch/plugins \
 --privi>     --privileged \
>     --network es-net \
   -p 92>     -p 9200:9200 \
>     -p 9300:9300 \
> elasticsearch:7.12.1
1d35d8d89fef1e343cbedd850dd176ef1f4e4150e81b7763d0f86c9e13c2a8ed
root:~# docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS              PORTS                                            NAMES
1d35d8d89fef   elasticsearch:7.12.1   "/bin/tini -- /usr/l…"   About a minute ago   Up About a minute   0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp   esTest
```

