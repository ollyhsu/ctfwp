# 攻防世界Crypto新手练习区Writeup

## 001 base64

![image-20200629152246029](/Users/kimix/Library/Application Support/typora-user-images/image-20200629152246029.png)

base64解密即可，直接上Python脚本

```python
import base64

a = open(r'crypto1.txt', 'r')
s = a.read()

print(base64.b64decode(s))
```

得到flag：`cyberpeace{Welcome_to_new_World!}`

## 002 Caesar

![pQIaZP](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/pQIaZP.png)

【原理】凯撒密码

【目的】掌握凯撒密码加密原理以及解码方式

【环境】Python

【工具】Python

【步骤】凯撒密码解密脚本

```python
#!/user/bin/env python
# -*-coding:utf-8 -*-

a = open(r'crypto2.txt', 'r')
ciphertext = a.read()
b = 'abcdefghijklmnopqrstuvwxyz'

for key in range(26):
    flag = ''
    for i in ciphertext:
        if i in b:
            num = b.find(i)
            num = num - key

            if num < 0:
                num = num + len(b)
            flag = flag + b[num]
        else:
            flag = flag + i
    print('key %s :%s' % (key, flag))
```

得到正确顺序的flag：`cyberpeace{you_have_learned_caesar_encryption}`

## 003 Morse

![LoFinJ](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/LoFinJ.png)



```pyhon
#!/user/bin/env python
# -*-coding:utf-8 -*-
a2mo_dict = {
    # 26 个英文字符
    'A': '.-', 'B': '-...', 'C': '-.-.',
    'D': '-..', 'E': '.', 'F': '..-.',
    'G': '--.', 'H': '....', 'I': '..',
    'J': '.---', 'K': '-.-', 'L': '.-..',
    'M': '--', 'N': '-.', 'O': '---',
    'P': '.--.', 'Q': '--.-', 'R': '.-.',
    'S': '...', 'T': '-', 'U': '..-',
    'V': '...-', 'W': '.--', 'X': '-..-',
    'Y': '-.--', 'Z': '--..',

    # 10 个数字
    '0': '-----', '1': '.----', '2': '..---',
    '3': '...--', '4': '....-', '5': '.....',
    '6': '-....', '7': '--...', '8': '---..',
    '9': '----.',

    # 16 个特殊字符
    ',': '--..--', '.': '.-.-.-', ':': '---...', ';': '-.-.-.',
    '?': '..--..', '=': '-...-', "'": '.----.', '/': '-..-.',
    '!': '-.-.--', '-': '-....-', '_': '..--.-', '(': '-.--.',
    ')': '-.--.-', '$': '...-..-', '&': '. . . .', '@': '.--.-.'
}

mo2a_dict = dict(zip(a2mo_dict.values(), a2mo_dict.keys()))

def mo2a(morse):
    morse_key = morse.strip().split(" ")
    plain_text = [mo2a_dict[key] for key in morse_key]
    plain_text = "".join(plain_text)
    return plain_text


a = open(r'crypto3.txt', 'r')
ciphertext = a.read()

ciphertext = ciphertext.replace('1', '-')
ciphertext = ciphertext.replace('0', '.')

FLAG = mo2a(ciphertext)
flag = FLAG.lower()
flag = 'cyberpeace{' + flag + '}'
print('flag is :', flag)
```

![6PNGlJ](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/6PNGlJ.png)

得到flag：`cyberpeace{morsecodeissointeresting}`

## 004 混合编码

![lcajcX](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/lcajcX.png)

密文采用Base64和Unicode混合加密方式

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-
import base64

a = open(r'crypto4.txt', 'r')
s = a.read()
b = len(s)

# base64解密
b = base64.b64decode(s).decode('ascii')
# 对解密后的字符串进行处理
b = b.strip('&#;')
c = []
c = b.split(';&#')
# unicode解密
d = ''
for i in c:
    d += chr(int(i))
# base64再次解密
e = base64.b64decode(d).decode('ascii')
# 对字符进行处理
e = e.strip('/')
f = []
f = e.split('/')
# 转化为ascii码
flag = ''
for i in f:
    flag += chr(int(i))
