# Nuxt.js-note
最近刚刚学习了Nuxt.js框架，正好公司有个移动的项目要开发，于是决定使用Nuxt.js，进行开发，现将开发的过程记录下来。  
本文不是教程，如果是刚入门，建议先去官网学习。这里只是开发的随手笔记和一些踩坑的过程...，你在项目进行中，可能会有点帮助。  
如果写的有问题，欢迎 Issues 我！！！  
由于是公司项目，代码不方便开源，不好意思...

### 项目的搭建
1. 如果 vue-cli 没有安装, 需先通过 npm install -g vue-cli 来安装；
2. 打开cmd，输入一下命令行，一次一回车， <project-name> 是你项目的名称
```
vue init nuxt-community/starter-template <project-name>

cd <project-name>

npm install

npm run dev
```
浏览器打开localhost:3000,页面显示成功，cmd+浏览器控制台（console）没有报错,则项目基本架构搭建完成。
可能出现的问题：  
- 按照教程，但是会报错，请移驾nodeJs官网，升级nodeJs版本，在试一次；
- 浏览器使用本地IP:3000,无法打开，请继续往下看。
- 修改端口相关配置，如：希望使用本地IP:3332在浏览器打开项目  
打开 package.json 文件，添加如下代码：
```
  "config": {
    "nuxt": {
      "host": "192.168.xx.xxx",
      "port": "3332"
    }
  },
```
host配置自己本地IP，如此，则可以使用 192.168.xx.xxx:3332 在浏览器打开项目。

### 开始项目
#### 1. 路由
> Nuxt.js 依据 pages 目录结构自动生成 vue-router 模块的路由配置。
打开pages文件夹，修改里面的index.vue文件，这个文件就是你的项目首页。  
注意的问题：
- <template></template>标签中只能存在一个子节点，否则会报错：
```
The template root requires exactly one element  vue/valid-template-root //报错信息

//错误代码：
<template>
  <section></section>
  <section></section>
</template>

//代码修改
<template>
  <section></section> 
</template>

```
#### 2. 使用SCSS
 1. 安装依赖包 node-sass、sass-loader  
 2. 相应的组件中，修改代码如下：  
```
<style lang="scss" scoped>

...

</style>
```
    即可，在该组件编辑SCSS代码。其中，scoped 是设置<style></style>中编辑的样式只会影响该组件的样式。  
#### 3.移动端， 使用px自动转换rem  
  这次没有内置scss处理px自动转化rem，习惯使用插件cssrem-master，具体移驾:[cssrem](https://github.com/flashlizi/cssrem).
- 引入flexible.js  
 1. 引入方法一：每个组件页面添加如下代码，该方法则是每个组件页面都要加上这段代码，故不推荐。
 ```
<script> 
  export default {
    head(){
      return{
        script: [
          { src: 'flexible.js' }
        ] 
      }
    } 
  }
</script>
```
    
2. 引入方法二：使用NuxtJs提供的使用[组件Api](https://nuxtjs.org/guide/plugins)，相关步骤如下：
 ```
 //1、安装依赖包，教程链接【https://www.npmjs.com/package/flexible.js】，不多说。本人将该包代码结合flexible.js 做了一定的修改，方便自己使用，需要的可以Issues 我。
 //2、nuxt.config.js 添加代码
  plugins: [
    { src: '~/plugins/flexible.js', ssr: false }
  ]
//2、plugins文件夹添加文件flexible.js，并添加如下代码：
 import Vue from 'vue'
 import flexible from 'flexible.js'

 Vue.use(flexible); 
 ```
搭配好插件cssrem-master，即可  
#### 4.asyncData 方法
asyncData方法会在组件（**限于页面组件**）每次加载之前被调用。<br>
它可以在服务端或路由更新之前被调用。<br>
在这个方法被调用的时候，第一个参数被设定为当前页面的上下文对象，你可以利用 asyncData方法来获取数据，Nuxt.js 会将 asyncData 返回的数据融合组件 data 方法返回的数据一并返回给当前组件。<br>
这个方法也是nuxt实现SSR的关键一步。
#### 5.assets文件夹
默认情况下 Nuxt 使用 vue-loader、file-loader 以及 url-loader 这几个 Webpack 加载器来处理文件的加载和引用。<br>
对于不需要通过 Webpack 处理的静态资源文件，可以放置在 static 目录中。<br>
url-loader 能根据你指定的文件大小阈值，来判断一个文件是转换成内联的base-64码（如果该文件尺寸小于该阈值）还是使用file-loader来降级处理。小文件base-64化能有效减少HTTP请求数。也即文件（图片或字体）的尺寸小于1K（配置可修改）的时候，它将会被转换成 Base-64 data URL 来内联引用；
#### 常用命令
nuxt：	启动一个热加载的Web服务器（开发模式）。<br>
nuxt build：	利用webpack编译应用，压缩JS和CSS资源（发布用）。<br>
nuxt start：	以生成模式启动一个Web服务器 (nuxt build 会先被执行)。<br>
nuxt generate：	编译应用，并依据路由配置生成对应的HTML文件 (用于静态站点的部署)。<br>
Nuxt.js 提供了两种发布部署应用的方式：服务端渲染应用部署 和 静态应用部署。<br>
服务端渲染应用部署<br>
```javascript
nuxt build 
nuxt start 
```

静态应用部署
```javascript
npm run generate
```
