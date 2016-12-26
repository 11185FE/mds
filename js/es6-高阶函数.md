# ES6 - 高阶函数  
date: 2016-07-27 00:27:01  
tags: JavaScript,ES2015,函数式编程  

By gxh

-------

> 函数式编程 — 高阶函数

-------

昨天重温了一下 `Redux` 中间件的使用，在一篇文章中看到了 `Redux` 关于中间件的执行代码，这段代码使用了 N 多函数式编程思想👏👏，燃起了自己对函数式编程的渴望🔥🔥🔥，之后将会针对函数式编程做一系列的学习。（ 中间件代码解析直达（暂时未更） — [Redux applyMiddleware 解析]()）  

本文将学习如何使用 `ES6` 实现高阶函数。

### 何为高阶函数
首先让我们看一段高阶函数的写法：
```javascript
const f = (x) => return x + 1;
const g = (x) => return 2 * x;
const compose = (f, g) => x => f(g(x));
compose(f, g);
```

函数式编程是非常理论和非常数学化的，高阶函数转化为数学语言的话，我们可以将它看做为是一组复合函数：
```javascript
given:
  f(x) = x + 1
  g(x) = 2 * x

then:
  (f ∘ g)(x) = f(g(x)) = 2 * x + 1
```

由上面的例子我们可以看出，高阶函数是至少具有以下`两种功能之一`的函数：
* 使用一个或多个函数作为实参
* 返回一个函数作为结果

### 语法理解
下面我们将以一个简单的加法函数来进行 `ES6` 高阶函数的语法理解，例子在 `ES5` 中会这样写
```javascript
// ....
function add(x){
  return function(y){
     return y + x;
  };
}

add(10)(11); // 21
// ....
```
这个加法函数输入 `x`,返回了一个输入 `y` 返回 `y + x` 的函数，我们使用 `ES6` 将这么书写：
```javascript
const add = x => y => x + y;
// outer function: x => [inner function, uses x]
// inner function: y => y + x;
```
我们所写的加法函数并不是超级有用，但是它可以说明一个外函数如何输入一个以 `x` 为变量的参数函数，并在它返回的函数中引用此函数。

### 高阶函数实践
我们将以一个 `过滤方法` 来进行我们的高阶函数实践，核心代码如下:
```javascript
const has = p => o => o.hasOwnProperty(p);

let result;
let users = [
  {name:'Gxh'},
  {name:'Amu',pets:'FatDog'}
];

result = users.filter(has('pets')); // [{ name: 'Amu', pets: 'FatDog' }]
```

让我们来看一看，在无高阶函数情况下返回函数的表达方式：
```javascript
result = users.filter((x) => x.hasOwnProperty('pets'));
```

#### 为什么选择高阶函数
高阶函数的有效性出于以下几个原因：
* 减少了重复代码

```javascript
// 非高阶函数
result = users
  .filter((x) => x.hasOwnProperty(x))
  .filter((x) => x.hasOwnProperty(y))；

// 高阶函数
result = users
  .filter(has(x))
  .filter(has(y))；
```
* 简化了代码的可重用性

```javascript
const hasPets = has('pets');
const isPeople = has('name');

let people = users.filter(isPeople);
let petOwningWorkers = people.filter(hasPets);

// 实现单返回值
let user = {name:'Gu'};
hasPets(user); // false
isPeople(user); // true
```
* 上述的两段代码，在笔者看来，高阶函数能提升代码含义的清晰度，让逻辑更加清晰

#### 更进一步，高阶函数实践之 React HOC
理解了高阶函数的使用，我们便能进行下一步更高级的操作了，实现 `React` 的 `HOC(High Order Component)`
```javascript
// HOC 概念
hoc :: ReactComponent -> ReactComponent
// 它接受一个ReactComponent，并返回一个新的ReactComponent，可以用来对 React 组件进行改造
```
当我们写一个 `TodoApp` 时，我们有一个基础组件 `BaseTodoItem`，我们可以使用 `HOC` 对基础组件进行功能性封装
```javascript
// BaseTodoItem
function BaseTodoItem(props) {
  return {
    render() {
      return (
        <label> {props.content} < /label>
      );
    }
  };
}
```
功能封装函数 `HOC` ：
```javascript
// 添加完成按钮
function MakeCompletable(Child) {
  class Completable extends Component {
    render() {
      const {checked,onChange,...childProps} = this.props;
      return (
        <div>
          <input
            className = "toggle"
            type = "checkbox"
            checked = {checked}
            onChange = {onChange}
          />
          <Child {...childProps}/>
        </div>
      );
    }
  }
  return Completable;
}

// 添加删除按钮
function MakeDeletable(Child) {
  class Deletable extends Component {
    render() {
      const {onDelete,...otherProps} = this.props;
      return (
        <div>
          <Child {...otherProps}/>
          <button
            className = "delete-todo"
            onClick = {onDelete}/>
        </div>
      );
    }
  }
  return Deletable;
}
```
`HOC` 使用方式
```javascript
// 生成TodoItem
const CompletableItem = MakeCompletable(BaseTodoItem);
const DeletableItem = MakeDeletable(CompletableItem);

class TodoItem extends Component {
  render() {
    const { isCompleted, content } = this.props;
    const className = classNames({
      'is-completed': isCompleted
    });
    return (
      <li className={className}>
        <DeletableItem
          checked={isCompleted}
          content={content}
          onChange={this._onChange}
          onDelete={this._onDelete}
        />
      </li>
    );
  }
}
```
这几段代码其实并不复杂，我们可以这么理解，将基础组件 `BaseTodoItem` 看做一个函数，`HOC` 函数会对 `BaseTodoItem` 进行改造，在保持原有功能的情况下向其函数内部添加新的功能点，然后输出一个新的函数（ `ES7` 的 `修饰器` 也有类似的功能 — [ES7修饰器学习](https://github.com/gu-xionghong/iCoding/blob/master/2016/07/ES7修饰器学习.md)），这也便是高阶函数的思想要点了。  
利用高阶函数实现的 `HOC` 函数，能大大提高 `React` 组件的复用性，且高度自由的对任何组件进行自定义的改装方式，会让整个项目显得更加清晰，开发体验得到大幅度提升。

### 结束语
文章前半段主要是对 `ES6高阶函数` 的分析介绍，后半部分为 `React HOC` 的实现机制，可能是因为对高阶函数的使用并不是很熟悉，所以文章没有介绍更多关于 JS 使用高阶函数的场景，大家如果有更好的想法的话，还请多多交流~
