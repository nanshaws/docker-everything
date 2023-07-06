# docker启动kibana

## 第一步拉镜像

```bash
docker pull kibana:(版本号)
```

## 第二步创建网络(如果在es那边创建完了网络的话，可以忽略)

```bash
docker network create es-net
```

## 第三步完美创建容器

```bash
docker run -d \
 --name kibana \
 -e ELASTICSEARCH_HOSTS=http://esTest:9200 \
 --network=es-net \
 -p 5601:5601 \
kibana:7.12.1
```

这个--network=es-net : 加入一个名为es-net的网络中，与elasticsearch在同一个网络中

-e ELASTICSEARCH_HOSTS=http://es:9200 : 设置elasticsearch的地址，因为kibana已经与elasticsearch在同一个网络，因此可以用容器名直接访问elasticsearch

## 第四步检测

```bash
root:~# docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED      STATUS          PORTS                    NAMES
ac2935194efc   kibana:7.12.1   "/bin/tini -- /usr/l…"   4 days ago   Up 17 seconds   0.0.0.0:5601->5601/tcp   kibana
```

