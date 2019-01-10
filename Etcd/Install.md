


# Install

```bash
BasePath=/data/apps/etcd/
Name=k8s-01
ProjectPath=$BasePath/$Name/

PeerPORT=2380
PeerAddress=172.11.51.201   #每个节点需要单独配置 属于下面列表中元素
ClientPORT=2379
ClientAddress=172.11.51.201 #每个节点需要单独配置 属于下面列表中元素

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
mkdir -p data/data/
```

#### Docker-compose

```bash
cat << EOF > docker-compose.yaml
version: '2.2'
services:
  etcd:
    build:
      context: data/dockerfile/
    command: gobetween -c /data/conf/gobetween
    network_mode: "host"
    volumes:
    - ./data/data/:/data/
    restart: always
EOF
```

#### 启动

```bash
docker-compose up -d
```