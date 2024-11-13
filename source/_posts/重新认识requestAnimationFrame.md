---
title: 重新认识requestAnimationFrame
date: 2024-11-13 10:42:17
categories: [javascript]
tags: [finished]
---

# 重新认识requestAnimationFrame

### 什么是requestAnimationFrame
一个api，在下次动画帧更新时执行

### 有什么用
在下一帧更新时执行一次，对动画、更新频率较高的dom比较友好

setTimeout、setInterval都是`定时`动画,频率太高，太消耗性能，频率太低，显示效果差

跟动画帧同步执行，频率正好，解决了`定时`动画不好确定更新时间的问题

核心思想：画面更新的时候，执行动画

### 错误思想
- 用来请求业务数据！
- 用来执行循环方法！

### 示例
鼠标移动时获取坐标
````javascript
const mouseEventData = {x: 0, Y: 0}
let requestFrameId: any = undefined
const updateMouseData = (event: MouseEvent) => {
  if(requestFrameId){
    cancelAnimationFrame(requestFrameId)
  }
  requestFrameId = requestAnimationFrame(() => {
    mouseEventData.x = event.clientX
    mouseEventData.y = event.clientY
  })
}

window.addEventListener('mousemove', (event) => {
  updateMouseData(event)
})
````

### 细节事项
`scroll`事件和`requestAnimationFrame`的触发频率是一致的