flag = 'cyberpeace{'+flag+'}'
print('flag is :', flag)
```

脚本运行得到Flag：`cyberpeace{welcometoattackanddefenceworld}`

## 005 幂数加密

![QnQiUp](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/QnQiUp.png)

```python
a = open(r'crypto5.txt', 'r')
ciphertext = a.read()

s = ciphertext.split('0')

flag = ''
for i in range(len(s)):
    list = []
    for j in s[i]:
        list.append(j)
    b = 0
    for k in list:
        b += int(k)
    # 字母ascii值与大写字母顺序相差为64
    flag += chr(b + 64)

flag = 'cyberpeace{' + flag + '}'
print('flag is :', flag)
```

打开文件看到一堆数字，观察数字是由0,1,2,4,8这几个数字组成的，不难发现都是2的指数幂，然后百度了一下，发现有一种二进制幂数加密。

简单的来说，就是所有的数都能由0,1,2,4,8这几个数字相加得到，由此我们可以将字母表的字母按照顺序变换成相应的数字，然后分成若干个0,1,2,4,8相加，从而达到加密的方式。

![KcWYMU](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/29/KcWYMU.png)

提交flag：`cyberpeace{WELLDONE}`

## 006 Railfence

![bJHFmr](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/30/bJHFmr.png)

【原理】栅栏密码

【目的】掌握栅栏密码编码以及解码方式

【环境】Windows

【工具】在线解密

【步骤】

根据题目这题考查的是栅栏密码，key为5，但是常见的栅栏密码貌似解不开，于是应该想到W型栅栏密码

使用在线加解密网站：http://www.atoolbox.net/Tool.php?Id=777

key为5，在线解密即可得到flag

![TaEuwn](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/30/TaEuwn.png)

提交flag：`cyberpeace{railfence_cipher_gogogo}`

## 007 easy_RSA

![I6is9r](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/06/30/I6is9r.png)

公钥密码算法（非堆成密钥算法）：产生一对可以互逆变换的密钥Kd与Ke，但是即使知道Kd，还是无法得知Ke，这样就可将Kd公开，但只有接收方知道Ke。在此情况下，任何人均可利用Kd加密，而只有知道Ke的接收方才能解密；或是只有接收方一人才能加密（加密与解密其实都是一种动作），任何人均能解密。

**简单地概述一下𝑅𝑆𝐴算法加密/解密的过程：**

N：公钥1	d：公钥2 	e：私钥

A： 密文	  B：明文    φ()：欧拉函数

- 公钥在同一加密规则下对于所有人来说都是已知的，`加密只需公钥`

- 首先约定私钥 𝑒e需满足：`1<𝑒<φ(𝑁)` 且`𝑔𝑐𝑑(𝑒,𝑁)=1`（互质，否则无解）

- 公钥 𝑑 由 `(d*e)≡1(mod N)` ① 计算出，此时称 𝑑是 𝑒的模反元素
- 为了增加破解（分解因数）的难度，𝑁 一般为两个大质数的乘积（`即 𝑝和 𝑞`）

**加密公式：** 
$$
A^d \equiv B(mod N) \quad 或 \quad A^d(mod N)=B
$$
**解密公式：**
$$
B^e \equiv A(mod N) \quad 或 \quad B^e(mod N)=A
$$
**数字签名：** 
$$
A^e \equiv B(mod N) \quad 或 \quad A^e(mod N)=B
$$
 **验证签名：** 
$$
B^d \equiv A(mod N) \quad 或 \quad  B^d(mod N)=A
$$
我们知道`当 𝑝和𝑞都为质数 `时，`φ(𝑁)=φ(𝑝∗𝑞)=(𝑝−1)∗(𝑞−1)`

故 ① 式变为：`𝑑∗𝑒%((𝑝−1)∗(𝑞−1))=1`，即 `𝑑∗𝑒∗𝑥−(𝑝−1)∗(𝑞−1)∗𝑦=1 其中：𝑥,𝑦∈𝑁`

easy_RSA 这道题就是模拟了计算公钥的过程，我们可以使用扩展欧几里得算法解决。

Python代码如下：

```python
import gmpy2

p = 473398607161
q = 4511491
e = 17

