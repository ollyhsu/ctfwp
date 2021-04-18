# 攻防世界WEB新手练习区Writeup

![image-20200402184013285](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-2020040218401328520200402184013.png)

## 001 view_source

![NYGssW20200401174309](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/NYGssW20200401174309.png)

打开链接，查看源码

![NP8dw720200401174416](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/NP8dw720200401174416.png)

得到Flag `cyberpeace{8fd345ebf032f889c4a154e9adb0d3e7}`

## 002 get_post

![image-20200401201930085](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-2020040120193008520200401215246.png)

![q0Pi0D20200401202017](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/q0Pi0D20200401202017.png)

利用HackBar 提交a=1

![DCLkEK20200401202131](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/DCLkEK20200401202131.png)

提交URL后得到页面

![mrTY2A20200401202230](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/mrTY2A20200401202230.png)

![ybaVnw20200401202247](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/ybaVnw20200401202247.png)

用HackBar 提交Post数据  b=2

![D9Xv9J20200401202330](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/D9Xv9J20200401202330.png)

得到Flag：`cyberpeace{cb63bbc87507234cccc4e46ad4865045}`

## 003 robots

![6DNqto20200401174637](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/6DNqto20200401174637.png)

题目提示该题目与robots协议相关，URL指向`robots.txt`

![onYTjv20200401174755](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/onYTjv20200401174755.png)

根据txt内容提示打开`f1ag_1s_h3re.php`

得到flag：`cyberpeace{94bf12fd1f3378e75ec1b6a2339ac053}`

## 004 backup

![KK6GzS20200401193149](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/KK6GzS20200401193149.png)

通过目录扫描脚本dirsearch扫描题目网站目录

![wlPPQZ20200401193127](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/wlPPQZ20200401193127.png)

扫描得到.bak文件，打开/index.php.bak，将下载该文件，

用Sublime打开该文件，即可得到Flag：`Cyberpeace{855A1C4B3401294CB6604CCC98BDE334}`

## 005 cookie

打开链接

![fyzgWH20200401193839](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/fyzgWH20200401193839.png)

根据题目提示找到cookie

![ta3NJa20200401194441](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/ta3NJa20200401194441.png)

在ur后指向cookie.php

![vQ8rHG20200401194502](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/vQ8rHG20200401194502.png)

查看http的返回

![mCNmfc20200401194343](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/mCNmfc20200401194343.png)

得到Flag：`cyberpeace{02d6d1081ac83cc9fdc0df1ccdd56c61}`

## 006 disabled_button

![cNeJZI20200401194647](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/cNeJZI20200401194647.png)

F12打开控制台，将按钮块`disabled=""`删除即可再次点击按钮

![bZZR9i20200401194859](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/bZZR9i20200401194859.png)



![9VQNrW20200401195108](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/9VQNrW20200401195108.png)

得到Flag：`cyberpeace{991772d1e43d58bf286216e5b4278769}`

## 007 weak_auth

![2oIdyk20200401195237](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/2oIdyk20200401195237.png)

打开链接，先尝试输入123和123，提示需要使用admin登陆

![nqtd8C20200401195431](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/nqtd8C20200401195431.png)

然后尝试用admin和admin登陆，提示密码错误

![GxrXnx20200401195749](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/GxrXnx20200401195749.png)

尝试用Burpsuite爆破密码

![bkJXOY20200401200305](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/bkJXOY20200401200305.png)

将其扔入Intruder，进行爆破

![aleB5s20200401200557](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/aleB5s20200401200557.png)

爆破出密码为123456，登陆得到Flag：`cyberpeace{42966aac2f0b0385028e7601a7bafd6d}`

## 008 simple_php

打开链接，阅读相关PHP代码

```php
<?php
show_source(__FILE__);
include("config.php");
$a=@$_GET['a'];
$b=@$_GET['b'];	//url接收参数a和b的值
if($a==0 and $a){
    echo $flag1;	//如果$a等于0 and $a，输出$flag1
}
if(is_numeric($b)){	//如果$b是数字或者字符串那么退出当前脚本
    exit();
}
if($b>1234){
    echo $flag2;	//如果$b>1234，输出$flag2
}
?>
```

