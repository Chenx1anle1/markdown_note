Flask在VSCODE下基本开发环境配置



Tags：[Flask](https://www.cppentry.com/do/search.php?type=keyword&keyword=Flask) [VSCODE](https://www.cppentry.com/do/search.php?type=keyword&keyword=VSCODE) [基本](https://www.cppentry.com/do/search.php?type=keyword&keyword=%BB%F9%B1%BE) [开发](https://www.cppentry.com/do/search.php?type=keyword&keyword=%BF%AA%B7%A2) [环境](https://www.cppentry.com/do/search.php?type=keyword&keyword=%BB%B7%BE%B3) [配置]

####  1.创建环境

```
cd /project/path

python3 -m venv venv
```

第一个VENV是命令，第二个是文件夹名

如果环境不要了，一般做法是直接整个（VENV）文件夹删掉

环境修改下面会说

#### 2.激活环境

`. venv/bin/activate `

 venv是1中创建的文件夹，这么写是接1,即认为你当前路徑

在VENV同级路徑执行过1后，会在VENS下创建一系列文件，其中2中所用的是激活脚本

#### 3.修改pip镜像为国内源

```
mkdir ~/.pip
```

```
vim ~/.pip/pip.conf
```

```
[global]
```

```
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

清华源，会比阿里的源更新的更快一些

修改后，PIP下载包的速度会提高很多，大部分都不会等太久

#### 4.安装项目依赖包

```
pip install -r requirement.txt
```

requirement.txt一般是大家的约定文件名

里面存放项目依赖等pip包，因为源或者其他环境因素可能会有安装失败的情况

最终结果以 pip list 返回结果为准

#### 5.VS code 中Debug Flask程序配置 修改`.vscode`中的`launch.json`为如下内容

```
{
    "name": "Python: Flask",
    "type": "python",
    "request": "launch",
    "stopOnEntry": false,
    "pythonPath": "${config:python.pythonPath}",
    "program": "${workspaceRoot}/venv/bin/flask",
    "env": {
        "FLASK_APP": "${workspaceRoot}/app.py"
    },
    "args": [
        "run",
        "--no-debugger",
        "--no-reload"
    ],
    "debugOptions": [
        "WaitOnAbnormalExit",
        "WaitOnNormalExit",
        "RedirectOutput"
    ]
}
```

截至发博客时间vs插件自带的

配置是有问题的修改后可以使用断点调试，变量观察等IDE特性

#### 6.解决 `E1101:Instance of 'SQLAlchemy' has no 'Table' member` 误报问题

```
pip install pylint-flask 
```

然后在 VS code中修改setting.json

```
"python.linting.pylintArgs": ["--load-plugins", pylint_flask"]
```


​	目前python等linting插件对SQLAlchemy支持是有问题的，会有误报但是用6所用方法修改之后，在跳转的时候有时还会有问题

#### 7.unittest在VS code的配置

```
"python.unitTest.unittestArgs": [    "-v",    "-s",    ".",   "-p",   "test*.py"   ],  "python.unitTest.pyTestEnabled": false,  "python.unitTest.nosetestsEnabled": false,  "python.unitTest.unittestEnabled": true *
```

*unittest默认的discover是test*.py，在vscoder中，三个用一个，必须禁用另外两个

```
[1,2,4] http://flask.pocoo.org/docs/1.0/installation/ 

[3] http://www.cnblogs.com/biglittleant/p/6944180.html 

[5] https://donjayamanne.github.io/pythonVSCodeDocs/docs/debugging_debugging-flask/ , https://www.jianshu.com/p/0f9fd8823d90

[6] https://stackoverflow.com/questions/28193025/pylint-cant-find-sqlalchemy-query-member
```

