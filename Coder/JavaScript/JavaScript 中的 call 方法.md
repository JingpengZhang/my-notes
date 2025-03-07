---
title: JavaScript 中的 call 方法
catalog: 前端
tags:
  - JavaScript
  - 面试题
post_time: 2023-09-24 16:56:24
---

## `call` 方法介绍

语法：`Function.call(     thisArg: any,     ...argArray: any[]): any`

- Function - 调用者函数
- thisArg - `this` 指向的目标
- ...argArray：传入调用者函数的参数，非数组形式，数量任意


`call` 函数能够调用者函数中的 `this` 指向 `call` 函数的第一个参数，并将剩余任意数量的参数传入调用者函数，实现函数的复用。

## 使用示例

比如，有如下对象 `college`：
```javascript
const college = {  
	name: '清华大学',  
	logSomething: function (location) {  
		return console.log(this.name, '，坐落于：' + location + '。')  
	}  
}
```
该对象中包含一个属性 `name` 及一个方法 `logSomething`，该方法接受一个参数 `location`，调用该方法会打印一句话
```javascript
college.logSomething('北京')
// 打印结果：清华大学 ，坐落于：北京。
```

如果有另外一个对象 `college2`，该对象上仅有一个 `name` 属性，可以使用 `call` 函数实现调用 `college` 对象上的 `logSomething` 函数打印 `college2` 的信息。
```javascript
const college2 = {  
name: '武汉大学'  
}  
  
college.logSomething.call(college2, '武汉')
// 打印结果：武汉大学 ，坐落于：武汉。
```
在  `logSomething` 函数上调用 `call` 方法，并传入对象 `college2`，`call` 方法会将 `logSomething` 函数内部的 `this` 指向改为传入的 `college2`，此时，`this.name` 即代表 `college2.name`，同时，`call` 方法支持传入任意数量的参数，并传入到`logSomething` 函数中，实现`logSomething` 函数的复用。