---
title: 'vue-cli3.0 配置公共less文件'
date: 2020-04-24 17:29:56
tags: vue
categories: js
---

##### 本地安装 

> cnpm/npm i 
style-resources-loader 
vue-cli-plugin-style-resources-loader  
less  
less-loader -S

##### vue.config.js文件中的配置


```
pluginOptions: {
        'style-resources-loader': {
            preProcessor: 'less',
            patterns: [
                path.resolve(__dirname, './src/assets/less/enter.less')
            ]
        }
    }
```
注意：在公共less文件中的图片路径会有问题建议有图片路径的css 不要写在公共less文件中
