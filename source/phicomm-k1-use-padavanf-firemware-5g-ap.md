title: 斐讯K1刷Padavan固件实现中继5G WiFi信号
tags:
  - 中继
  - 路由器
  - K1
  - Padavan
  - WiFi
id: 67
date: 2016-09-11 16:06:06
---
淘宝弄了台斐讯K1，正好WNDR4300到我卧室的信号不太好，就拿来中继信号用了
<!--more-->
首先，我们刷上Breed不死BL，具体方法看这里

http://www.jianshu.com/p/ea0ea4305452

然后刷上我编译的精简过的Padavan固件，没有任何多余功能。

[RT-AC54U_3.4.3.9-099.trx](http://share.weiyun.com/5b76772951a38606448b262d920dc374)

![](//ws4.sinaimg.cn/large/a15b4afegw1f7pp4nsau0j20j10dgq3g)

刷完之后打开路由器的/Advanced_System_Content.asp页面，设置成中文

然后打开/Advanced_WMode_Content.asp用5G WiFi桥接至你的主路由的5G WiFi

![](//ws4.sinaimg.cn/large/a15b4afegw1f7ppaovgmej20q50f277w)

然后打开/Advanced_OperationMode_Content.asp设置工作模式为AP模式

![](//ws4.sinaimg.cn/large/a15b4afegw1f7ppcal2w9j20r30ccdiq)

保存，重启，大功告成。