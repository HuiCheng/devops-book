# Install

```bash
BasePath=/data/apps/etcd/
Name=k8s-01
ProjectPath=$BasePath/$Name/

PeerPORT=2380
PeerAddress=172.11.51.201   #每个节点需要单独配置 属于下面列表中元素
ClientPORT=2379
ClientAddress=172.11.51.201 #每个节点需要单独配置 属于下面列表中元素

Token=012312fasfhsdhfsdfio3

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
  etcd:
    image: registry.cn-hangzhou.aliyuncs.com/google_containers/etcd-amd64:3.2.24
    command: etcd-3.2.24
    network_mode: "host"
    environment:
    - ETCD_DATA_DIR=/data/
    - ETCD_LISTEN_CLIENT_URLS=http://$ClientAddress:$ClientPORT
    - ETCD_ADVERTISE_CLIENT_URLS=http://$ClientAddress:$ClientPORT
    - ETCD_LISTEN_PEER_URLS=http://$PeerAddress:$PeerPORT
    - ETCD_INITIAL_ADVERTISE_PEER_URLS=http://$PeerAddress:$PeerPORT
    - ETCD_INITIAL_CLUSTER_TOKEN=$Token
    - ETCD_INITIAL_CLUSTER=node01=http://$NODE01:$PeerPORT,node02=http://$NODE02:$PeerPORT,node03=http://$NODE03:$PeerPORT
    volumes:
    - ./data/data/:/data/
    restart: always
EOF
```

#### 启动

```bash
docker-compose up -d
```



