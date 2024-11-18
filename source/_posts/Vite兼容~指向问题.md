---
title: Vite兼容~指向问题
date: 2024-11-18 15:04:30
categories: [vite, webpack, less]
tags: [finished]
---

# Vite兼容~指向问题

vite项目引入一些依赖项，其实less文件引入其它项目的文件，
如果原项目使用的是webpack，包名前面会有~别名

在vite项目中解决这个问题，是在resolve.alias中加入~开头的包名别名如

````javascript
export default defineConfig({
    // ....
    resolve: {
        alisas: {
            '~ant-design-vue': path.resolve(__dirname, 'node_modules/ant-design-vue')
        }
    }
    // ....
})
````

> 写这些内容的时候我是很愤怒的，愤怒自己不知变通，查了半天的资料