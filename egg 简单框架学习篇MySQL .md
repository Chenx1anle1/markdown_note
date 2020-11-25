#### egg 学习篇

**学习目标**：

+ 安装好NodeJS
+ 安装好yarn & tyarn （加速node依赖包的下载）（优势于 npm & cnpm）
  + npm install -g yarn tyarn | npm i -g yarn tyarn
+ 安装配置 VS Code
+ Umi + TypeScript + Egg.js建议列表开发

#### **准备工作：**

> **后端建表**
>
> <img src="C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027165228274.png" alt="image-20201027165228274" style="zoom: 67%;" />

> **前端实现**
>
> <img src="C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027165313808.png" alt="image-20201027165313808" style="zoom:67%;" />

#### **开发环境**

> ```
> node -version | node -v
> npm -version | npm -v
> #安装
> npm i -g yarn tyarn | npm install -g yarn tyarn 
> #检查
> yarn -version | yarn -v
> #vs code
> #项目下 code . 启动vscode 文件夹项目
> mkdir demo-server
> cd demo-server
> ```
>
> **工作步骤**
>
> ![image-20201027170132660](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027170132660.png)
>
> ```
> #egg 项目生成器 Generator
> #不设置type 进入选择状态
> npm init egg --type=simple
> 
> # egg.js MySQL数据库驱动依赖
> tyarn add egg-mysql
> 
> 
> ```
>
> ```
> 在egg项目中 使用TypeScript
> $ mkdir showcase && cd showcase
> $ npm init egg --type=ts
> $ npm i
> $ npm run dev
> ```
>
> **本次开发使用simple**
>
> <img src="C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027171336968.png" alt="image-20201027171336968" style="zoom:67%;" />
>
> ```
> demo-server code ./
> 使用VS Code 打开当前文件夹（项目 demo-server）
> demo-server subl ./
> 使用 Sublime text3 打开项目
> ```

#### **项目配置及编写**

> Egg 项目插件安装 引入依赖 
>
> **配置方法** 1 plugin
>
> <img src="C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027172201643.png" alt="image-20201027172201643" style="zoom:67%;" />
>
> **配置方法** 2 config.default
>
> <img src="C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027172532726.png" alt="image-20201027172532726" style="zoom:67%;" />
>
> + 编写Controller
>
>   + ```
>     引入
>     extends
>     导出
>     ```
>
>   + ![image-20201027175447794](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027175447794.png)
>
> + 并配置API路由
>
>   + <img src="C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027175419842.png" alt="image-20201027175419842" style="zoom:67%;" />
>
> + 编写Service，实现数据库查询
>
>   + ![image-20201027175115723](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201027175115723.png)
>
> + 测试API
>
> 1
>
> 1
>
> ```
> tyarn dev
> 运行
> ```
>
> 









