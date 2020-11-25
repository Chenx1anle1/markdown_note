## 服务器搭建--Linux安装Nodejs

> 先去官网下载：https://nodejs.org/en/download/

![image-20201017093715628](C:%5Cworkshop%5C%E5%B7%A5%E4%BD%9C%E7%AC%94%E8%AE%B0-%E8%AE%B0%E5%BD%95%20markdown%20Typora%5Cimages%5Cimage-20201017093715628.png)

把压缩包上传到服务器的/usr/local/soft（博主习惯）文件夹下 解压文件：

```delphi
cd /usr/local/soft



tar -xvf node-v8.11.1-linux-x64.tar.xz
```

建立软连接，设置全局：

```delphi
ln -s /usr/local/soft/node-v8.11.1-linux-x64/bin/node /usr/local/bin/node



ln -s /usr/local/soft/node-v8.11.1-linux-x64/bin/npm /usr/local/bin/npm
```

使用node -v命令查看是否安装成功：

```delphi
[root@manmanda2018 soft]# node -v



v8.11.1
```

为了加速下载我们使用cnpm

安装cnpm

```delphi
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

建立软连接：

```delphi
ln -s /usr/local/soft/node-v8.11.1-linux-x64/bin/cnpm /usr/local/bin/cnp
```

安装express-generator脚手架(新版本须装)

```delphi
cnpm install -g express-generator
```

安装Express

```delphi
cnpm install -g express 
```

建立软链接

```delphi
ln -s /usr/local/soft/node-v8.11.1-linux-x64/bin/express /usr/local/bin/express
```

创建项目（先在根目录创建project文件夹）：

```delphi
cd /project
express app
```

进入app项目，安装相关依赖:

```delphi
cd /app
cnpm install
```

启动node进程：

```shell
npm start
```

访问http://127.0.0.1:3000

```
curl http://127.0.0.1:3000
```

![image-20201017093940366](C:%5Cworkshop%5C%E5%B7%A5%E4%BD%9C%E7%AC%94%E8%AE%B0-%E8%AE%B0%E5%BD%95%20markdown%20Typora%5Cimages%5Cimage-20201017093940366.png)

Express欢迎页面呈现

**测试是否安装完成**

输入

```bash
node -v
npm -v
```

**返回node和npm版本号 安装完成**

输入

```bash
node
```

**进入node命令行 按两次 ctrl + c 退出命令行**