# CODE_STYLE

React Native 官方并未给出编码标准，结合实际开发特约定如下标准：

## 命名约定

- 文件夹和子文件夹的名称应始终以小写字母开头，并且属于该文件夹的文件始终以驼峰式大小写。
- 为了命名组件，我们遵循基于模式路径的组件命名，这包括根据组件相对于文件夹组件或 src 的相对路径来命名组件。基本上，位于： `components / common / Button.js`的组件将被命名为`Button.js`。组件名称应遵循驼峰式大小写。
- 当文件位于同名文件夹中时，我们无需重复该名称。这意味着`components / user / form / Form.js`将被命名为`UserForm`，而不是`UserFormForm`。
- 单个导入中包括所有控件，以分号属于同一模块。两次进口之间不应有空格。

```javascript
import {ScrollView, View, TouchableOpacity, KeyboardAvoidingView, ListView, AsyncStorage, Alert } from ‘react-native’;
```

- 应该将类名声明为文件名，这样在导入过程中将很容易并且可以保持标准声明。
- 对象和变量声明应始终使用驼峰式大小写语句。如果我们使用分号，那么请在语句末尾的所有位置使用或不使用。

```javascript
const textExample = “Hello World”;
// or
const textExample = “Hello World”
```

## 布局约定

- 始终以分号结束声明。
- 当我们必须使用状态时，我们应该创建类组件，否则应该使用功能组件。
- 不允许在 React 组件的`Render（）`上调用`setState（）`。
- 如果没有自动缩进连续行，则将其缩进一个制表位（四个空格）。
- 在方法和属性定义之间至少添加一个空白行。
- 相似外观的语句之间或相似代码段之间不应有行距适用于同一活动。、

```javascript
const {loading} = this.state;
const {label, scroll, dropdown, disabledLabel} = styles;
const datasources = this.buildDataSource();
// and
if (!this.state.isSelctionChange) {
  this.props.selectedIndex.punchIndex = 0;
  this.props.selectedIndex.jobIndex = 0;
}
```

- 将箭头函数定义为类实例，并且由于箭头函数没有自己的作用域，因此内部箭头函数将始终指向该类。因此，您不需要在内部构造函数中进行绑定。在大多数情况下，完全不需要使用构造函数。在我们的项目中，我们从未在任何组件中使用构造函数。

```javascript
// 优化前
class Button extends Component {
  constructor(props) {
    super(props);
    this.state = {clicked: false};
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({clicked: true});
  }
  render() {
    return <button onClick={this.handleClick}>Click Me!</button>;
  }
}

// 优化后
class Button extends Component {
  state = {clicked: false};
  handleClick = () => this.setState({clicked: true});
  render() {
    return <button onClick={this.handleClick}>Click Me!</button>;
  }
}
```

- 巧用解构。ES6 已经支持数组扩展运算符。您也可以对对象使用相同的语法。因此，我们无需直接编写`Object.assign（{}，a，{b：2}）`，而可以直接使用`{…a，b：2}`。它可以使您的 React 代码更加美观和简洁。让我向您展示使用传播运算符之前和之后的代码。

```javascript
const {loading} = this.state;
const {label, scroll, dropdown, disabledLabel} = styles;
const datasources = this.buildDataSource();
// and
if (!this.state.isSelctionChange) {
  this.props.selectedIndex.punchIndex = 0;
  this.props.selectedIndex.jobIndex = 0;
}
```

- 将箭头函数定义为类实例，并且由于箭头函数没有自己的作用域，因此内部箭头函数将始终指向该类。因此，您不需要在内部构造函数中进行绑定。在大多数情况下，完全不需要使用构造函数。在我们的项目中，我们从未在任何组件中使用构造函数。

```javascript
// 优化前
function todoApp(state = initialState, action) {
    switch (action.type) {
        case SET_VISIBILITY_FILTER:
            return Object.assign({}, state, {
            visibilityFilter: action.filter
            });
        default: return state;
    }
}
// 优化后
function todoApp(state = initialState, action) {
    switch (action.type) {
        case SET_VISIBILITY_FILTER:
            return { …state, visibilityFilter: action.filter };
        default: return state;
    }
}
```

- Refs：使用 ref 回调。它更具声明性。

```javascript
// 优化前
<Welcome ref=”myRef” />
// 优化后
<Welcome ref={(ref) => { this.myRef = ref; }} />
```

- 按需渲染：生命周期方法在重新渲染过程之前运行。当组件的属性或状态发生变化时，React 会将新值与渲染的值进行比较。当它们不相等时，React 将更新 DOM。默认情况下，它返回 true，由 React 进行更新。您可以使用`shouldComponentUpdate（nextProps，nextState）`并通过将 nextProps 与已渲染的（上一个）值进行比较来返回 false，以停止组件中所有子分支的重新渲染。当您不需要重新渲染组件时，它可以显着提高性能。