s = (p - 1) * (q - 1)
d = gmpy2.invert(e, s)  # 求逆元d，d*e ≡ 1 mod s (或 d*e (mod s) =1)
print('result is :', d)
```

然后提交flag：`cyberpeace{125631357777427553}`

## 008 不仅仅是Morse

![ppxz91](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/07/01/ppxz91.png)

先在线进行摩尔斯密码的解密再进行培根密码的解密即可得到flag

下面给出python代码：

```python
# Morse解密脚本
a2mo_dict = {
    # 26 个英文字符
    'A': '.-', 'B': '-...', 'C': '-.-.',
    'D': '-..', 'E': '.', 'F': '..-.',
    'G': '--.', 'H': '....', 'I': '..',
    'J': '.---', 'K': '-.-', 'L': '.-..',
    'M': '--', 'N': '-.', 'O': '---',
    'P': '.--.', 'Q': '--.-', 'R': '.-.',
    'S': '...', 'T': '-', 'U': '..-',
    'V': '...-', 'W': '.--', 'X': '-..-',
    'Y': '-.--', 'Z': '--..',

    # 10 个数字
    '0': '-----', '1': '.----', '2': '..---',
    '3': '...--', '4': '....-', '5': '.....',
    '6': '-....', '7': '--...', '8': '---..',
    '9': '----.',

    # 16 个特殊字符
    ',': '--..--', '.': '.-.-.-', ':': '---...', ';': '-.-.-.',
    '?': '..--..', '=': '-...-', "'": '.----.', '/': '-..-.',
    '!': '-.-.--', '-': '-....-', '_': '..--.-', '(': '-.--.',
    ')': '-.--.-', '$': '...-..-', '&': '. . . .', '@': '.--.-.'
}

mo2a_dict = dict(zip(a2mo_dict.values(), a2mo_dict.keys()))


def mo2a(morse):
    morse_key = morse.strip().split(" ")
    plain_text = [mo2a_dict[key] for key in morse_key]
    plain_text = "".join(plain_text)
    return plain_text


a = open(r'crypto8.txt', 'r')
ciphertext = a.read()

ciphertext = ciphertext.replace('/', ' ')

FLAG = mo2a(ciphertext)
print(FLAG)

# 培根解密脚本
import re

# 培根密文转化为指定格式
s = 'AAAAABAABBBAABBAAAAAAAABAABABAAAAAAABBABAAABBAAABBAABAAAABABAABAAABBABAAABAAABAABABBAABBBABAAABABABBAAABBABAAABAABAABAAAABBABBAABBAABAABAAABAABAABAABABAABBABAAAABBABAABBA '
a = s.lower()

# 字典
CODE_TABLE = {
    'a': 'aaaaa', 'b': 'aaaab', 'c': 'aaaba', 'd': 'aaabb', 'e': 'aabaa', 'f': 'aabab', 'g': 'aabba',
    'h': 'aabbb', 'i': 'abaaa', 'j': 'abaab', 'k': 'ababa', 'l': 'ababb', 'm': 'abbaa', 'n': 'abbab',
    'o': 'abbba', 'p': 'abbbb', 'q': 'baaaa', 'r': 'baaab', 's': 'baaba', 't': 'baabb', 'u': 'babaa',
    'v': 'babab', 'w': 'babba', 'x': 'babbb', 'y': 'bbaaa', 'z': 'bbaab'
}


# 5个一组进行切割并解密
def peigendecode(peigen):
    msg = ''
    codes = re.findall(r'.{5}', a)
    for code in codes:
        if code == '':
            msg += ' '
        else:
            UNCODE = dict(map(lambda t: (t[1], t[0]), CODE_TABLE.items()))
            msg += UNCODE[code]
    return msg


