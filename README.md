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
1. 路由
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
2. 使用SCSS
    1. 安装依赖包 node-sass、sass-loader  
    2. 相应的组件中，修改代码如下：  
  ```
<style lang="scss" scoped>

...

</style>
  ```
    即可，在该组件编辑SCSS代码。其中，scoped 是设置<style></style>中编辑的样式只会影响该组件的样式。  
3.移动端， 使用px自动转换rem  
  这次没有内置scss处理px自动转化rem，习惯使用插件cssrem-master，具体移驾:[cssrem](https://github.com/flashlizi/cssrem).
    1. 引入flexible.js
        - 引入方法：
