# 文件信息泄漏

### 图片

1. file查看文件类型
2. 具体分析
3. 用strings和binwalk看（一定要看）

```bash
exiftool for-007.jpg    好用
strings for-007.jpg     一般
binwalk --通用分析一下，可能存在不一样的信息
steghide extract -sf nsa.jpg   --可以拆解出图片信息
```

```bash
hexeditor tokyo.jpeg
头签名：（如果全图有这个头，那就把之前的删掉，如果没有就加一个，结尾是D9）
FF D8 FF E0
```

### 视频

```bash
python2 tcsteg2.py -p  mulder.fbi
再使用truecrypt分析
注意有可能会有密码，要回顾之前所得
```

### 视频文件爆破

```bash
truecrack -v -t 【文件】 -w 【密码本】
得到密码再用VeraCrypt打开
```

### 压缩包doc等文件

```bash
爆破zip
fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt backup 
或者
hash提取
zip2john safe.zip > pass
john pass
```
