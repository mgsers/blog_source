---
title: shallowCopyAnddeepCopy
date: 2017-09-07 10:10:10
tags: javascript
---

## 深浅拷贝的区别

> 浅拷贝只负责对象的第一层键值的复制，而没有对更加深层键值对进行处理赋值
>
> 深拷贝则是对整个对象树进行遍历，对每一层的键值都进行复制，通常通过递归实现

### shallow copy

```javascript


let shallowCopy = (target, source) => {
  if (!source || typeof source !== 'object') return;

  if (!target || typeof target !== 'object') return;

  for (let key in source) {
    if (source.hasOwnproperty(key)) {
      target[key] = source[key]
    }
  }
}

// Object copy

Object.assign(obj, obj1)



// array copy

let arr = [1,2,3,5]
// 1. [].concat()
let arr2 = [].concat(arr)
// 2. arr.slice(0)
let arr3 = arr.slice(0)

```

### deep cope


```javascript

let deepClone = (obj) => {
  let copy
  if (!obj || typeof obj !== 'object') return obj;

  // Date
  if (obj instanceof Date) {
    copy = new Date()
    copy.setTime(obj.getTime())
    return copy;
  }

  // Array
  if (obj instanceof Array) {
    copy = []
    for (let i = 0; i < obj.length; i++){
      copy[i] = deepClone(obj[i])
    }
    return copy;
  }

  // Object
  if (obj instanceof Object) {
    copy = {}
    for (let i in obj) {
      if (obj.getOwnProperty(i)) {
        copy[i] = clone(obj[i])
      }
    }
    return copy;
  }

}

// simple way 

let obj2 = JSON.parse(JSON.stringify(obj))

```