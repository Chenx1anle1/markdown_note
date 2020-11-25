## 在 WIndows 10 上装 Vim （几乎和 Linux 或 MacOS 下的 vim 一摸一样）

一、下载 Vim

http://www.canadiancontent.net/tech/download/Vim_for_Windows.html

如果是压缩包下载，解压后记得添加到环境变量里面。

然后就可以打开 PowerShell 愉快地玩耍了~（按住shift右击，打开power shell）

输入 vim -v    测试环境变量



Vim 在 PowerShell 上已经和 Linux 上的几乎一摸一样了

解决非 UTF-8 乱码和默认 GBK 的问题：

在 vim.exe 所在目录的 defaults.vim 文件最后加入以下语句：

```
set encoding=utf-8
set langmenu=zh_CN.UTF-8
language message zh_CN.UTF-8
```


上面的语句还会自动使得其他格式的编码转化成 UTF-8 的编码，只要不保存就不会用 UTF-8 编码的文件覆盖掉原来文件。

设置 Tab 为四个空格，也是在  defaults.vim 文件最后加入以下语句：

```
set ts=4
set expandtab
```


总之，所有在 linux 下在 .vimrc 中配置的命令，都可以在 defaults.vim 文件中进行配置