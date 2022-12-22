# 流量包

1. 分析方法

```bash
Binwalk --通用分析一下
tcpflow ----分离流量包

1.TCP流
tcp.stream eq 1
tcp.stream eq 2

2.如果流量包内嵌有其他文件
可以用tree分析

3.抽离文件（适用于包含了图片啊，文本的情况）
foremost 【文件】
```
