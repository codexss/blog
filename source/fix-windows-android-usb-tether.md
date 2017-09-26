title: 关于Windows使用安卓USB共享网络的问题
tags:
  - Android
  - BUG
  - 网络共享
  - USB
  - Windows
id: 9
date: 2016-07-24 11:40:34
---

这可能是个windows的历史遗留问题，我的Nexus5在XP到Win10一直有打开USB共享之后电脑就卡死的情况

<!--more-->

设备管理器中，选择 usb 共享的那个网卡（一般是名字里有 NDIS 这几个字母的）， [![](https://ooo.0o0.ooo/2016/05/11/5732c2c42afa1.png)](https://ooo.0o0.ooo/2016/05/11/5732c2c42afa1.png)
然后右键，更新驱动程序，然后选下边那一项（从计算机设备列表中选取） [![](https://ooo.0o0.ooo/2016/05/11/5732c2c458b71.png)](https://ooo.0o0.ooo/2016/05/11/5732c2c458b71.png) ，
然后去掉“显示兼容设备”的对钩，然后在列表左边找到“ Microsoft ”，然后在右边拉到最下边，选择“远程 NDIS 兼容设备”这个，之后确定即可。 [![](https://ooo.0o0.ooo/2016/05/11/5732c2c461bee.png)](https://ooo.0o0.ooo/2016/05/11/5732c2c461bee.png)
[![](https://ooo.0o0.ooo/2016/05/11/5732c2c4a5811.png)](https://ooo.0o0.ooo/2016/05/11/5732c2c4a5811.png)
[![](https://ooo.0o0.ooo/2016/05/11/5732c2c4b7e83.png)](https://ooo.0o0.ooo/2016/05/11/5732c2c4b7e83.png)
[![](https://ooo.0o0.ooo/2016/05/11/5732c2c4c5d8b.png)](https://ooo.0o0.ooo/2016/05/11/5732c2c4c5d8b.png)

作者：杨晓恒
链接： [http://www.zhihu.com/question/35185870/answer/93712562](http://www.zhihu.com/question/35185870/answer/93712562)
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。