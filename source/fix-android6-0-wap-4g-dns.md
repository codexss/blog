title: 解决Android6.0版本WAP接入点4G网络下无法获取DNS的问题
tags:
  - Android
  - BUG
  - DNS
  - WAP
id: 11
date: 2016-07-01 10:16:51
---

要解决这个问题我们通过修改内核来实现
<!--more-->
首先下载解包工具，我用的是这个程序 [bootimg.exe](https://pan.baidu.com/s/1eRRaxbk)
然后提取出来手机的boot.img
首先查看boot所在分区
> adb shell su -c "ls -l /dev/block/platform/msm_sdcc.1/by-name|grep boot"

![](https://ooo.0o0.ooo/2016/06/30/5775ee3b47672.png)

然后提取到sd卡
> adb shell dd if=/dev/block/mmcblk0p19 of=/sdcard/boot.img

提取到PC
> adb pull /sdcard/boot.img d:/

然后解包boot.img (boot.img和bootimg.exe要在同一目录下)
> bootimg  --unpack-bootimg

在 initrd\init.rc 最后加上下面的内容并保存
```shell
on property:net.dns1=
setprop net.dns1 119.29.29.29
on property:net.rmnet0.dns1=
setprop net.rmnet0.dns1 119.29.29.29
```
最后重新打包
> bootimg --repack-bootimg

手动刷入boot-new.img即可

&nbsp;

部分内容参考自 淡淡的回忆