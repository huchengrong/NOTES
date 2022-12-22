# 搜索危险函数

```bash
grep -R -e system -e exec -e passthru -e '`' -e popen -e proc_open *
```
