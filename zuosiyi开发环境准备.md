#### 一、官网下载：

##### 1、Nodejs官网下载 	12.19.0	https://nodejs.org/en/download/

选择wendows installer下载并安装。

![image-20201021162559190](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201021162559190.png)

##### 2、安装nodejs附带安装：

###### Npm             					                                     6.14.8  

###### Npminstall          			                                    3.27.0 

##### 3、Visual Studio Code官网下载 1.50.1  https://nodejs.org/en/download/

 选择windows下载并安装。

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml10412\wps2.jpg)

 

#### 二、命令行安装：

##### 1、cnpm （淘宝镜像）                                                      		  6.1.1  

###### $npm install -g cnpm --registry-https://registry.npm.taobao

##### 2、Supervisor （自启动工具）           	                                   0.12.0

###### $npm install -g supervisor 

*$supervisor 代替 $node 运行程序时可能会出现无限循环，可能与其他包冲突了。

#### 三、Vscode扩展安装：

##### 1、Chinese (Simplified) Language Pack for Visua  1.50.2（中文汉化包）

<img src="file:///C:\Users\Administrator\AppData\Roaming\Tencent\Users\1975219352\QQ\WinTemp\RichOle\_1%%VZWBP0PZ[ASZ]6Q2WU5.png" alt="img"  />

##### 2、node-snippets （提示工具）                                1.2.2

![image-20201021162716220](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201021162716220.png)

##### 3、Gitee（gitee平台操作仓库）                                 0.0.6  

![image-20201021162800478](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201021162800478.png)

##### 4、码云（Gitee）常用功能                                           0.1.4

![img](file:///C:\Users\Administrator\AppData\Roaming\Tencent\Users\1975219352\QQ\WinTemp\RichOle\M(}ND@`)H9B`DR16J{TVVLM.png)

##### 5、GitLens — Git supercharged                              10.2.2

![img](file:///C:\Users\Administrator\AppData\Roaming\Tencent\Users\1975219352\QQ\WinTemp\RichOle\O234MHIWHZSC[@YKW$}{8MD.png)

##### 6、Git History                                                               0.6.12

![image-20201021163128808](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201021163128808.png)

#### 四、egg框架安装：

##### 脚手架生成egg项目：

```
$ npm i egg-init -g
$ mkdir egg-example && cd egg-example
$ npm init egg --type=simple
$ npm i
```

##### 运行egg：

```
$ npm run dev
$ open http://localhost:7001
```