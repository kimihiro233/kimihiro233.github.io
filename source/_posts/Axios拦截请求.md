---
title: Axios拦截请求
date: 2024-11-21 15:13:07
categories: [javascript, axios]
tags: [finished]
---

# Axios拦截请求

前端组件化之后，组件初始化请求数据，就会出现大量请求，比如人员选择器组件初始化查询人员列表，部门选择器组件初始化查询部门列表

## Axios怎么拦截请求

axios是带有拦截器的，但是他的拦截器，并不能阻断请求，并且返回正常数据，所以要满足要求，只能在request外面包一层方法

这里采用覆写request方法来处理，伪代码如下

```javascript
const request = axios.prototype.request
axios.prototype.request = function (config) {
    // 对有缓存的接口直接返回结果
    const cache_response = get_cache_response(config)
    if(cache_response) return Promise.resolve(cache_response)
    // 执行request
    const response = request(config)
    // 对需要缓存的接口缓存response
    cache_request(config, response)
}
```

> axios的执行逻辑是promise，发起后不能阻断会依次执行前置过滤器(request)-请求-后置过滤器(response)，只能返回错误结果
> 
> axios的request返回的是一个promise，内部是被拦截器处理过的response数据

## 处理并发请求
同一页面的组件，一般会同时进行初始化，这时候并没有一个被缓存的结果，所以需要对请求的promise进行截留，
根据config比如，相同时返回promise实例

```javascript
const request = axios.prototype.request
axios.prototype.request = function (config) {
    // 对有现成实例的请求，直接返回请求实例
    const response_instance = get_cache_response(config)
    if(response_instance) return response_instance
    // 执行request
    const response = request(config)
    // 对可能存在并发的接口保留实例
    store_promise_instance(config, response)
}

// 在实例完成后，移除保存的实例，保证下一次（非并发）发起的请求真正发起
response_promise.then(() => {
    clear_instance(key)
})
```