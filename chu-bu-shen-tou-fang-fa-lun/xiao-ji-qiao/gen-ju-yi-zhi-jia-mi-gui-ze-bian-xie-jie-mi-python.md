# 根据已知加密规则编写解密python

实例如下

```clike
1. 加密规则
array2[i] = (array[i] ^ Protected.key[i % Protected.key.Length] ^ 223);
2. 加密密钥
private static byte[] key = Encoding.ASCII.GetBytes("armando");
3. 初始的密码
"0Nv32PTwgYjzg9/8j5TbmvPd3e7WhtWWyuPsyO76/Y+U193E";
```

解密脚本

```clike
import base64
enc_password = "0Nv32PTwgYjzg9/8j5TbmvPd3e7WhtWWyuPsyO76/Y+U193E"
key = "armando".encode("UTF-8") 
array = base64.b64decode(enc_password)
array2 = ""
for i in range(len(array)):
    array2 += chr(array[i] ^ key[i % len(key)] ^ 223) 
print(array2)
```