所以，这里我们既要保证输出$a，$b，又要保证$b是数字，那么就用到php的弱类型比较了

所以可以构造`a=c&b=2222a`

![kpmLpQ20200401201746](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/kpmLpQ20200401201746.png)

得到Flag：`Cyberpeace{647E37C7627CC3E4019EC69324F66C7C}`



## 009 xff_referer

![uPuwCx20200401202543](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/uPuwCx20200401202543.png)

![1b9wFE20200401202624](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/1b9wFE20200401202624.png)

提示需要使用特定IP访问，利用X-Forwarded-For Header浏览器插件伪造IP

![image-20200401202813564](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-2020040120281356420200401215347.png)

然后提示`必须来自https://www.google.com`

![dsmobF20200401203803](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/dsmobF20200401203803.png)

用Burpsuite构造

```php
X-Forwarded-For:123.123.123.123
Referer:https://www.google.com
```

得到Flag：`cyberpeace{b2e0eea7b3e46ecab97c241980c852e3}`

## 010 webshell

![7dqwMl20200401204559](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/7dqwMl20200401204559.png)

根据提示然后得到我们可以得到这个一句话的密码是shell

使用蚁剑，右键单击空白处添加数据

![4j3UXr20200401204748](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/4j3UXr20200401204748.png)

输入地址和密码连接

![ATTEIT20200401204906](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/ATTEIT20200401204906.png)

右键文件管理，查看文件目录

![RAFjBw20200401205005](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/RAFjBw20200401205005.png)

发现flag.txt ，打开txt文件

![7uhxAo20200401205130](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/7uhxAo20200401205130.png)

得到Flag： `cyberpeace{9c298e551cd051ba2be17c1022b3c5fe}`

## 011 command_execution

![A0FOSs20200401205847](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/A0FOSs20200401205847.png)

观察题目要求，是ping功能，看看页面中的内容，尝试输入IP地址尝试一下

输入常见的本地地址`127.0.0.1`试试看，有回显，这时候看回显内容感觉有点像linux系统的回显，测试输入ls看看能不能列出内容，发现没有什么问题，可以断定是linux系统了，那就要用到命令连接符了

![TJuGQP20200401205937](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/TJuGQP20200401205937.png)

有回显，证明这个是可以运行的，那接着往下看看有没有关于flag这个文件，

输入命令`127.0.0.1 && find / -name flag.txt`，查找其中有没有flag.txt文件(注意空格

![nbMRNU20200401210027](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/nbMRNU20200401210027.png)

看到确实有个flag文件，就在这个home文件夹里，那我们使用cat命令来查看一下其中的内容，

输入命令`127.0.0.1 && cat /home/flag.txt`，得出答案

![wWQ0dy20200401210133](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/wWQ0dy20200401210133.png)

得到Flag：`cyberpeace{4f01cba3ce0dc9ead6ef996ce1628449}`

## 012 simple_js

打开该场景后发现是一个登录界面，随便输入一个密码，回显一个对话框就没了，习惯性首先查看源代码

![AY3Cel20200401210602](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/AY3Cel20200401210602.png)

![oW9ace20200401210442](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/oW9ace20200401210442.png)

源代码里果然有东西，看到一串比较显眼的数字，一下子想到了ASCII码，转换过来竟然是回显的内容，继续往下看发现了一串代码

![CfMz6A20200401210637](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/CfMz6A20200401210637.png)

使用python将先将16进制数输出

```python
data="\x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30"
print(data)
```

得到：`55,56,54,79,115,69,114,116,107,49,50`

再将数字（ascii码）转换为对应的字符

```python
a = [55,56,54,79,115,69,114,116,107,49,50]
c = ""
for i in a:
	b = chr(i)
	c = c+b
print(c)
```

得到字符串：786OsErtk12

规范flag格式，可得到Flag：`Cyberpeace{786OsErtk12}`



⚠️：更新于2020.06.29，如官方题目有更新，请及时联系我更新WP