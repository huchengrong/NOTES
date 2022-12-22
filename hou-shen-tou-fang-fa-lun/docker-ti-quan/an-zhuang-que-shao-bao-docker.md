# 安装缺少包（docker）

```bash
cat /etc/os-release 
得到
Debian 10 (buster)：
这个版本的安装版本如下，其他的版本可以自行研究
wget http://http.us.debian.org/debian/pool/main/libc/libcap2/libcap2-bin_2.25-2_amd64.deb
wget http://http.us.debian.org/debian/pool/main/libc/libcap2/libcap2_2.25-2_amd64.deb

而后安装依赖
dpkg -i libcap2_2.25-2_amd64.deb 
dpkg -i libcap2-bin_2.25-2_amd64.deb 、
```
