# Code Style Guide  
date: 2016-12-28
tags: rule  

By czl

## 1 编程规约
### 1.1 HTML规范
- 标签：使用BEM命名方式。  
- id：使用小驼峰命名。  
- class：使用BEM命名方式。
- 语义化。  

```HTML
<slider-page id="aB" class="a-b"></slider-page>
```
### 1.2 CSS规范
- 标签选择器：使用BEM命名方式。
- Class选择器：使用BEM命名方式。
- Id选择器：禁用。
- 顺序：文字系列-位置属性-大小-边距-背景-其他

```CSS
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


### 1.3 JS规范
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

## 2 工程规范
### 2.1 文件命名规范
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
### 2.2 文件必要信息
- 必须在工程根目录有README.md文件，内容包括项目名称、项目截止日期、项目最后修改日期、参与人员、进度信息。
### 2.3 代码提交规范
- 禁止提交项目源码无关文件,如npm错误日志、yarn.lock、编辑器特有文件、工程构建后文件dist
- 禁止提交node_modules