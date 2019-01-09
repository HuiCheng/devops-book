# Install

```shell

```

# Requirements

初级运维即可完成

# Setting

#### 配置文件
```bash
mkdir -p /etc/docker/
{
    "graph": "/data/apps/docker/",
    "log-opts": {"max-size": "1024m", "max-file": "10"},
    "live-restore": true,
    "registry-mirrors": ["https://h3vtnoaa.mirror.aliyuncs.com"]
}
EOF
```

#### 启动
```bash
systemctl start  docker
systemctl enable docker
```

