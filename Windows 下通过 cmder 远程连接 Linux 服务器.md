## Windows 下通过 cmder 远程连接 Linux 服务器

> 阅读引导
> \1. 需要先在 Windows 系统中安装 [cmder](https://links.jianshu.com/go?to=http%3A%2F%2Fcmder.net%2F)
> \2. 文中用 "<xxx>" 表示的字符均需替换为自己机器中真实的名称（注意去掉 <>）
> \3. 以 "$ " 开头的命令代表需要在命令行工具中输入，输入时不需要带上 "$ " 字符。

### 前言

SSH 为 [Secure Shell](https://links.jianshu.com/go?to=https%3A%2F%2Fbaike.baidu.com%2Fitem%2FSecure%20Shell) 的缩写，由 IETF 的网络小组（Network Working Group）所制定；SSH 为建立在应用层基础上的安全协议。SSH 是目前较可靠，专为[远程登录](https://links.jianshu.com/go?to=https%3A%2F%2Fbaike.baidu.com%2Fitem%2F%E8%BF%9C%E7%A8%8B%E7%99%BB%E5%BD%95%2F1071998)会话和其他网络服务提供安全性的协议。利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。

SSH 目前提供两种级别的安全验证

- 基于口令的安全验证
- 基于秘钥的安全认证（不需要在网络上传输口令，相对来说更加安全）

### 方式一：通过 SSH 口令方式连接

1. 打开 cmder
2. 输入以下命令按回车确认



```bash
$ ssh <username>@<server-ip-address>
```

1. 根据给出的提示输入用户密码，按回车确认
2. 登录成功

### 方式二：通过 SSH 密钥方式连接（实现无密码登录）

*请先检查本机目录 `C:\Users\<用户名>\.ssh` 下是否有 `id_rsa` 和 `id_rsa.pub` 两个文件，如果有直接上传公钥 `id_rsa.pub` 到 Linux 服务器（步骤2）即可，无需再生成密钥对*

1. 在本机生成 SSH 密钥对

   1.1 打开 cmder

   1.2 输入以下命令按回车确认

   ```bash
$ ssh-keygen -t rsa
   ```
   
   1.3 弹出密钥保存位置提示后，继续按回车（密钥对将生成到默认位置）

   

   ```
C:\Users\<用户名>\.ssh\
   ```
   
   

   1.4 弹出输入密码提示后，继续按回车（此时不设置密钥对验证密码）

   1.5 弹出确认密码提示后，继续按回车

   1.6 检查本机目录

    

   ```
C:\Users\<用户名>\.ssh\
   ```
   
    

   下存在

    

   ```
id_rsa
   ```
   
    

   和

    

   ```
id_rsa.pub
   ```
   
    

   两个文件

   1.7 密钥对生成完毕

2. 上传公钥到 Linux 服务器

   2.1 通过方式一连接到 Linux 服务器

   2.2 在远程服务器上输入以下命令

   

   ```bash
   $ mkdir ~/.ssh && touch ~/.ssh/authorized_keys
   $ chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys
   ```

   2.3 在本机输入命令

   

   ```bash
   $ scp C:\Users\<用户名>\.ssh\id_rsa.pub <username>@<server-ip-address>:~/.ssh/authorized_keys
   ```

   2.4 输入密码后，按回车确认

   2.5 上传成功后输入以下命令即可成功连接服务器

   

   ```bash
   $ ssh <username>@<server-ip-address>
   ```

   2.6 配置

    

   ```
   config
   ```

    

   文件简化登录输入

   

   ```bash
   $ vim C:\Users\<用户名>\.ssh\config
   ```

   输入以下内容：

   

   ```xml
   Host <name-you-want>
     HostName <server-ip-address>
     User <username>
     PubkeyAuthentication yes
   ```

   ```
   config
   ```

    

   文件创建好后，直接输入以下命令登录服务器

   

   ```ruby
   $ ssh <name-you-want>
   ```

###### 附：另外附上 cmder 的一些初始化配置



```bash
##### 添加至环境变量
将 cmder.exe 存放的目录添加到系统环境变量 Path <br>
Win+R 打开运行，输入 cmder 按回车打开 cmder <br>

##### 添加至右键菜单（需要运行管理员权限）
以管理员身份运行 cmd 输入命令：`Cmder.exe /REGISTER ALL`

##### 解决中文显示乱码问题
Settings --> Startup --> Environment 添加
`set LANG=zh_CN.UTF-8`

##### 修改默认的命令提示符λ改成$
将 `cmder\vendor\clink.lua` 文件中第42行中 `local lambda = "λ"` 修改为 `local lambda = "$"` <br>
```

参考来源：
[https://github.com/cmderdev/cmder/blob/master/README.md](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fcmderdev%2Fcmder%2Fblob%2Fmaster%2FREADME.md)
[https://www.linode.com/docs/security/authentication/use-public-key-authentication-with-ssh/](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.linode.com%2Fdocs%2Fsecurity%2Fauthentication%2Fuse-public-key-authentication-with-ssh%2F)