


# Install

```bash
BasePath=/data/apps/etcd/
Name=k8s-01
ProjectPath=$BasePath/$Name/

PeerPORT=2380
PeerAddress=172.11.51.201   #每个节点需要单独配置
ClientPORT=2379
ClientAddress=172.11.51.201 #每个节点需要单独配置

NODE01=172.11.51.201
NODE02=172.11.51.202
NODE03=172.11.51.203
```

# Requirements

初级运维即可完成

# Setting

#### 配置文件

```bash
docker pull registry.cn-hangzhou.aliyuncs.com/google\_containers/etcd-amd64:3.2.24

```