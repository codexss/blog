title: 一个简易的 PC 浏览器同步手机当前打开网页的方案
tags:
  - Chrome
  - Safari
  - iOS
  - https
date: 2018-04-21 20:57:44
---
有时候 PC 上浏览了个页面想在手机上打开，但是 PC 的 Chrome 跟手机 Safari 的历史记录没有同步，扫二维码也不是特别方便，我做了个书签，搭配一个 php 使用。 

php 源文件如下，只是获取 url 之后写到一个 txt 里面暂存 url 

u.php  
```
<?php  
header('Access-Control-Allow-Origin:*');  
if ($_GET["url"]) {  
fwrite(fopen("url.txt","w"),$_GET["url"]);  
echo "Success";  
} else {  
header('Location: '.file_get_contents('url.txt'));  
}  
?>
```

Crhome 书签地址如下 
```
javascript:xmlhttp=new XMLHttpRequest();xmlhttp.open("get","https://yourdomain/u.php?url="+window.location.href,true);xmlhttp.send();xmlhttp.onreadystatechange=function(){if (xmlhttp.readyState==4 && xmlhttp.status==200){alert("ok");}} 
```
实现的结果就是浏览器上点一下书签，然后手机上访问 https://yourdomain/u.php 就能跳转到你当前标记的网页了。 
