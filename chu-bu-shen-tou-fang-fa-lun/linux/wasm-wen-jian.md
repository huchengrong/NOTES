# wasm文件

1. 常见于修改返回值

```bash
proxychains4 -f /etc/proxychains4.conf git clone --recursive https://github.com/WebAssembly/wabt
cd wabt/
apt install cmake
make
wasm-decompile main.wasm 
到这里就生成好了
wasm2wat main.wasm -o main.wat
而后修改wat文件，返回值是const后的参数
wat2wasm main.wat -o main.wasm
```
