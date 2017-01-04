---
title: React入门
date: 2016-12-30 09:26:56
tags:
---

by zy

---

>该笔记主要介绍一些React的基本知识

---

# 一、Hello，World

```
    <!DOCTYPE html>
    <html>
      <head>
        <script src="./build/react.js"></script>
        <script src="./build/react-dom.js"></script>
        <script src="./build/browser.min.js"></script>
      </head>
      <body>
        <div id="example"></div> 
        <script type="text/babel">

          ReactDOM.render(
            <h1>Hello,World!</h1>,
            document.getElementById('example')
          )
        </script>
      </body>
    </html>

```

以上代码引用了三个库：react.js(该库是React的核心库)、react-dom.js(该库提供与DOM相关的功能)、Brower.js(该库的作用是将JSX语法转为JavaScript语法)。

ReactDOM.render()是React的最基本方法，用于将模板转为HTML语言，并插入指定的DOM节点。

# 二、JSX语法

React允许HTML和JS混合写，其中以<span><</span>开头的以HTML规则解析，以\{开头的用js解析。

```
    var rows = ['John', 'Lily', 'Peter'];
      ReactDOM.render(
        <div>
          {
            rows.map(function(name,i){
              return <li key={i}>{name}</li>
            })
          }
        </div>,
        document.getElementById('example')
      )
```

ps:其中key=\{i\}用来标注唯一性，数组需要这样做；否则会报warning:Each child in an array or iterator should hava a unique "key" prop.

# 三、组件
React允许封装组件，然后可以像HTML标签一样使用，也可以任意加入属性。所有组件都必须有render方法，用户输出组件。

```
  var Component = React.createClass({
      render: function(){
        return (
          <div>Hello,world!</div>
        )
      }
    })
    ReactDOM.render(
      <Component />,
      document.getElementById('example')
    )
```

组件类的第一个字母<span style="color:red;">必须大写</span>，这很重要,它可能不会报错，但是一定会渲染的不对。组件类只能包含一个顶层标签，多个顶层标签会造成错误。其中class需要写成className，for需要写成htmlFor,这是因为class和for是JavaScript的保留字。

```
  var Component = React.createClass({
      render: function(){
        return (
          <div className="wrap">Hello,{this.props.name}</div>
        )
      }
    })
    ReactDOM.render(
      <Component name="Lily"/>,
      document.getElementById('example')
    )
```

组件的属性可以通过this.props获得。

# 四、this.props.children
this.props对象的属性与组件的属性是一一对应的，但是有一个例外，就是this.props.children属性。它表示组件的所有子节点。

```
  var Component = React.createClass({
      render: function(){
        return (
          <ul>
            {
              React.Children.map(this.props.children, function(child){
                return <li>{child}</li>;
              })
            }
          </ul>
        )
      }
    })
    ReactDOM.render(
      <Component>
        <span>span1</span>
        <span>span2</span>
        <span>span3</span>
      </Component>,
      document.getElementById('example')
    )
```

this.props.children的值有三种可能：如果当前组件没有子节点，它就是undefined.如果有一字子节点，它就是object,如果有多个子节点，数据类型就是array。React提供了React.Children来处理this.props.children.

# 五、PropTypes
组件的属性可以接受任意值、字符串、对象、函数等等都可以。有时可能需要一种机制来验证别人使用组件时提供的数据是否符合要求。这时PropTypes属性就起作用。

```
  var name = 123;
  var Component = React.createClass({
    propTypes: {
      name: React.PropTypes.string.isRequired,
    },
    render: function(){
      return (
        <div>hello,{this.props.name}</div>
      )
    }
  })
  ReactDOM.render(
    <Component name={name} />,
    document.getElementById('example')
  )
```

这个时候会报错，react.js:19287 Warning: Failed propType: Invalid prop `name` of type `number` supplied to `Component`, expected `string`.


# 六、获取真实的DOM节点
组件并不是真实的DOM节点，而是存在于内存之中的一种数据结构，叫做虚拟DOM，只有当它插入文档后才会变成真实的DOM。this.refs.[refName]返回一个真实的DOM节点，所以必须等虚拟DOM插入文档以后才能使用这个属性，否则会报错。

```
  var Component = React.createClass({
    handlerClick: function(){
      this.refs.focusText.value="11111111";
    },
    render: function(){
      return (
        <div>
          <input type="text" ref="focusText"/>
          <input type="button" value="click" onClick={this.handlerClick}/>
        </div>
      )
    }
  })
  ReactDOM.render(
    <Component />,
    document.getElementById('example')
  )
```

# 七、this.state
React提倡所有的数据都由父组件来管理，通过props的形式传递给子组件来处理，props是不可变的。但是组件是避免不了互动的，互动的数据则需要state来管理。一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染UI。

```
  var Component = React.createClass({
    getInitialState: function(){
      return ({
        value: '',
      });
    },

    handlerChange: function(value){
      this.setState({
        value: value,
      })
    },
    render: function(){
      return (
        <div>
          <SubComponent todo={this.handlerChange}/>
          <ShowBox value={this.state.value}/>
        </div>
      )
    }
  })

  var SubComponent = React.createClass({
    handleSubmit: function(e){
      e.preventDefault();
      var newValue = this.refs.focusText.value;
      this.props.todo(newValue);
      this.refs.focusText.value = '';
    },
    render: function(){
      return (
        <form onSubmit={this.handleSubmit}>
          <input type="text" ref="focusText"/>
        </form>
      )
    }
  });

  var ShowBox = React.createClass({
    render: function(){
      return (
        <div>{this.props.value}</div>
      )
    }
  })
  ReactDOM.render(
    <Component />,
    document.getElementById('example')
  )
```

getInitialState方法用于初始化数据状态，this.status用户获取属性，this.setState用于修改数据状态。数据状态每修改一次，UI重新渲染一遍。当需要对用户输入、服务器请求或者时间变化等作出响应，这是就需要使用State.要尝试把尽可能多的组件无状态化，这样做可以隔离state,把它放到最合理的地方，也能减少冗余，同时易于解释程序运作过程。

# 八、组件生命周期

## 实例化

### 首次实例化

* getDefaultProps
* getInitialState
* componentWillMount
* render
* componentDidMount

### 实例化完成后的更新

* getInitialState
* componentWillMount
* render
* componentDidMount

## 存在期

### 组件已存在时的状态改变

* componentWillReceiveProps
* shouldComponentUpdate
* componentWillUpdate
* render
* componentDidUpdate

## 销毁&清理期

* componentWillUnmount

详细说明请参考[文档](http://reactjs.cn/react/docs/component-specs.html).

