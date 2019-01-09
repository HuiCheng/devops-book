# Install

```shell
BasePath=/data/apps/VIP/
Name=k8s-01
ProjectPath=$BasePath/$Name/
VIP=0.0.0.0
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
mkdir -p $ProjectPath; cd $ProjectPath
mkdir -p data/{data,conf,dockerfile}/

```

#### 健康检查脚本

```bash
cat << EOF > data/conf/healthcheck.sh
#/bin/bash
timeout 2 curl -k https://\$1:\$2/
if [ "\$?" == "0" ]; then; echo -n 1
else; echo -n 0; fi
EOF
```

#### 负载均衡配置

```bash
cat << EOF > data/conf/gobetween
[servers.k8s-vip]
bind     = "$VIP:$PORT"
protocol = "tcp"
balance  = "roundrobin"

max_connections      = 10000
client_idle_timeout  = "60m"
backend_idle_timeout = "60m"
backend_connection_timeout = "2s"

[servers.k8s-vip.discovery]
kind = "static"
static_list = [
    "$NODE01 weight=5",
    "$NODE02 weight=5",
    "$NODE03 weight=5"
]
EOF
```

#### 高可用配置

```bash
cat << EOF > data/conf/keepalived.conf
EOF
```

#### Dockerfile

```bash
cat << EOF > data/dockerfile/Dockerfile
FROM alpine:3.8
ENV  PKGS bash curl keepalived tzdata
RUN  apk add --no-cache \$PKGS && \
     ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
     test -f /usr/local/bin/gobetween || \
     curl -sSL https://github.com/yyyar/gobetween/releases/download/0.6.1/gobetween_0.6.1_linux_amd64.tar.gz | \
     tar xzf - -C /usr/local/bin/ gobetween
EOF
```


#### 启动

```bash
docker-compose up -d
```



