# Code Style Guide  
date: 2017-03-24
tags: rule  

By czl

## 1 排版规范
### 1.1 HTML排版规范
- 使用 4 个空格作为缩进。
- 文件应以“```<!DOCTYPE ......>```”首行顶格开始，推荐使用“```<!DOCTYPE html>```”。
- 必须申明文档的编码charset，且与文件本身编码保持一致，推荐使用UTF-8编码```<meta charset="utf-8"/>```
- 必须标明```<title>```
- 使用link将css文件引入，并置于head中
- 使用script将js文件引入，并置于body底部
- 每个块级元素必须另起一行
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta content="telephone=no" name="format-detection">
    <meta name="renderer" content="webkit">
    <meta http-equiv="X-UA-Compatible" content="IE=9,IE=10,IE=11,IE=edge,chrome=1">
    <meta name="description" content="中国邮政">
    <link rel="stylesheet" href="index.css">
    <title>中国邮政</title>
</head>

<body>
    <div class="sharelogo">
        <img src="~images/logo.png" alt="">
    </div>
    <div class="full-loading">
        <img src="~images/loading.svg" alt="">
    </div>
    <app></app>
    <script src="http://res.wx.qq.com/open/js/jweixin-1.2.0.js"></script>
</body>

</html>
```

### 1.2 CSS排版规范
- 使用 4 个空格作为缩进。
- 类名使用破折号代替驼峰法。
- 不要使用 ID 选择器。
- 在一个规则声明中应用了多个选择器时，每个选择器独占一行。
- 在规则声明的左大括号 `{` 前加上一个空格。
- 在属性的冒号 `:` 后面加上一个空格，前面不加空格。
- 规则声明的右大括号 `}` 独占一行。
- 规则声明之间用空行分隔开。

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```


### 1.3 JS排版规范
- 使用大括号包裹所有多行代码块
```javascript
if (test) return false;

if (test) {
    return false;
}
```

-  如果通过 `if` 和 `else` 使用多行代码块，把 `else` 放在 `if` 代码块关闭括号的同一行。
```javascript
if (test) {
    thing1();
    thing2();
} else {
    thing3();
}
```

- 使用 4 个空格作为缩进。
```javascript
function () {
∙∙··var name;
}
```

- 在大括号前放一个空格。

```javascript
function test() {
    console.log('test');
}
dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog'
});
```

- 在控制语句（`if`、`while` 等）的小括号前放一个空格。在函数调用及声明中，不在函数的参数列表前加空格。

```javascript
if (isJedi) {
    fight();
}
function fight() {
    console.log('Swooosh!');
}
```

- 使用空格把运算符隔开。
```javascript
var x = y + 5;
```

 - **使用分号。**

```javascript
// good
(function () {
    var name = 'Skywalker';
    return name;
})();

// good (防止函数在两个 IIFE 合并时被当成一个参数
;(function () {
    var name = 'Skywalker';
    return name;
})();
```

## 2 命名规范
### 2.1 HTML命名规范
- 标签：使用BEM命名方式。  
- id：使用小驼峰命名。  
- class：使用BEM命名方式。
- 语义化。  

```HTML
<slider-page id="aB" class="a-b"></slider-page>
```
### 2.2 CSS命名规范
- 标签选择器：使用BEM命名方式。
- Class选择器：使用BEM命名方式。
- Id选择器：禁用。
- 顺序：文字系列-位置属性-大小-边距-背景-其他

```css
.slider-page {
    font-size:2rem;
    position:absolute;
    z-index:1;
    top:2rem;
    left:2rem;
    float:left;
    display:flex;
    width:2rem;
    height:2rem;
    padding:2rem;
    margin:2rem;
    border:2rem black solid ;
    background:yellow;
    transition:all linear 0.2s;
    animation:fadeIn linear 0.2s;
}
```


### 2.3 JS命名规范
- 变量、对象、函数、实例：使用小驼峰命名方式。
- 常量：使用大写下划线命名方式，使用const定义。
- 类、枚举、单例对象、组件：使用大驼峰命名方式。
- 禁用无意义命名名称。

```javascript

//变量、对象、函数、实例
var thisIsMyVar = "";
const thisIsMyObject = {};
const sliderPage = new SliderPage();
function thisIsMyFunction() {}

//常量
const CONSTANT_CASE = 233;

//类、枚举、单例对象、组件
const Api = {}
class SliderPage {}
function SliderPage(){};SliderPage.protoype={}

//禁用无意义命名名称
var var1 = 233;

```

## 3 注释规范
### 3.1 HTML注释规范
- 对于单个内容多且复杂的HTML文件，应使用```<!--xxx/s--><!--xxx/e-->```对各个模块进行标记
```html
<!--module1/s-->
<div class="module1">
</div>
<!--module1/e-->
<!--module2/s-->
<div class="module2">
</div>
<!--module1/e-->
```

### 3.2 CSS注释规范
- 对于单个内容多且复杂的css源文件，应使用```/*xxx*/```对各个主要模块进行标记
```less
/*xx模块*/
.xx-module{
    width:23rem;
    .logo{
        display:flex;//use flex
    }
}
```


### 3.3 JS注释规范
- 参考使用[jsdoc](http://usejsdoc.org/)对复杂模块进行注释,应至少包含标题、参数、返回等信息
```javascript
/**
 * Build a Book
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 * @param {string} author - The author of the book.
 * @returns {Object} Book
 */
function Book(title, author) {
    return {title, author}
}
```




## 4 工程规范
### 4.1 文件命名规范
- 构建后的所有文件：使用BEM命名方式、根文件夹命名为dist。
- 工程根目录：使用BEM命名方式。
- 图片：使用BEM命名方式。
- html、css、js：全部使用BEM命名方式 或 根据模块返回内容一致。

```javascript
//build
dist/index.html
dist/js/index.js
dist/css/index.css
dist/images/say-yes.jpg

//工程根目录
wx-games

//图片
say-yes.jpg
say-yes.png
say-yes.gif
say-yes.svg


//js、css、html,仅选择一种命名方式
//1.所有文件都用BEM，建议vue项目使用
user-list.html
api.js
user-list.js
user-list.css

//2.命名方式和模块export返回的默认内容一致，建议react项目使用
thisIsMyObject.js
SliderTreeCompounent.js
Api.js
CONSTANT_CASE.js
```
### 4.2 文件必要信息
- 必须在工程根目录有README.md文件，内容包括项目名称、项目截止日期、项目最后修改日期、参与人员、进度信息。
### 4.3 代码提交规范
- 禁止提交项目源码无关文件,如npm错误日志、yarn.lock、编辑器特有文件、工程构建后文件dist
- 禁止提交node_modules