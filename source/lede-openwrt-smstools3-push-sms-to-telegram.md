title: Openwrt/LEDE 利用 3G 上网卡推送短信到 Telegram/微信
tags:
  - LEDE
  - Openwrt
  - smstools3
  - Telegram
  - 微信
date: 2017-06-08 17:17:21
---

之前咸鱼买了俩 3g 上网卡，型号是 zte mf637u,路由器是 tp 的 wr703n  
感觉手机卡就收个短信太浪费，就插路由器上了（雾  
顺便折腾一下路由器，光是转码这个翻了老半天，帖子都是 N 年前的……  
以下是安装步骤  

将3g网卡插入路由并安装依赖软件
```shell
opkg update
opkg install kmod-usb-serial kmod-usb-serial-wwan kmod-usb-serial-option usb-modeswitch smstools3
```
编辑push脚本
vi /usr/local/bin/pushsms

```shell
#!/bin/sh

if [ "$1" == "RECEIVED" ]; then

  FROM=$(grep "From:" $2)
  TEXT=$(sed -e '1,/^$/ d' < "$2" | iconv -f UNICODEBIG -t UTF-8)

  curl -d "chat_id=<your id>&text=$TEXT%0a$FROM" -X POST https://api.telegram.org/bot<token>/sendMessage

fi
```
给执行权限 `chmod +x /usr/local/bin/pushsms`  
编辑smstools3配置文件
vi /etc/smsd.conf

```shell
#
# Description: Main configuration file for the smsd
#

devices = GSM1
incoming = /var/spool/sms/incoming
outgoing = /var/spool/sms/outgoing
checked = /var/spool/sms/checked
failed = /var/spool/sms/failed
sent = /var/spool/sms/sent
receive_before_send = no
autosplit = 3
eventhandler = /usr/local/bin/pushsms

[GSM1]
init = AT+CPMS="ME","ME","ME"
signal_quality_ber_ignore = yes
check_memory_method = 2
device = /dev/ttyUSB1
incoming = yes
#pin = 0000
baudrate = 115200
```
重启smsd进程  
```shell
/etc/init.d/smstools3 restart
```

另外如果不能直连api.telegram.org的话建议在 网络=>DHCP/DNS=>DNS转发 中填入 `/telegram.org/208.67.222.222#5353` 即可

![wr703n and zte mf637u](https://ww4.sinaimg.cn/large/a15b4afegy1fgdx5yvhbzj21hc14043f.jpg)
