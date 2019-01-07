# Install

安装最新的7版本即可

# Requirements

初级运维即可完成

# Setting

```bash
#关闭selinux
setenforce 0
sed -i 's/=enforcing/=disabled/g' /etc/selinux/config

#关闭service
ServiceList={firewalld,}
for ServiceName in ServiceList; do
    systemctl $ServiceName firewalld
    systemctl $ServiceName firewalld
done
```



