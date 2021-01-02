
### 前端工程化(1)：process.env环境的使用


#### 0 

>在前端工程化中，我们需要根据开发环境还是生产环境来进行判断某些函数是否执行、某些字段是否变化。__简单来说就是环境变量__

#### 1 简单的例子

一个最简单的例子，从[vue-template-admin](
https://github.com/PanJiaChen/vue-admin-template)的```vue.config.js```某一行来说.
```javascript
const port = process.env.port || process.env.npm_config_port || 9528 // dev port
```
这个赋值语句赋值了访问端口声明 `process.env.port` 代表着当前环境的端口。如果没有的话那就去找`process.env.npm_config_port`这个属性,哈爱是没有的话就赋值9528.

#### 2.process.env

`process`是什么？这是node官方文档给出的：
>process 对象是一个全局变量，提供了有关当前 Node.js 进程的信息并对其进行控制。 作为全局变量，它始终可供 Node.js 应用程序使用，无需使用 require()。 它也可以使用 require() 显式地访问。


`process.env`的解释:
>process.env 属性会返回包含用户环境的对象

#### 3.vue/cli中的使用

一个vue项目中有三个模式 ：

* `development` 用于 vue-cli-service serve 开发环境
* `production` 用于vue-cli-service build 生产环境
* `test` 用于vue-cli-service test 测试环境

vue-cli中还有对应的 __环境文件__

>当运行 vue-cli-service 命令时，所有的环境变量都从对应的环境文件中载入。如果文件内部不包含 NODE_ENV 变量，它的值将取决于模式，例如，在 production 模式下被设置为 "production"，在 test 模式下被设置为 "test"，默认则是 "development"。

我们先在vue.config.js中的同级文件中创建:`.env.production` 和 `.env.development’
```sh
#.env.development
# 定义一个环境变量
FOO = 'chj-dev'
```

```sh
#env.production
# 定义一个环境变量
FOO = 'chj-pro'
```

在 __新创建好的vue脚手架项目中__ 更新`vue.config.js`
```javascript
const env = process.env.NODE_ENV || "noENV here"
const foo = process.env.FOO || "no FOO here"
console.log(env, foo)
```

现在我们运行 npm run serve:
![npm run serve](https://img-blog.csdnimg.cn/2021010221525727.png)

现在我们运行 npm run build:
![ npm run build](https://img-blog.csdnimg.cn/20210102215404576.png)


可以看到相应的环境变量已经输出。以后的项目可以由此来判断真减条件、变更变量
。
