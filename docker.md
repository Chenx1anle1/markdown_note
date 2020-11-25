![image-20200911093914204](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911093914204.png)

docker 虚拟机
E   远程仓库
A   镜像（安装虚拟机镜像文件）

B   容器（类比正在运行中的虚拟机）

C   tar 文件 load 虚拟机

D   dokerfile 简短的配置文件 通过指令 构建虚拟机

play with docker
添加实例

![image-20200911094229063](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911094229063.png)

1.获得镜像(镜像站)

```
docker 安装略
下载nginx镜像
docker pull nginx
同等于
docker pull nginx:latest	指定版本 默认不指定为最新版本
docker images 				查看镜像命令  



```

![image-20200911094531913](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911094531913.png)

```shell
通过run指令 将镜像运行为一个容器
docker run -d -p 80:80 nginx -d 后台运行（不阻塞shell） -p 映射内/外端口
通过172.18.0
docker ps 查看当前运行的容器列表
启动多个（端口更换）
docker run -d -p 81:80 nginx
nginx 可访问到nginx 初始页

通过 pull run 指令 将容器运行起来了
```

![image-20200911094859545](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911094859545.png)

```
使用ID修改容器
docker exec -it 92 bash 进入linux nginx容器中了
cd /usr/share/nginx/html/
修改文件
exit
```

![image-20200911100652904](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911100652904.png)

```
删除容器
docker rm -f 8b

docker commit 92 mi	指定镜像名字

 修改过的容器保存成镜像 再运行 可以保持变化
```

![image-20200911100917693](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911100917693.png)

dockerfile

![image-20200911101318188](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911101318188.png)

![image-20200911101204245](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911101204245.png)

```
指定 镜像 
并将当前目录下的文件保存到指定文件夹下

docker build -t m2 . 		.表示当前目录下  即使用当前目录下的dockerfile创建镜像m2

docker run -d -p 100:80 m2 
```

![image-20200911101546356](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911101546356.png)

tar

```
docker save m2 >1.tar

docker rmi m2  	将m2镜像删除
	容器基于镜像的无法删除镜像 即需要删除容器之后
```

![image-20200911101837239](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911101837239.png)

![image-20200911101849277](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911101849277.png)

![image-20200911101907981](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911101907981.png)

![image-20200911101923607](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911101923607.png)

```
docker run -d -p 88:80 --name mynginx（容器） -v `pwd`: /usr/share/nginx/html/ nginx：1.13（镜像）（注意版本 可以默认 也可以指定版本）
-v 文件映射

mysql data 文件映射到外部防止丢失等的 应用
```



搭建一个lnmp

通信方式等

![image-20200911102614383](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911102614383.png)

运行一个容器

![image-20200911102749819](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911102749819.png)

![image-20200911102832938](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911102832938.png)

```
docker exec -it mynginx bash	进入容器（虚拟机linux alpin）
```

ip查看 ifconfig

```
cat /etc/hosts
exit
```

![image-20200911103034668](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911103034668.png)

 运行一个alpine （5M最小linux 系统）普通容器 安装curl

![image-20200911103321546](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911103321546.png) 

```

clear
curl 172.27.0.2

```

![image-20200911103431467](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911103431467.png)

生产过程中如何进行通信

用alpine 访问 myng nginx 

```
docker ps
```

![image-20200911103501041](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911103501041.png)

```
docker run -dit --link myng：myng alpine it防止断掉 注意link
```

![image-20200911103913428](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911103913428.png)

```
sh 进入alpine容器
```

![image-20200911103923803](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911103923803.png)

```
--link 方式 将另一个容器映射到本容器
映射方式其实是 修改 hosts文件
cat /etc/hosts
```

![image-20200911104101599](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200911104101599.png)

```
exit
```

cat /flask/dockerfile

```
docker-compose

```