```javascript
shouldComponentUpdate(nextProps, nextState) {
    if (this.props.color !== nextProps.color) {
        // 通过使用不可变库，我们也可以避免对象的深度比较
        return true;
    }
    if (this.state.count !== nextState.count) {
        return true;
    }
    return false;
}
```

- 由于 React-native 支持 ES6，因此上述布局约定除外，因此我们可以使用所有 ES6 功能。

## 注释约定

- 将注释放在单独的行上，而不是在代码行的末尾。
- 以大写字母开始注释文本。
- 用句号结束 ​​ 注释文本。
- 在注释定界符（//）和注释文本之间插入一个空格。

## 语言准则

- 数据类型： ReactNative 中的变量可以包含任何数据。变量在某个时态可以是字符串，而另一时态可以是数字。

```javascript
// 不会报错
let message = “hello”;
message = 123456;
```

- 数字类型代表整数和浮点数。数字有很多操作，例如乘法\*，除法/，加法+，减法-等。

```javascript
let n = 123;
n = 123.123;
```

- 字符串： ReactNative 中 的字符串必须用引号引起来。

```javascript
let str = “Hello”;
let str2 = ‘Single quotes are ok too’;
let phrase = `can embed ${str}`;

// React Native中有三种类型的引号

// Double quotes: “Hello”.
// Single quotes: ‘Hello’.
// Backticks: `Hello`.
```

双引号和单引号是“简单”引号。在 ReactNative 中，它们之间没有区别。 反引号是“扩展功能”引号。它们允许我们通过将变量和表达式包装在\$ {…}中来将它们嵌入到字符串中，例如：

```javascript
let name = “John”;
// embed a variable
alert(`Hello, ${name}!`); // Hello, John!
// embed an expression
alert(`the result is ${1 + 2}`); // the result is 3
```

在其中放置任何内容：名称之类的变量或 1+ 2 之类的算术表达式或更复杂的内容。请注意，这只能在反引号中进行。其他引号没有此嵌入功能。

- 布尔值：布尔类型只有两个值 true 和 false。此类型通常用于存储`yes / no`值：true 表示“是，正确”，而 false 表示“否，不正确”。例如：

```javascript
let nameFieldChecked = true; // yes, name field is checked
let ageFieldChecked = false; // no, age field is not checked
```

布尔值也是比较的结果：

```javascript
let isGreater = 4 > 1;
alert(isGreater); // true (the comparison result is “yes”)
```

- 文字和属性：我们可以将一些属性作为“键：值”对放入{…}中：

```javascript
let user = { // an object
    name: “John”, // by key “name” store value “John”
    age: 30 // by key “age” store value 30
};
```

- 数组：创建空数组有两种语法,几乎总是使用第二种语法。我们可以在方括号中提供初始元素.数组元素从零开始编号，我们可以通过方括号中的数字获得元素.

```javascript
let arr = new Array();
let arr = [];

let fruits = [“Apple”, “Orange”, “Plum”];

let fruits = [“Apple”, “Orange”, “Plum”];
alert( fruits[0] ); // Apple
alert( fruits[1] ); // Orange
alert( fruits[2] ); // Plum
```

- prop: prop 是 Properties 的缩写。简单的经验法则是，不应更改道具。在编程世界中，我们称其为“Immutable”或简单的英语为“Unchangeable”。

```javascript
// 父组件
export default class ScreenOne extends React.Component {
    render() {
        return (
            <View>
            <Heading message={‘Custom Heading for Screen One’} />
            </View>
        )
    }
}
// 子组件
export default class Heading extends React.Component {
    render() {
        return (
            <View>
            <Text>{this.props.message}</Text>
            </View>
        )
}
}
Heading.propTypes = {
    message: PropTypes.string
}
Heading.defaultProps = {
    message: ‘Heading One’
}


```

- state： 与 props 相比，state 的工作方式有所不同。state 是组件内部的，而 props 则传递给组件。

```javascript
class Form extends React.Component {
    constructor(props) {
        super(props)
        this.state = {
            input: ‘’
        }
    }
    handleChangeInput = (text) => {
        this.setState({ input: text })
    }
    render() {
        const { input } = this.state
        return (
            <View>
            <TextInput style={{ height: 40, borderColor: ‘gray’, borderWidth: 1 }}
            onChangeText={this.handleChangeInput}
            value={input}
            />
            </View>
        )
    }
}
```
