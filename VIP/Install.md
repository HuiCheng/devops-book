# Install

```shell
BasePath=/data/apps/VIP/
Name=k8s-01
ProjectPath=$BasePath/$Name/

mkdir -p $ProjectPath
cd $ProjectPath

mkdir -p data/{data,conf}/
cat << EOF > data/conf/Caddyfile
EOF

cat << EOF > data/conf/Keepalived.conf
EOF

cat << EOF > docker-compose.yaml
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

