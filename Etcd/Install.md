


# Install

```bash
BasePath=/data/apps/VIP/
Name=k8s-01
ProjectPath=$BasePath/$Name/

RouterID=100
VRRP=ens33                              #用于发送VRRP协议的接口
VIP="172.16.190.100/24 dev ens33"       #VIP配置信息

PORT=6443
NODE01=172.11.51.201:6443
NODE02=172.11.51.202:6443
NODE03=172.11.51.203:6443
```

# Requirements

初级运维即可完成

# Setting

#### 配置文件

```bash
docker pull registry.cn-hangzhou.aliyuncs.com/google\_containers/etcd-amd64:3.2.24

```