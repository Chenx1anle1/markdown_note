## 码云gitee本地初始化项目基本设置

直接bash中敲代码

##### 1、本地初始化一个项目

```php
git config --global user.name "你的名字或昵称"
git config --global user.email "你的邮箱"
```

##### 2、初始化版本库的文件夹中

```ruby
git init 
git remote add origin <你的项目地址> // 注:项目地址形式为:https://gitee.com/xxx/xxx.git或者 git@gitee.com:xxx/xxx.git
```

注：如果想长期记住密码，如下操作

```cpp
git remote add origin http://您的账号:你的密码@gitee.com/您的项目地址.git
```

##### 3、克隆一个项目

```
git clone <项目地址>
```

##### 4、完成第一次提交

```
git pull origin master
<这里需要修改/添加文件，否则与原文件相比就没有变动>
git add .
git commit -m "第一次提交"
git push origin master

至此完成远程项目的本地初始化
```

延伸操作：
[码云gitee利用PHP脚本拉取实现自动部署（可用于生产环境）](https://www.jianshu.com/p/5b9d6ca85233)

------

##### 扩展信息

+ 如果你原本使用的仓库地址，可以执行以下命令

```cpp
// 删除原本的ssh仓库地址
git remote rm origin // origin 代表你原本ssh地址的仓库的别名
// 新增http地址的仓库
git remote add origin https://gitee.com/username/project.git
```

+ 其他记住密码操作

按照以下设置记住密码十五分钟：

```php
git config --global credential.helper cache
```

如果你想自定义记住的时间，可以这样：

```java
git config credential.helper 'cache --timeout=3600' //这里记住的是一个小时，如需其他时间，请修改3600为你想修改的时间，单位是秒
```

你也可以设置长期记住密码：

```php
git config --global credential.helper store  // 建议还是用上面第2点提到的记住密码方式，方便多项目操作
```

+ Git提交代码到码云

```java
git add .    // 提交当前目录下的所有文件；
git commit -m '注释'    // 添加注释
git pull     //下载服务器代码 这是为了同步最新远程文件到本地，防止冲突
git push    // 传代码至服务器
```