#### uni-app支持快应用（Light版），欢迎体验

[快应用](https://www.quickapp.cn/)是基于手机硬件平台的新型应用形态，标准由国内主流手机厂商联合制定。

快应用可以认为是手机硬件厂商的小程序，但和微信、支付宝等小程序又有较大不同：

- 微信、支付宝、百度、字节跳动等各家小程序架构设计接近，开发规范接近，都是基于webview渲染，布局方式一致，开发者开发不同小程序时，学习成本较低，且可借助跨端框架或转换器快速实现多平台发行。
- 快应用是单独的架构设计，单独的开发规范，基于 Native 原生渲染（相比web，布局上有更多限制），有额外的学习成本，且项目代码不易与 Web、小程序等相互复用

这些差异，严重制约了快应用生态的发展，参与的开发者少，提交的快应用的数量也很少，不过几千款，与微信的百万级应用数差距很大。

为此，vivo、华为等厂积极探索，推出快应用(Light 版)（为叙述方便，下文统称为「快应用」），它同小程序一样，采取 Webview 渲染方式，使得开发者没有额外学习成本（有 Web、小程序开发经验即可），能够使用 Web 上各种能力，同时令用户有良好应用访问体验。

uni-app在第一时间跟进了快应用新引擎适配，目前已在 uni-app 的 vue-cli alpha版中完成了对快应用-Light版的适配，本文简单介绍体验方式，欢迎有兴趣的各位一起共研完善。

## 创建项目

开发者按照如下方式基于`vue-cli`创建`uni-app`项目，编译发行到快应用-Light版：

```shell
# npm script
# 全局安装vue-cli
$ npm install -g @vue/cli
# 创建uni-app项目，会提示选择项目模板，初次接触建议选择 hello uni-app 模板
$ vue create -p dcloudio/uni-preset-vue#alpha my-project
# 进入项目目录
$ cd my-project
# dev 模式，编译预览
$ npm run dev:quickapp-light
# build 模式，发行打包
$ npm run build:quickapp-light
1234567891011
```

编译目录为: `dist\(dev|build)\quickapp-light`

## 预览测试

1. 下载开发者工具，快应用-Light 版目前尚处于测试阶段，开发工具及测试基座尚未统一:

- vivo：直接从快应用-Light 版官网下载开发工具，详见：[https://www.hellohub.cn/](https://www.hellohub.cn/framework/quickstart/getstart.html#安装开发工具)
- 华为：从华为官网下载，详见：[安装华为快应用IDE](https://developer.huawei.com/consumer/cn/doc/development/quickApp-Guides/quickapp-installtool)；

1. 启动开发者工具，打开编译后的项目目录：`dist\(dev|build)\quickapp-light`
2. 将手机与电脑成功连接，并打开“开发者调试”模式
3. 点击顶部菜单的`运行`按钮，开发者工具会通过USB自动安装调试 apk 到手机上，并自动启动基座进行测试

## 欢迎共研

所有快应用适配代码，均已开源在[github](https://www.github.com/dcloudio/uni-app)，欢迎star鼓励！也欢迎加入QQ群交流：148203425。

如果你对原生渲染的快应用适配感兴趣，也欢迎参与社区共研，详见 https://ask.dcloud.net.cn/article/37145。