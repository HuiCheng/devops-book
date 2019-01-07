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
    systemctl stop    $ServiceName
    systemctl disable $ServiceName
done

#时间同步
yum install ntp
cat << EOF > /etc/ntp.conf
# ntp.conf
logfile    /var/log/ntp.log
pidfile    /var/run/ntpd.pid
driftfile  /var/lib/ntp/drift

# Access Control Support
restrict    127.0.0.1
restrict    default kod nomodify notrap nopeer noquery
restrict -6 default kod nomodify notrap nopeer noquery

# local clock
server 127.127.1.0
fudge  127.127.1.0 stratum 10

server   ntp1.aliyun.com          iburst minpoll 4 maxpoll 10
restrict ntp1.aliyun.com          nomodify notrap nopeer noquery

server   ntp2.aliyun.com          iburst minpoll 4 maxpoll 10
restrict ntp2.aliyun.com          nomodify notrap nopeer noquery
EOF
systemctl enable  ntpd
systemctl restart ntpd

```



