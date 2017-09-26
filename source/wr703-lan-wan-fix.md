title: 再次填坑：WR703单网口LAN/WAN识别问题的解决方案
tags:
  - 填坑
  - OpenWrt
  - WR703
id: 7
date: 2016-08-01 16:14:50
---

今天在网上查了下，没有什么好用的解决方案，所以我再吧这个坑填一下，很简单就可以搞定，利用Openwrt自带的的VLAN功能，不需要下载任何软件包.
<!--more-->
打开/etc/config/network
> vi /etc/config/network
然后修改**config interface**字段下的lan设置

在option ifname '**eth0**'中的网卡名后面加上"**.1**"，例如：
> option ifname '**eth0.1**'

然后再最后加上WAN的设置：
> config interface 'wan'
> option proto 'dhcp'
> option ifname 'eth0'

保存退出，重启network
> /etc/init.d/network restart

大功告成！

![](https://ooo.0o0.ooo/2016/08/01/579f041552ad3.png)

**注：发帖时WR703的固件版本号为OpenWrt Chaos Calmer 15.05.1**