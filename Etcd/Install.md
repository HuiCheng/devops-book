


# Install

```bash
BasePath=/data/apps/etcd/
Name=k8s-01
ProjectPath=$BasePath/$Name/

PeerPORT=2380
PeerAddress=172.11.51.201   #每个节点需要单独配置 要在下面列表中
ClientPORT=2379
ClientAddress=172.11.51.201 #每个节点需要单独配置 要在下面列表中

NODE01=172.11.51.201
NODE02=172.11.51.202
NODE03=172.11.51.203
```

# Requirements

初级运维即可完成

# Setting

#### 配置文件

```bash
mkdir -p $ProjectPath; cd $ProjectPath
mkdir -p data/{data,conf,dockerfile}/
```

#### Dockerfile

```bash
cat << EOF > data/dockerfile/Dockerfile
FROM alpine:3.8
ENV PKGS bash curl keepalived tzdata
RUN apk add --no-cache \$PKGS && \
ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
test -f /usr/local/bin/gobetween || \
curl -sSL https://github.com/yyyar/gobetween/releases/download/0.6.1/gobetween_0.6.1_linux_amd64.tar.gz | \
tar xzf - -C /usr/local/bin/ gobetween
EOF
```

#### Docker-compose

```bash
cat << EOF > docker-compose.yaml
version: '2.2'
services:
gobetween:
build:
context: data/dockerfile/
command: gobetween -c /data/conf/gobetween
network_mode: "host"
volumes:
- ./data/:/data/
restart: always
keepalived:
build:
context: data/dockerfile/
command: keepalived -D -n -l
network_mode: "host"
volumes:
- ./data/conf/keepalived.conf:/etc/keepalived/keepalived.conf
restart: always
cap_add:
- NET_ADMIN
EOF
```

#### 启动

```bash
docker-compose up -d
```