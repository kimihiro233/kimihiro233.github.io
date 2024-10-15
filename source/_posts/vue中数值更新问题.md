---
title: vue中数值更新问题
date: 2024-10-15 10:11:17
categories: [vue]
tags: [processing]
---

# vue中数值更新问题

在vue中父子组件传值可以使用prop,emit('update')

如果存在比较复杂的情况，比如prop传入一个对象，而子组件内需要对这个对象的值进行处理
就会出现问题。
假设有这样的数据, 

````javascript
locationIds: 'location1,location2'
````
被子组件处理成一个数组进行使用
````javascript
locationIds: ['location1','location2']
````

如果直接update到父组件，不符合数据更新原则，会导致组件异常，不同代码对数据处理的错误