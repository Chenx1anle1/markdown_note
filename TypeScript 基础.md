#### TypeScript 基础

> ![image-20201028002216077](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028002216077.png)
>
> JavaScript中没有数据类型；定义变量时直接写一个名字就行了；
>
> 比如当我们封装好的一些方法或者模块，别人不知道我们的参数类型时 调用就会出错，即一种不可预见的错误。“TypeScript让我们来更规范的写代码”
>
> **环境**
>
> ```
> nodejs环境
> VS Code
> 
> #安装TS环境和常见的命令
> sudo npm i typescript -g #全局安装TypeScript
> sudo npm install typescript -g #全局安装TypeScript
> 
> tsc -v #查看TS版本
> tsc --init #初始化一个ts的项目编译配置 生成配置文件 tsconfig.json
> tsc -w #监听当前项目文件夹中的ts文件改变之后编译生成对应的js文件
> ```
>
> **配置文件  tsconfig.json  的解读**
>
> ```
> tsc --init #初始化编译环境 tsconfig.json文件
> ```
>
>  ![image-20201028011245449](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028011245449.png)
>
> #### 第一段TS代码
>
> ```
> github 源码
> https://github.com/btc022003/egg-ts-common-base-app
> 本机
> /workshop/nodeJS/egg-ts-common-base-app/
> ```
>
> **.gitignore配置参考**
>
> <img src="C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028015923224.png" alt="image-20201028015923224" style="zoom: 67%;" />![image-20201028020341050](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028020341050.png)
>
> ```
> 创建src
> mkdir src
> tsc main.ts
> ```
>
> ```typescript
> // main.ts
> function sun(a: number, b: number): number {
> 	return a + b
> }
> console.log(sum(3, 4));
> ```
>
> ![image-20201028011634894](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028011634894.png)
>
> ```bash
> tsc
> tsc #主动生成dist/main.js js文件的命令
> ```
>
> ```javascript
> //main.js
> "use scrict";
> function sum(a, b) {
> 	return a + b;
> }
> console.log(sum(3, 4));
> ```
>
> TS中常见数据类型
>
> ```
> string
> boolean
> number
> 等等 
> ```
>
> 项目html文件使用main.js  **如图引用**
>
> ![image-20201028012240806](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028012240806.png)
>
> ```
> tsc -w #监听ts文件命令的使用 （保存触发）
> ```
>
> TypeScript 总结
>
> ```
> 针对我们不确定的数据类型的变量为其添加预定义好的类型
> ```
>
> 

#### Egg.js中使用TypeScript

> ```
> npm init egg --type=ts #初始化一个 ts 版本的egg
> 生成器 提问选项 默认执行即可
> 
> npm install | npm i #安装依赖项
> npm run dev
> ```
>
> ![image-20201028012849616](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028012849616.png)
>
> 分别 理解 
>
> ```
> ./app/router.ts
> ./app/controller/home.ts
> ./app/service/test.ts
> ```
>
> 

#### Egg TypeScript 项目编写的理解流程

> controller => router.ts
>
> controller => service => controller => router.ts
>
> 数据库依赖 jwt 依赖等 流程

#### 如何在egg ts 项目中 使用 mongoo DB数据库快速搭建一系列API

> README.md 编写说明
>
> ```
> README.md
> ​```
> mongoose 数据库插件
> restful post/get/delete/put
> class 的继承
> ​```
> ```
>
> **mongoes 插件/依赖 安装  引入**
>
> ![image-20201028014017376](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028014017376.png)
>
> ```
> npm i egg-mongoose
> ```
>
> **引入**
>
> ```typescript 
> //   ./config/plugin.ts
> import { EggPlugin } from 'egg';
> 
> const plugin: EggPlugin = {
> 	//static: true,
> 	nunjucks: {
> 		enable: true,
> 		package: 'egg-view-nunjucks'
> 	},
> 	mongoose: {
> 		enable: true,
> 		package: 'egg-mongoose'
> 	}
> }
> ```
>
> 代码snyc 报错 vscode 自动补全操作
>
> ```
> // ./.prettierrc
> {
> 	"singleQuote": true, //设置单引号
> 	"trailingComma": "all" //设置不全逗号
> }
> ```
>
> ![image-20201028015204522](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028015204522.png)
>
> **rescources路由设置**
>
> ![image-20201028020810509](C:%5CUsers%5Cdemon%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201028020810509.png)
>
> 8-增删改查功能实现
>
> ```python
> #知识点
> 分类页实现
> Math.ceil() 向上取整
> 注释 /** */
> /**
> * 分页方式获取数据
> * @param query   查询条件
> * @param page    当前页码
> * @param per     每页显示的数量
> */
> async list(query = {}, page = 1, per = 10) {
>     const data = await this.app.model[this.model]
>     .find(query)
>     .limit(per)
>     .skip((page - 1) * per)
>     .sort({
>         _id: -1,
>     });
>     const totalCount = await this.app.model[this.model].count(query);
>     return {
>         totalCount,
>         pages: Math.ceil(totalCount / per),
>         data,
>     };
> }
> limit//
>     skip//跳过
>     sort//排序
>     count//count
> 
> 
> findById //(id: string)根据d查找单条记录
> findByIdAndUpdate //(id: string, data: any)根据id修改单条记录
> insertMany(models) //参数(models: any[])保存多条记录
> findByIdAndDelete(id) //(id: string)根据id删除单条记录
> remove({$in: ids}) //参数(ids: string[]) 根据ids删除多个数据
> //(data: any)保存单条
>     const result = new this.app.model[this.model](data);
>     await result.save();
> ```
>
> 9-base-service代码提取
>
> ```
> 基础操作 每张表都存在 所以提取封装 类的继承（继承一些基础的功能 就不用重复写一些基础代码）
> 服务封装
> ./app/service/base.ts
> ./app/model
> ```
>
> 10-service代码优化
>
> 11-控制器封装
>
> ```
> base控制器
> ./app/controller/api/v1/admin/base.ts
> ```
>
> 12-最简单的方式创建一个功能
>
> model => service => controller => router.ts
>
> 20行代码新增article 方便！！！
>
> 封装 值得拥有

