# 公司 · Python · 后端工作手册

##### **by.** <u>chenx1anle1</u>

###### ***2020年7月14日***

### 一 **订单系统**

### **二 分发系统**

```shell
#linux 部署
#部署 docker
#服务器管理 可能用到的命令
sudo python3 /opt/miner/manager/monitor-script/monitor_produce_https.py

cd ~/movie

uwsgi --ini uwsgi8000.ini

sudo systemctl restart nginx
```

###### 矿机

```shell
#$ ssh <username>@<server-ip-address>

ssh cat@39.130.180.229-254

#password

JmkJ_2020

```



###### Redis 上要注意分发系统和订单系统的数据库 都是2 可能冲突

##### 线上系统

```
https://ipfscnpool.cn/
http://ipfscnpool.cn/
https://os.ipfscnpool.cn/
https://mobile.ipfscnpool.cn/
```



###### 使用短信验证平台

​		通过对接第三方短信平台（如 螺丝帽）（Luosimao）实现了短信验证码登录以及重要消息提醒的短信服务，通过接入第三方云存储服务（七牛云）实现了小纸条模块用户上传图片的存储、水印以及缩略图等功能，使用Celery+Redis实现了三方平台接入的异步化处理（避免因三方平台问题造成的请求阻塞

#### 阿里云账号密码等问刁总

### **分发系统**

1. ###### 提现

2. ###### 结算

3. ###### 分发

###### linux环境变量 可以用于记录 计算用户收益的固定参数