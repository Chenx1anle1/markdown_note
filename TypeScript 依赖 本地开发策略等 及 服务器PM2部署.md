### 服务器PM2部署 && TypeScript 依赖 本地开发策略等 

> **服务器PM2部署**
>
> PM2支持配置**文件方式**进行应用服务设置，**文件**支持的**配置格式**为`Javascript`、`JSON`、`YAML`。
>
> ```
> 
> ```
>
> <img src="C:%5Cworkshop%5C%E5%B7%A5%E4%BD%9C%E7%AC%94%E8%AE%B0-%E8%AE%B0%E5%BD%95%20markdown%20Typora%5Cimsges%5Cimage-20201028134044684.png" alt="image-20201028134044684" style="zoom:33%;" />

**TypeScript** 编写的项目配置

> 创建pm2.yaml
>
> ```
> //pm2.yaml
> apps:
>     interpreter: ./node_modules/.bin/ts-node
>     script: ./src/index.ts
>     name: dowinAPI
>     env_production:
>         NODE_ENV: production
>         HOST: localhost
>         PORT: 3000
> ```
>
> 

**TypeScript 依赖 本地开发策略**