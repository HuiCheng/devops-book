# Install

```shell
BasePath=/data/apps/VIP/
Name=k8s-01
ProjectPath=$BasePath/$Name/
VIP=172.16.190.200

mkdir -p $ProjectPath
cd $ProjectPath

mkdir -p data/{data,conf,dockerfile}/
cat << EOF > data/conf/healthcheck.sh
timeout 2 curl -k https://\$1:\$2/ 2>&1 > /dev/null
if [ "$?" == "0" ]; then
    echo -n 1
else
    echo -n 0
fi
    
EOF


cat << EOF > data/conf/gobetween

EOF

cat << EOF > data/conf/keepalived.conf
EOF

cat << EOF > docker-compose.yaml
version: '2.2'
services:
  caddy:
    image: registry.cn-beijing.aliyuncs.com/vipdax/01:ykt-php-v4
    command: caddy --conf=/data/Caddyfile
    ports:
    - 9000:9000
    volumes:
    - ./data/data/:/data/
    restart: always
EOF

docker-compose up -d

```

# Requirements

初级运维即可完成

# Setting

#### 配置文件
```bash
```

#### 启动
```bash
```

