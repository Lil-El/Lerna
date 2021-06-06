# 概念

-   monoRepo：将所有模块统一在一个主干分支上
-   multiRepo：一个项目就是一个仓库

# Lerna

## 安装

```shell
    npm i lerna -g
```

## 命令

```
    lerna init - 初始化
        package.json - private: true(私有的，不会发布到npm上)
    lerna bootstrap - 安装依赖
    lerna clean - 删除各个包下的node_modules
    lerna list - 查看本地包列表
    lerna change - 显示自上次release tag以来有修改的包
    lerna diff - 显示自上次release tag以来有修改的包
    lerna exec - 在每个包目录下执行任意命令
    lerna run - 执行每个包package.json的命令
    lerna add 添加一个包的版本为各个包的依赖
    lerna import 引入package
    lerna link 连接相互引用的库
    lerna create 新建package
    lerna publish 发布
```
## 配置
- package.json: 配置workspace为packages/*
- lerna.json: 配置npmClient为yarn；useWorkspace：true

## yarn和lerna
yarn和lerna很多命令时等价的；
- yarn 用于处理依赖
 - lerna 用于初始化和发包

--------

# 初始化

1. lerna init
2. lerna create mino-cli
3. lerna create mino-utils
4. 在mino-cli的bin目录的index.js中引入utils的文件；（按照以往是需要将utils包进行link，然后才能引用）
5. **yarn**：自动安装依赖，并将各个包link至node_modules中；那么此时上一步就可以引入成功了
   1. 如果希望其他的项目也可以使用mino-utils，需要在utils的package.json配置bin:{mino-utils: "bin/index.js"}
   2. 进入utils目录，执行npm link
   3. 全局的node_modules就会拥有utils目录的软链接
6. package.json创建script命令**create**：类似于vue create [package name]，执行mino-cli的bin的文件
7. 给项目安装依赖
   1. 进入mino-cli目录下，执行yarn workspace mino-cli add chalk jquery（依赖会被安装至根目录的node_modules中）


[Lerna](https://segmentfault.com/a/1190000023160081)

[zhu-cli](http://www.zhufengpeixun.com/grow/html/133.vue-cli.html)
