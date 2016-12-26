---
title: DIY jQuery 系列学习 -- 01
date: 2016-08-25 14:23:55
tags: [jQuery]
---

By gxh

--------------------------------------------------------------------------------

> DIY jQuery 系列学习笔记 ---- 01，笔记将针对原文提到的知识点做理解拓展

--------------------------------------------------------------------------------

原文链接：[从零开始，DIY一个jQuery（1）](http://www.cnblogs.com/vajoy/p/5510743.html)

### 工厂模式 -- 免 new 实现

`工厂模式` 即是将 `new` 操作封装在库内，让每次调用 `$()` 时能自行在内部进行实例化操作，简单工厂模式实现如下：

```javascript
// ES5
let jQuery = function(selector) {...},
    jQuery.prototype = {version: 1};

// ES6
class jQuery {
  constructor(selector) {
    this.version = 1;
    ...
  }
}

let $ = function Factory(selector) {
  return new jQuery(selector);
}
```

上述的做法有个问题，就是不能在使用 `jQuery()` 来进行实例化操作

```javascript
// 死循环，调用栈会直接爆掉，大家可以尝试下~
jQuery = function (selector) {
  return new jQuery(selector);
};
```

优化写法，实例化一个 `this` 指向 `jQuery`上下文、原型指向 `jQuery` 原型的构造函数即可

```javascript
let $ = jQuery = function() {
  return new jQuery.init();
}

jQuery.prototype = {
  version: 1
};

// this 指向 jQuery 上下文
jQuery.init = function() {
  console.log(this);
}

// 原型指向 jQuery 原型
jQuery.init.prototype = jQuery.prototype;

// 因为 ES6 Class对象不能被复写且必须 new 实例化，所以暂时没有想到如何实现这串代码
```

### 链式操作
链式操作很容易理解，即在每个调用的方法后面返回自身 `this` 即可：

```javascript
// ES5
let jQuery = function() {};
jQuery.prototype = {
  version: 1,
  setVersion: function(num) {
    this.version = num;
    return this;
  },
  getVersion: function() {
    console.log(this.version);
    return this;
  }
}

// ES6
class jQuery {
  constructor() {
    this.version = 1;
  }
  setVersion(num) {
    this.version = num;
    return this;
  }
  getVersion() {
    console.log(this.version);
    return this;
  }
}

new jQuery().getVersion().setVersion(2).getVersion(); // 1 2
```

### END
第一部分笔记暂时这么多，干货不多，继续跟进学习该系列~
