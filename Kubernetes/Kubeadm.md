# Install

```bash
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF

VERSION=1.13.1-0
yum install -y kubelet-$VERSION kubeadm-$VERSION kubectl-$VERSION

systemctl start  kubelet
systemctl enable kubelet
```

# Requirements

初级运维即可完成

# Setting

#### 配置文件

```bash
```