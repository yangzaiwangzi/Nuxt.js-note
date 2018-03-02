# Nuxt.js-note
最近刚刚学习了Nuxt.js框架，正好公司有个移动的项目要开发，于是决定使用Nuxt.js，进行开发，现将开发的过程记录下来。  
本文不是教程，如果是刚入门，建议先去官网学习。这里只是开发的随手笔记和一些踩坑的过程...，你在项目进行中，可能会有点帮助。  
如果写的有问题，欢迎 Issues 我！！！  
由于是公司项目，代码不方便开源，不好意思...

### 项目的搭建
1. 如果 vue-cli 没有安装, 需先通过 npm install -g vue-cli 来安装；
2. 打开cmd，输入一下命令行，一次一回车，‘<project-name>’是你项目的名称
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
host配置自己本地IP，如此，则可以使用 192.168.xx.xxx:3332 在浏览器代开项目。
