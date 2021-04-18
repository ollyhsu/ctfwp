# 攻防世界MISC新手练习区Writeup 

![image-20200628190929504](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/image-20200628190929504.png)

## 001 this_is_flag

![FnJuyE](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/FnJuyE.png)

【步骤】题目描述就是flag。

`flag{th1s_!s_a_d4m0_4la9}`

## 002 pdf

【目标】简单密码学

【环境】windows

【工具】PDF编辑器

【分析过程】

- 打开pdf，猜测flag在图片底下，可以wps等工具编辑PDF，将图片删除或移开后发现flag

- ![RlsLjN](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/RlsLjN.png)
- 得到flag：`flag{security_through_obscurity}`
- 此处附上在线转换地址：http://app.xunjiepdf.com/pdf2word

## 003 如来十三掌

【目标】简单密码学

【环境】windows

【工具】rot-13

【分析过程】

1. 打开附件

![34kQWk](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/34kQWk.png)

2.与佛论禅编码解码:http://www.keyfc.net/bbs/tools/tudoucode.aspx 

![image-20200628220533426](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/image-20200628220533426.png)

得到：`MzkuM3gvMUAwnzuvn3cgozMlMTuvqzAenJchMUAeqzWenzEmLJW9`

3.Rot13密码解码：https://www.jisuan.mobi/puzzm6z1B1HH6yXW.html

![M5015d](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/M5015d.png)

得到：`ZmxhZ3tiZHNjamhia3ptbmZyZGhidmNraWpuZHNrdmJramRzYWJ9`

4.Base64解码：http://ctf.ssleye.com/base64.html

![n8uhQ5](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/n8uhQ5.png)

得到flag：`flag{bdscjhbkzmnfrdhbvckijndskvbkjdsab}`

## 004 give_you_flag

【目标】简单密码学

【环境】windows

【工具】stegsolve

【分析过程】

1、下载附件，打开gif图会看到小龙人数完钞票会展示二维码，使用stegsolve等工具查看帧数得到二维码。

![BDelFH](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/BDelFH.png)

二维码缺少三个小方块，而这些小方块被称为定位图案，用于标记二维码矩形的大小，用三个定位图案可以标识并确定一个二维码矩形的位置和方向。

2、使用工具ps将二维码修复完全便可获得完整二维码，扫描获得flag。

![2](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/2.png)

得到flag：`flag{e7d478cf6b915f50ab1277f78502a2c5}`

## 005 SimpleRAR

![Eenvqd](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/Eenvqd.png)

1.将压缩包直接解压，发现压缩包损坏，但得到了一个flag.txt

![v81IvN](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/v81IvN.png)

2.根据提示flag不在这，那应该在剩余的文件中，将压缩包用winHex打开发现应该有png文件。

![TIJg7w](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/TIJg7w.png)

3.根据flag.txt的内容，补齐图片格式将A8 3C 7A改为A8 3C 74后保存，

![KXpaFO](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/KXpaFO.png)

4.再次解压得到一个空白图片，放在winhex下，发现是一个.gif图片，将图片后缀修改为.gif

![2Q2STV](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/2Q2STV.png)

5.用PhotoShop打开，发现有两个空白的图层

![tgpf9s](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/tgpf9s.png)

6.将两个图层分别提取出来，用StegSolve打开，不断点击箭头直到显示出二维码

![ibgD06](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/ibgD06.png)

7.使用stegsolve帧功能模块，得到两张不同的帧图片，调节颜色，得到两张残缺的二维码图片，合并补齐后，扫一扫即可。

![4lA1tr](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/4lA1tr.png)

8.然后扫描就看到flag啦:	`flag{yanji4n_bu_we1shi}`

## 006 坚持60s

下载发现是一个.jar的游戏，使用java反编译工具，查看源码，得到flag

![QTuVfq](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/28/QTuVfq.png)

得到flag：`flag{RGFqaURhbGlfSmlud2FuQ2hpamk=}` 提交了一下发现不对，仔细一看原来里面还有个base64加密，解密后再提交就可以了，最后flag结果：`flag{DajiDali_JinwanChiji}`

## 007 gif

【目标】简单密码学

【环境】windows

【工具】转换二进制为字符串工具

【分析过程】

打开文件出现多个黑白，让人联想到二进制，白色图片代表0，黑色图片代表1。

01100110前八位二进制换算后为 f 证明思路正确。

于是我们直接上python脚本：

```python
from PIL import Image
result = ""

for num,i in enumerate(range(104)):
	img = Image.open(f"{i}.jpg")
	im = img.convert("RGB")
	r,g,b = im.getpixel((1,1))
	if r != 255:
		result += "1"
	else:
		result += "0"

for i in range(0,len(result),8):
	byte = result[i:i+8]
	print(chr(int(byte,2)),end="")
print("\n")
```

![C1MS0h](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/C1MS0h.png)

得到flag：`flag{FuN_giF}`

## 008 掀桌子

![YF6NK0](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/YF6NK0.png)

【目标】简单密码学

【环境】windows

【工具】python

【分析过程】

解密方法，两个一位，16进制转10进制，然后减去128再转成字符即可：

```python
string = "c8e9aca0c6f2e5f3e8c4efe7a1a0d4e8e5a0e6ece1e7a0e9f3baa0e8eafae3f9e4eafae2eae4e3eaebfaebe3f5e7e9f3e4e3e8eaf9eaf3e2e4e6f2"
flag = ''
for i in range(0,len(string), 2):
    s = "0x" + string[i] + string[i+1]
    flag += chr(int(s, 16) - 128)
print(flag)
```