flag = peigendecode(a)
flag = 'cyberpeace{' + flag + '}'
print('flag is ', flag)
```

得到flag：`cyberpeace{attackanddefenceworldisinteresting}`

## 009 easychallenge

![rtlYDm](https://cdn.jsdelivr.net/gh/kimix102/PicBed@master/2020/07/01/rtlYDm.png)

**解释型语言和编译型语言的区别**
计算机是不能够识别高级语言的，所以当运行一个高级语言程序时，就需要一个“翻译机”来从事把高级语言转变成计算机能读懂的机器语言的过程。这个过程分成两类，第一种是编译，第二种是解释。
（1）编译型语言：在程序执行之前，先会通过编译器对程序执行一个编译的过程，把程序转变成机器语言。运行时就不需要翻译，而直接执行就可以了。最典型的例子就是C语言。
（2）解释型语言：没有编译的过程，而是在程序运行时，通过解释器对程序逐行解释，然后直接运行，最典型的例子是Ruby。
（3）编译型语言与解释型语言的优缺点：编译型语言在程序运行之前就已经对程序做出了“翻译”，所以在运行时就少掉了“翻译”的过程，所以效率比较高。但是我们也不能一概而论。
（4）先编译后解释的语言：Java首先是通过编译器编译成字节码文件，然后在运行时通过解释器给解释成机器文件。Java等基于虚拟机的语言的存在，我们又不能把语言纯粹地分成解释型和编译型这两种。Python也是一门基于虚拟机的语言。当我们在命令行中输入python hello.py时，其实是激活了Python的“解释器”，告诉“解释器”：你要开始工作了。可是在“解释”之前，其实执行的第一项工作和Java一样，是编译。

**Python的运行过程**
关于PyCodeObject和pyc文件：在硬盘上看到的pyc文件，其实PyCodeObject才是Python编译器真正编译成的结果。当python程序运行时，编译的结果是保存在位于内存中的PyCodeObject中，当Python程序运行结束时，Python解释器则将PyCodeObject写回到pyc文件中。当python程序第二次运行时，首先程序会在硬盘中寻找pyc文件，如果找到，则直接载入，否则就重复上面的过程。所以，我们可以说pyc文件其实是PyCodeObject的一种持久化保存方式。

对于py文件，可以执行下面命令来生成pyc文件：`python -m foo.py`
原来Python的程序中，是把原始程序代码放在.py文件里，而Python会在执行.py文件的时候。将.py形式的程序编译成中间式文件（byte-compiled）的.pyc文件，这么做的目的就是为了加快下次执行文件的速度。所以，在我们运行python文件的时候，就会自动首先查看是否具有.pyc文件，如果有的话，而且.py文件的修改时间和.pyc的修改时间一样，就会读取.pyc文件，否则，Python就会读原来的.py文件。
其实并不是所有的.py文件在与运行的时候都会产生.pyc文件，只有在import相应的.py文件的时候，才会生成相应的.pyc文件。

给的文件为.pyc文件，先进行反编译为.py文件，再写解密脚本

反编译.pyc文件：

- 反编译可以使用uncompyle6或者在线反编译pyc
- 安装uncompyle6 ：`pip install uncompyle6`
- 反编译命令 `uncompyle6 crypto.pyc`

反编译结果：

```python
import base64

def encode1(ans):
    s = ''
    for i in ans:
        x = ord(i) ^ 36
        x = x + 25
        s += chr(x)

    return s


def encode2(ans):
    s = ''
    for i in ans:
        x = ord(i) + 36
        x = x ^ 36
        s += chr(x)

    return s


def encode3(ans):
    return base64.b32encode(ans)


flag = ' '
print 'Please Input your flag:'
flag = raw_input()
final = 'UC7KOWVXWVNKNIC2XCXKHKK2W5NLBKNOUOSK3LNNVWW3E==='
if encode3(encode2(encode1(flag))) == final:
    print 'correct'
else:
    print 'wrong'
```

**解密脚本**

```python
#!/usr/bin/env python
# encoding: utf-8

import base64
'''
a = 'UC7KOWVXWVNKNIC2XCXKHKK2W5NLBKNOUOSK3LNNVWW3E==='
b = base64.b32decode(a)
'''
# 先将字符串base32解码出来，然后将其变为字符串再进行ord等操作。
b = "\xa0\xbe\xa7Z\xb7\xb5Z\xa6\xa0Z\xb8\xae\xa3\xa9Z\xb7Z\xb0\xa9\xae\xa3\xa4\xad\xad\xad\xad\xad\xb2"
s = ''
for i in b:
    s += chr((ord(i) ^ 36) - 36)
l = ''
for i in s:
    l += chr((ord(i) - 25) ^ 36)
print ('flag is ',l)
```

解密得到flag：`cyberpeace{interestinghhhhh}`

## 010



## 011



## 012 easy_ECC

