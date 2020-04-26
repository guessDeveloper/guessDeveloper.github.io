---
title: 'vue-cli3.0 配置autoprefixer css加兼容前缀'
date: 2020-04-24 17:29:56
tags: vue
categories: js
---

##### 本地安装 autoprefixer

> npm install autoprefixer -dev --save

##### package.json

```
browerslist: [
  "defaults",
  "> 1%",
  "last 2  versions",
  "not ie <= 8",
  "ios >= 7"
]

```


##### vue.config.js

```
const webpack = require('webpack');
const hostName = 'https://m.health.pingan.com';
const autoprefixer = require('autoprefixer')
module.exports = {
    lintOnSave: false,
    publicPath: process.env.VUE_BASE_URL || './',
    productionSourceMap: false,
    pages: {
        faq: {
            entry: 'src/main.js',
            template: 'public/faq.html',
            filename: 'faq.html',
        }
    },
    css: {
        loaderOptions: {
            postcss: {
                plugins: [autoprefixer({
                    overrideBrowserslist: ['ie >= 8', 'Firefox >= 20', 'Safari >= 5', 'Android >= 4', 'Ios >= 6', 'last 4 version'],
                    remove: true
                })],
                sourceMap: true
            }
        }
    },
    
    devServer: {
        open: true,
        port: 80,
        https: false,
        hotOnly: false,
        historyApiFallback: true,
        noInfo: true,
        overlay: true,
        proxy: {
            '/mapi/*': {
                target: hostName,
                secure: true,
                changeOrigin: true, //是否跨域
            },

            // 'secure': true, // 允许https请求
        },
        host: '0.0.0.0',
        before: appsvr => {}
    },
}
```