得到flag：`flag{hjzcydjzbjdcjkzkcugisdchjyjsbdfr}`

## 009 base64stego

【目标】base64 隐写

【环境】python

【工具】python

【分析过程】

无法直接解压压缩包，将其放在winhex下，查找查找`504B`标志位，发现是一个ZIP伪加密,将第二个504B后的0900改为0000

![4STOhT](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/4STOhT.png)

解压得到一个内容全是base64编码的文件

![dFLbSu](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/dFLbSu.png)

发现是base64文件隐写，python2环境下直接利用脚本即可解出flag.

```python
# -*- coding: cp936 -*-
b64chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
with open('stego.txt', 'rb') as f:
    bin_str = ''
    for line in f.readlines():
        stegb64 = ''.join(line.split())
        rowb64 =  ''.join(stegb64.decode('base64').encode('base64').split())
        offset = abs(b64chars.index(stegb64.replace('=','')[-1])-b64chars.index(rowb64.replace('=','')[-1]))
        equalnum = stegb64.count('=') #no equalnum no offset
        if equalnum:
            bin_str += bin(offset)[2:].zfill(equalnum * 2)
        print ''.join([chr(int(bin_str[i:i + 8], 2)) for i in xrange(0, len(bin_str), 8)]) 
```

运行的结果：

![cj0iaC](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/cj0iaC.png)

提交flag：`flag{Base_sixty_four_point_five}`

## 010 ext3

![V2NNm9](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/V2NNm9.png)

方法一：

下载附件，放入到Hex Fiend看看，找到flag.txt

![he4Xzw](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/he4Xzw.png)

尝试将目标文件后缀改为zip，进行解压，从而得到文件中的flag.txt文件

![v91VJP](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/v91VJP.png)

发现flag.txt中base64加密的数据`ZmxhZ3tzYWpiY2lienNrampjbmJoc2J2Y2pianN6Y3N6Ymt6an0=`

![Kzn2by](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/Kzn2by.png)

解密后得到flag：`flag{sajbcibzskjjcnbhsbvcjbjszcszbkzj}`

方法二：

1.可以先用file查看一下文件信息，似乎没什么东西

2.使用strings命令`strings linux|grep flag`，查看指定文件下有没有flag这样的字符串

![BYzm44](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/BYzm44.png)

发现在07avZhikgKgbF目录下有flag.txt文件

3.root模式下使用`mount f1fc23f5c743425d9e0073887c846d23 /mnt`命令将linux光盘挂载在mnt目录下，切换到mnt目录，使用`cat O7avZhikgKgbF/flag.txt`命令即可对flag内容进行读取

![xbid79](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/xbid79.png)

发现是一个base64编码，解密后得到flag.

flag：`flag{sajbcibzskjjcnbhsbvcjbjszcszbkzj}`

## 011 stegano

1.文件下载是一个pdf，使用pdfinfo查看信息，如下所示，Keywords中有一串base64码，解密后发现不是flag：

![DVlanI](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/DVlanI.png)

2.打开pdf后直接全选粘贴放在sublime里面，发现有一串的AB，考虑摩斯密码，将A替换为.，B替换为-，再解码即可得到flag

![M2sgdB](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/M2sgdB.png)

3.利用python脚本

```python
s = "BABA BBB BA BBA ABA AB B AAB ABAA AB B AA BBB BA AAA BBAABB AABA ABAA AB BBA BBBAAA ABBBB BA AAAB " \
    "ABBBB AAAAA ABBBB BAAA ABAA AAABB BB AAABB AAAAA AAAAA AAAAB BBA AAABB"
mose = ''
for c in s:
    if c == 'A':
        c = '.'

    if c == 'B':
        c = '-'
        
    mose += c

print(mose)
```

4.得到摩尔斯电码：`-.-. --- -. --. .-. .- - ..- .-.. .- - .. --- -. ... --..-- ..-. .-.. .- --. ---... .---- -. ...- .---- ..... .---- -... .-.. ...-- -- ...-- ..... ..... ....- --. ...--`

5.进行解码，得到：`1nv151bl3m3554g3`

![image-20200629121322867](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-20200629121322867.png)

6.根据题目要求是小写，提交flag：`flag{1nv151bl3m3554g3}`

## 012 功夫再高也怕菜刀

1.使用binwalk 查看该文件，可以看到里面有一个压缩包。

![YljxhC](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/YljxhC.png)

2.用foremost工具分离该文件,在输出结果中分离出一个压缩包,里面有一个flag.txt文件

3.打开wireshark分析数据包，`分组字节流`搜索`字符串flag.txt`，发现6666.jpg

![6ZVD8P](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/6ZVD8P.png)

4.追踪TCP流，找到jpg文件的文件头(FFD8)和文件尾(FFD9)并复制

![image-20200629123538298](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-20200629123538298.png)

![image-20200629123327470](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-20200629123327470.png)

5.用Hex Fiend新建文件，将复制内容粘贴为Ascll Hex 格式并保存，保存为jpg格式，可以得到图片，

![image-20200629123556077](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-20200629123556077.png)

6.得到压缩包解压密码：`Th1s_1s_p4sswd_!!!`，打开flag.txt文件

![image-20200629124017386](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/image-20200629124017386.png)

7.得到flag：`flag{3OpWdJ-JP6FzK-koCMAK-VkfWBq-75Un2z}`



⚠️：最后更新于2020年6月29日