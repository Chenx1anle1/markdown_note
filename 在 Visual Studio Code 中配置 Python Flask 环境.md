# 在 Visual Studio Code 中配置 Python Flask 环境



# 在 Visual Studio Code 中配置 Python Flask 环境

> 本文由 *赤石俊哉* 原创编写，您可以在学习交流用途以内自由使用文章。
> 但是禁止抄袭文章，转载时，请注明来源地址，谢谢。
> 最后更新时间： 2017年11月24日 17:53:15
>
> 更多文章可以参见 [小赤石的Code Space](javascript:void())

- [0. 准备阶段](javascript:void())
- [1. 在 vscode 中安装 python 语言支持](javascript:void())
- [2. 使用 pip 安装 virtualenv、pylint、yapf](javascript:void())
  - [virtualenv](javascript:void())
  - [pylint](javascript:void())
  - [yapf](javascript:void())
  - [安装过程](javascript:void())
  - [安装中可能出现的问题](javascript:void())
    - [UnicodeEncodeError 'utf-8' codec can't encode character...](javascript:void())
- [3. 修改 vscode 中的设置](javascript:void())
- [4. 使用 virtualenv 创建工程目录](javascript:void())
  - [创建文件夹并配置虚拟环境](javascript:void())
  - [往虚拟环境中安装包](javascript:void())
- [5. 修改 launch.json](javascript:void())
- [6. 创建测试代码并运行测试](javascript:void())

## 0. 准备阶段

本文默认您已经完成了以下工作的情况：

```
1. 安装完成了 Visual Studio Code。
2. 安装完成了 Python 3.6.3 并且将 Python 添加到系统变量 PATH 中。
```

## 1. 在 vscode 中安装 python 语言支持

运行 vscode，按下 `Ctrl` + `P`，会打开一个输入框，输入 `ext install python`，就会进入扩展商店，搜索 `python`。
我们需要的是发行者为 `Microsoft` 的那一个名为 `Python` 的扩展。点击 `安装` 按钮，安装完成之后，点击 `重新加载`。

## 2. 使用 pip 安装 virtualenv、pylint、yapf

下面是各个包的简单说明，如果您足够了解的话，可以直接跳转到 `安装过程` 小节。

### virtualenv

> 摘自：[廖雪峰的官方网站 - virtualenv](javascript:void())
>
> 在开发 Python 应用程序的时候，系统安装的 Python3 只有一个版本：3.4。所有第三方的包都会被 `pip` 安装到Python3的 `site-packages` 目录下。
> 如果我们要同时开发多个应用程序，那这些应用程序都会共用一个 Python，就是安装在系统的 Python 3。
> 如果应用 A 需要 jinja 2.7，而应用 B 需要 jinja 2.6 怎么办？
> 这种情况下，每个应用可能需要各自拥有一套“独立”的 Python 运行环境。`virtualenv` 就是用来为一个应用创建一套“隔离”的 Python 运行环境。

### pylint

> 摘自：[如何使用 Pylint 来规范 Python 代码风格](javascript:void())
>
> Pylint 是一个 Python 代码分析工具，它分析 Python 代码中的错误，查找不符合代码风格标准（Pylint 默认使用的代码风格是 PEP 8，具体信息，请参阅参考资料）和有潜在问题的代码。

简单的来说，Pylint 为我们提供了纠错的功能，如果你希望在你的代码中，及时发现标注波浪线的错误，请安装它。

### yapf

> 摘自：[有哪些命令行的软件堪称神器？ - int32bit的回答 - 知乎](javascript:void())
>
> Google开发的python代码格式规范化工具，支持pep8以及Google代码风格。

简单的说， yapf 为我们提供了格式化代码的功能，如果你希望在你的代码中，使用 `Alt` + `Shfit` + `F` 来自动格式化你的 Python 代码，请安装它。

### 安装过程

使用下面的命令依次安装他们：

```
pip install virtualenv
pip install pylint
pip install yapf
```

### 安装中可能出现的问题

下面总结一下，笔者在安装中出现过的问题，以及解决方法。

#### UnicodeEncodeError 'utf-8' codec can't encode character...

这个也是一个比较常见的问题，遇到这个问题时，可以参考错误中的倒数第三行中的路径：

```
...
File "c:\users\xxx\appdata\local\programs\python\python36-32\lib\site-packages\pip\compat\__init__.py", line 75, in console_to_str
    return s.decode('utf_8')
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc1 in position 55: invalid start byte
```

比如，上面的错误中，我们打开`c:\users\xxx\appdata\local\programs\python\python36-32\lib\site-packages\pip\compat\__init__.py`这个文件，定位到 第 75 行。
将 `return s.decode('utf_8')` 改为 `return s.decode('cp936')`
如上操作可能需要管理员权限，建议使用 `Windows` + `X` 使用管理员权限的命令提示符或者管理员权限的 PowerShell。
然后输入 `code c:\users\xxx\appdata\local\programs\python\python36-32\lib\site-packages\pip\compat\__init__.py` 改成对应你的文件名。

## 3. 修改 vscode 中的设置

打开 vscode，进入 文件 > 首选项 > 设置，按照下面的注释修改对应的值。

```
// 如果使用 pylint， 设置下面的为 true。如果使用其他语法纠错的库，可以将对应的设置为 true，其他的设置为 false。
    "python.linting.pylintEnabled": true

    // 如果安装了 yapf，并且希望使用 yapf 格式化代码的，请修改下面的选项。
    "python.formatting.provider": "yapf"
```

## 4. 使用 virtualenv 创建工程目录

为每一个 Python 项目配置一个独立的环境和目录，是一个比较好的想法，这样你可以根据需要安装不同的库以及版本。
这一小节，将使用 virtualenv 创建一个虚拟环境，并且安装 flask。

首先，我们先启动一个具有管理员权限的 PowerShell。（你也可以使用 CMD）
假设我们需要将项目放在 `D:\pydemo\` 这个文件夹内。

### 创建文件夹并配置虚拟环境

```
PS D:\> mkdir pydemo

PS D:\> cd pydemo

PS D:\pydemo> virtualenv --no-site-packages .venv
Using base prefix 'c:\\program files\\python36'
New python executable in D:\pydemo\.venv\Scripts\python.exe
Installing setuptools, pip, wheel...done.

PS D:\pydemo>
```

如果出现上面的提示，就说明安装已经完成了，接下来我们要将 PowerShell 的环境切换到这个虚拟环境中。

在 PowerShell 中：

```
PS D:\pydemo> ./.venv/Scripts/activate.ps1
(.venv) PS D:\pydemo>
```

如果提示错误，可以尝试使用下面的方法解决

```
(.venv) PS D:\pydemo> Set-ExecutionPolicy RemoteSigned

执行策略更改
执行策略可帮助你防止执行不信任的脚本。更改执行策略可能会产生安全风险，如 http://go.microsoft.com/fwlink/?LinkID=135170
中的 about_Execution_Policies 帮助主题所述。是否要更改执行策略?
[Y] 是(Y)  [A] 全是(A)  [N] 否(N)  [L] 全否(L)  [S] 暂停(S)  [?] 帮助 (默认值为“N”): Y
```

如果你使用的是 CMD，则使用下面的命令：

```
D:\pydemo> ./.venv/Scripts/activate.bat
(.venv) D:\pydemo>
```

### 往虚拟环境中安装包

如果你的命令行，或者 PowerShell 已经变成了

```
(.venv) PS D:\pydemo>
```

前面有一个括号，表示的是你最开始创建的虚拟环境的位置，那么这就说明你已经把上下文的环境切换到了虚拟环境里面。
我们在这里面安装的 pip 就不会放到公共的 site-packages 里面了。

执行下面的命令安装 flask 和 watchdog（如果又出现 UnicodeEncodeError，参考上一节所描述的解决方案，修改虚拟环境中的 `__init__.py`。）

```
(.venv) PS D:\pydemo> pip install flask
Collecting flask
  Using cached Flask-0.12.2-py2.py3-none-any.whl
Collecting Jinja2>=2.4 (from flask)
  Using cached Jinja2-2.10-py2.py3-none-any.whl
Collecting Werkzeug>=0.7 (from flask)
  Using cached Werkzeug-0.12.2-py2.py3-none-any.whl
Collecting click>=2.0 (from flask)
  Using cached click-6.7-py2.py3-none-any.whl
Collecting itsdangerous>=0.21 (from flask)
Collecting MarkupSafe>=0.23 (from Jinja2>=2.4->flask)
Installing collected packages: MarkupSafe, Jinja2, Werkzeug, click, itsdangerous, flask
Successfully installed Jinja2-2.10 MarkupSafe-1.0 Werkzeug-0.12.2 click-6.7 flask-0.12.2 itsdangerous-0.24

(.venv) PS D:\pydemo> pip install watchdog
Collecting watchdog
Collecting argh>=0.24.1 (from watchdog)
  Using cached argh-0.26.2-py2.py3-none-any.whl
Collecting PyYAML>=3.10 (from watchdog)
Collecting pathtools>=0.1.1 (from watchdog)
Installing collected packages: argh, PyYAML, pathtools, watchdog
Successfully installed PyYAML-3.12 argh-0.26.2 pathtools-0.1.2 watchdog-0.8.3

(.venv) PS D:\pydemo>
```

安装完成之后，我们可以从 PowerShell 中直接运行 vscode 并且将工作目录设置为当前目录（也就是`D:\pydemo`）。

```
(.venv) PS D:\pydemo> code .
```

## 5. 修改 launch.json

打开 vscode 之后，使用 `Ctrl` + `Shift` + `D`，或者点击侧边栏的调试选项，调出调试选项侧边栏。
然后点击齿轮 配置或修复 "launch.json"，自动生成一个 `launch.json`。
如果出现选择环境，我们选择 `Python`。

在 configurations 中，我们仅保留 `"name": "Python: Flask (0.11.x or later)"`这一段。其他的全部删掉。

将这一段配置中的下面几个选项重新配置一下：

```
// 将 Python 指定为虚拟环境中的 Python
"pythonPath": "${workspaceRoot}/.venv/Scripts/python.exe"

// 将 program 和 env.FLASK_APP 都设定为你这个项目的入口文件。
"program": "${workspaceRoot}/main.py"
"env": {
    "FLASK_APP": "${workspaceRoot}/main.py"
}
```

配置完之后，应该是这样的：

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Flask (0.11.x or later)",
            "type": "python",
            "request": "launch",
            "stopOnEntry": false,
            "pythonPath": "${workspaceRoot}/.venv/Scripts/python.exe",
            "program": "${workspaceRoot}/main.py",
            "cwd": "${workspaceRoot}",
            "env": {
                "FLASK_APP": "${workspaceRoot}/main.py"
            },
            "args": [
                "run",
                "--no-debugger",
                "--no-reload"
            ],
            "envFile": "${workspaceRoot}/.env",
            "debugOptions": [
                "WaitOnAbnormalExit",
                "WaitOnNormalExit",
                "RedirectOutput"
            ]
        }
    ]
}
```

保存并关闭。

## 6. 创建测试代码并运行测试

使用 `Ctrl` + `Shift` + `E` 或者点击左侧边栏的文件，回到文件侧边栏。
在 pydemo 中，我们新建一个文件，名为`main.py`。如果你上面的配置指定的是其他文件名，可以修改成你自己指定的。

并加入下面的代码：

```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == '__main__':
    app.debug = False
    app.run(host='localhost', port=5000)
```

这里必须将 `app.debug` 设置为 `False`，否则会出现一直`Restarting`。
按下 `F5` 运行代码，将会在 调试控制台 中看到：

```
* Running on http://localhost:5000/ (Press CTRL+C to quit)
```

这个时候，我们可以通过浏览器访问`http://localhost:5000/`，会有 `Hello World!` 显示。
到此，我们的环境配置就完成了。

------

参考文章：
[https://www.liaoxuefeng.com/w...](javascript:void())

相关文章

- \1. [visual studio code的python配置](http://www.voidcn.com/article/p-qzsqxrsh-bqk.html)
- \2. [Visual Studio Code配置PHP开发环境](http://www.voidcn.com/article/p-auxevymd-bpe.html)
- \3. [.NET Core Visual Studio Code 环境配置](http://www.voidcn.com/article/p-mhmkdaem-mm.html)
- \4. [在visual studio 2005中配置iup环境](http://www.voidcn.com/article/p-zaxswenx-bm.html)
- \5. [在Visual Studio Code中配置GO开发环境](http://www.voidcn.com/article/p-ccosskib-mm.html)
- \6. [Visual Studio+Opencv2.4.9环境配置](http://www.voidcn.com/article/p-bwxurqxs-r.html)
- \7. [Visual Studio Code配置](http://www.voidcn.com/article/p-pramsgbc-bqg.html)
- \8. [visual studio code配置python开发环境的一点心得](http://www.voidcn.com/article/p-diddszqe-bpu.html)
- \9. [在Visual Studio Code配置GoLang开发环境](http://www.voidcn.com/article/p-dhfkrrtb-bec.html)
- \10. [Visual Studio Code 配置指南](http://www.voidcn.com/article/p-hanubzrx-bpe.html)
- [更多相关文章...](http://www.voidcn.com/relative/p-gfgctiug-bqz.html)

相关标签/搜索

[Visual Studio 2012环境](http://www.voidcn.com/tag/Visual+Studio+2012环境) [Visual Studio 配置](http://www.voidcn.com/tag/Visual+Studio+配置) [visual-studio-code](http://www.voidcn.com/tag/visual-studio-code) [Visual Studio Code](http://www.voidcn.com/tag/Visual+Studio+Code) [python环境配置](http://www.voidcn.com/tag/python环境配置) [android studio 环境配置](http://www.voidcn.com/tag/android+studio+环境配置) [Android studio环境配置](http://www.voidcn.com/tag/Android+studio环境配置) [visual studio环境搭建](http://www.voidcn.com/tag/visual+studio环境搭建) [Flask+uwsgi环境](http://www.voidcn.com/tag/Flask%2Buwsgi环境) [Flask环境](http://www.voidcn.com/tag/Flask环境) [Visual Studio配置](http://www.voidcn.com/cata/1181765) [环境配置](http://www.voidcn.com/cata/1315515) [环境配置](http://www.voidcn.com/cata/1390483) [环境配置](http://www.voidcn.com/cata/1231062) [环境配置](http://www.voidcn.com/cata/2034515) [环境配置](http://www.voidcn.com/cata/5721023) [环境配置](http://www.voidcn.com/cata/1130455) [环境配置](http://www.voidcn.com/cata/510767) [环境配置](http://www.voidcn.com/cata/1352483) [环境配置](http://www.voidcn.com/cata/795170) [Visual Studio](http://www.voidcn.com/column/visual-studio) [Python](http://www.voidcn.com/column/python) [visual studio code java 环境](http://www.voidcn.com/search/enzomb) [visual studio 配置mysql编译环境](http://www.voidcn.com/search/zurvib) [vs code 配置C++环境](http://www.voidcn.com/search/ztjzpo) [android studio uiautomatorview环境配置](http://www.voidcn.com/search/fgbfiw) [uiautomator android studio 环境配置](http://www.voidcn.com/search/ostwyu) [uiautomator Android studio 环境配置](http://www.voidcn.com/search/ufishu) [python elephas 环境配置](http://www.voidcn.com/search/cjzesb) [visual studio 2012在win10 上安装并配置QT 环境](http://www.voidcn.com/search/pvnird) [IntelliJ IDEA中Python环境配置](http://www.voidcn.com/search/bdssnq) [在dev cpp中配置OpenGL的环境](http://www.voidcn.com/search/edtwwc)