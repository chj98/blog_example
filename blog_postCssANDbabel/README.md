
### 前端工程化(2)：postCss 和 babel的使用

本文例子可以[点击这里](https://github.com/chj98/blog_example/tree/main/blog_postCssANDbabel)
#### 0 前言 
babel是什么：
官网给出的定义
>Babel 是一个工具链，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。

postcss是什么：
官网给出的的定义：
>PostCSS 是一个允许使用 JS 插件转换样式的工具。 这些插件可以检查（lint）你的 CSS，支持 CSS Variables 和 Mixins， 编译尚未被浏览器广泛支持的先进的 CSS 语法，内联图片，以及其它很多优秀的功能。

>PostCSS 接收一个 CSS 文件并提供了一个 API 来分析、修改它的规则（通过把 CSS 规则转换成一个抽象语法树的方式）。在这之后，这个 API 便可被许多插件利用来做有用的事情，比如寻错或自动添加 CSS vendor 前缀。

总而言之：这两个插件对于前端工程化是非常重要的

#### 1 在vuecli中使用postcss

使用vue-cli 安装一个脚手架
``` sh
vue create vue_postcssbabel
```
因为vue-cli已经内置postcss-loader，所以直接之前根目录下新建文件`postcss.config.js` 即可

在该文件上注册插件
``` javascript
module.exports = {
    'plugins': {
        'autoprefixer': {},
        'cssnano': {},
        'postcss-preset-env': {}
    }
}
```
推荐插件可以去[postcss官网](https://www.postcss.com.cn/)上查看

这里介绍三个常用插件
>autoprefixer:利用从 Can I Use 网站获取的数据为 CSS 规则添加特定厂商的前缀。 Autoprefixer 自动获取浏览器的流行度和能够支持的属性，并根据这些数据帮你自动为 CSS 规则添加前缀。

>PostCSS Preset Env:将最新的 CSS 语法转换成大多数浏览器都能理解的语法，并根据你的目标浏览器或运行时环境来确定你需要的 polyfills，此功能基于 cssdb 实现。

>cssnano:缩减（minification）是指利用各种方法来 减少代码体积的过程。和 gzip 之类的保留 CSS 文件的原始语义（即无损失）的技术不同，缩减（minification） 天生是一个有损失的过程，例如，其中某些值可能会被替换为更简化的 等价语法，或者选择器被合并。

在app.vue中简单编辑
``` html
<style lang="less">
:fullscreen {
  color:red
}

</style>
```
运行`npm run build` 查看编译出来的文件:
```
:-webkit-full-screen {
    color: red
}

:-ms-fullscreen {
    color: red
}

:fullscreen {
    color: red
}
```
可以看到postcss插件中使用的autoprefixer插件已经生效



#### 2 在vuecli中使用babel

因为vuecli在生成文件时已经生成了babel.config.js,我们只要做一个简单的验证就行：
打开babel.config.js 把preset中的`"@vue/cli-plugin-babel/preset"`删除

在app.vue中写一个es6方法

``` javascript
export default {
  name: "App",
  components: {
    HelloWorld
  },
  mounted(){
    this.test()
  },
  methods:{
    test(){
      return ()=>{
        console.log(`我是es5`);
      }
    }
  }
};
</script>
```
执行`npm run build`
能找到这一段`methods:{test:function(){return function(){console.log("我是es5")}}}}` 可见箭头函数已经被转换成es5语法

