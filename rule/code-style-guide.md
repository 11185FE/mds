# Code Style Guide  
date: 2016-12-28
tags: rule  

By czl


## html

```html
<sample-shabee id="aB" class="a-b"></sample-shabee>
```

## js
```javascript
//vars, objects, functions, instances.
var thisIsMyVar = "";
const thisIsMyObject = {};
const sampleShabee = new SampleShabee();
function thisIsMyFunction() {}

//Constant names
const CONSTANT_CASE = 233;

//constructors, Enum, classes, singleton,compounent.
const StaticClass = {}
class SampleShabee {}
function SampleShabee(){};SampleShabee.protoype={}

```


## css
```less
//Do not use ID selectors
.sample-shabee

//OOCSS and BEM除外
```



## files

```javascript

//build
小写

//项目根目录
sample-shabee

//images
sample-shabee.jpg
sample-shabee.png
sample-shabee.gif
sample-shabee.svg


//其他仅选用一种
//ver1
//所有文件都用a-b
sample-shabee.html
shabee.js
sample-shabee.js
sample-shabee.css

//ver2
//命名方式和模块export返回的默认内容一致
thisIsMyObject.js
SampleShabbeeCompounent.js
SampleShabee.js
CONSTANT_CASE.js
```

