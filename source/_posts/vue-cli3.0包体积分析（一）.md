---
title: 'vue-cli3.0 包体分析（一）'
date: 2020-08-24 17:29:56
tags: vue
categories: js
---

vue-cli3.0 整体结构针对于vue2.0 优化了很多，相对的配置文件也只有一个vue.confing.js，在项目中我们难免会引入各种各样的组件，这样我们的构建的静态文件会越来越大。为了优化网页的加载速度，以及用户体验，我们就需要对一些特定的包体积较大的js进行优化，首先我们要有一个好的工具来分析我们的js由哪几部分组成。
##### webpack-bundle-analyzer
>这款工具可以可视化的输出webpack的输出文件的大小，及其组成部分（相当牛逼）此处盗个图
![海](https://img-blog.csdnimg.cn/20200707214636159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3l1YW5mYW5neW91c2hhbg==,size_16,color_FFFFFF,t_70)

那我们来开始安装它

```
 npm install webpack-bundle-analyzer --save -dev
```
vue.config.js 配置
```
 chainWebpack: config => {
        config
            .plugin('webpack-bundle-analyzer')
            .use(require('webpack-bundle-analyzer').BundleAnalyzerPlugin)
 }
```
然后执行 npm run build 访问http://localhost:8888/ 就可以看到我们的js的组成部分了，针对于想要的部分做出优化

>这里有一个问题 下次执行npm run build 的时候 要中止上一个服务，在不用的时候请将配置注释掉
