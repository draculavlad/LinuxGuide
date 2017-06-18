# centos-release-packages-added

## centos 6
```shell
rpm -Uvh http://fedora-epel.mirror.lstn.net/6/i386/epel-release-6-8.noarch.rpm   
```
## centos 7
```shell
rpm -Uvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
```
or 
```shell
yum install -y epel-release
```

# SetUpShadowSocksOnCentos
* now for centos7

## references:
(official instruction)[http://shadowsocks.org/en/download/servers.html]
(advance usage)[https://www.ifshow.com/centos-7-installation-and-configuration-shadowsocks/]

## shell script
```shell
yum update -y
yum install -y python-setuptools git && easy_install pip
pip install shadowsocks
sudo ssserver -p 443 -k ${your_password} -m aes-256-cfb --user nobody -d start
```

# Cloned Vmware Image Network Configuration
* for centos 6.6

1. modify /etc/udev/rules.d/70-persistent-net.rules 
delete info for eth0,  update name of interface eth1 with eth0. 
 
2. replace the mac addr in /etc/sysconfig/network-scripts/ifcfg-eth0 with the mac addr of interface eth0 after updating /etc/udev/rules.d/70-persistent-net.rules

* or
* repeate 1
* do a little change in /etc/sysconfig/network-scripts/ifcfg-eth0
* remove HWADDR and UUDI
* set onboot=yes
