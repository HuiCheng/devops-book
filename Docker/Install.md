# Install
---
```shell

export Version=18.06.1.ce-3.el7

yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yum -y install docker-ce-$Version
```

# Requirements
---
初级运维即可完成

# Setting
---

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

