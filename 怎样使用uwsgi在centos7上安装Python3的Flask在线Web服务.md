## 怎样使用uwsgi在centos7上安装Python3的Flask在线Web服务

查看版本：

```shell
cat /etc/redhat-release
CentOS Linux release 7.7.1908 (Core)
```



### 1、添加一个用户

新增用户：

```shell
adduser antpython
```

修改密码：

```shell
passwd antpython
```

添加到sudo用户组：

```shell
gpasswd -a antpython wheel
```

切换到antpython用户：

```shell
sudo -iu antpython
```

注意：下方所有的命令，都是切换到了antpython用户进行的，所以很多都带上了sudo



### 2、初始化环境

初始化仓库：

```shell
sudo yum install epel-release
```

安装gcc和ngnix：

```shell
sudo yum install gcc nginx
```



### 3、安装anaconda

下载地址在：

```
https://www.anaconda.com/distribution/
```

下载Anaconda的安装文件：

```shell
wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
```

安装Anaconda：

```shell
sh Anaconda3-2019.10-Linux-x86_64.sh
```

路径选择的时候，不要改动，默认是：

```shell
/home/antpython/anaconda3
```



### 4、创建python虚拟环境

激活anaconda：

```shell
source anaconda3/bin/activate
```

安装virtualenv：

```shell
pip install virtualenv
```

创建目录：

```shell
mkdir ~/myproject
cd ~/myproject
```

创建虚拟环境目录：

```shell
virtualenv myprojectenv
```

激活新创建的虚拟环境：

```shell
source myprojectenv/bin/activate
```



### 5、初始化一个简单地flask应用

安装flask和uwsgi：

```shell
pip install uwsgi flask
```

创建一个flask文件：

```shell
vim ~/myproject/myproject.py
```



```python
# 把这段代码粘贴进去

from flask import Flask
application = Flask(__name__)

@application.route("/")
def hello():
    return "Hello There!"

if __name__ == "__main__":
    application.run(host='0.0.0.0')
```

回到命令行，启动测试flask服务：

```shell
python myproject.py
```

打开系统的5000端口号

```shell
sudo firewall-cmd --permanent --add-port=5000/tcp
sudo firewall-cmd --reload
```

在浏览器访问，即可打开网页，其中的xx.xx.xx.xx换成你的ip：

```
http://xx.xx.xx.xx:5000/
```



### 6、创建一个wsgi入口

```shell
vim ~/myproject/mywsgi.py
```



```python
# 粘贴代码如下： 
from myproject import application

if __name__ == "__main__":
    application.run()
```

使用这个命令测试下uwsgi

```shell
uwsgi --socket 0.0.0.0:5000 --protocol=http -w mywsgi
```

在浏览器访问，即可打开网页，其中的xx.xx.xx.xx换成你的ip：
[http://xx.xx.xx.xx:5000](http://xx.xx.xx.xx:5000/)

### 7、配置uwsgi的配置文件

编辑一个配置文件

```shell
vim /home/antpython/myproject/myproject.ini
```



```ini
[uwsgi]
module = mywsgi

master = true
processes = 5
threads = 100

http = 0.0.0.0:5000
virtualenv = /home/antpython/myproject/myprojectenv
die-on-term = true
```

回到命令行，通过以下命令启动一个uwsgi服务器：

```shell
uwsgi --ini myproject.ini
```



### 8、创建自启动Systemd配置

好处是：系统自己重启后，服务会自动启动

```shell
sudo vim /etc/systemd/system/myproject.service
```



```shell
# 输入下面的内容
[Unit]
Description=uWSGI instance to serve myproject
After=network.target

[Service]
User=antpython
Group=nginx
WorkingDirectory=/home/antpython/myproject
Environment="PATH=/home/antpython/myproject/myprojectenv/bin"
ExecStart=/home/antpython/myproject/myprojectenv/bin/uwsgi --ini myproject.ini

[Install]
WantedBy=multi-user.target
```

启动服务

```shell
sudo systemctl start myproject.service
```

开机自动启动服务

```shell
sudo systemctl enable myproject.service
```



### 9、参考资料：

- https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-centos-7
- https://www.kingname.info/2019/07/08/deploy-flask-uwsgi-without-nginx/

