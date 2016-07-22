# react-native-resource
react native相关资料

## 第三方库

### UI组件
1.一个带渐变背景颜色的View https://github.com/brentvatne/react-native-linear-gradient


## 环境
**集成React Native 到现有iOS工程**

### 第一种方式(使用Cocopods)

1. 在项目根目录创建`package.json`文件,说明npm的依赖
`{
  "name": "drivercommunity",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "react-native start"
  },
  "dependencies": {
    "react": "15.2.1",
    "react-native": "0.29.2"
  }
}`
2. 通过 `npm install` 安装依赖包
3. 通过Cocoapods来从本地安装React Native, podfile文件添加`pod 'React', :path => './node_modules/react-native', :subspecs => [
'Core', // 这些是需要使用的模块,可选
'ART',
'RCTActionSheet',
'RCTAdSupport',
'RCTGeolocation',
'RCTImage',
'RCTNetwork',
'RCTPushNotification',
'RCTSettings',
'RCTText',
'RCTVibration',
'RCTWebSocket',
'RCTLinkingIOS',
]`
4. 需要添加RN的第三方库:先使用npm安装,然后找到相应的podspec安装(也可以使用rnpm安装).

### 第二种方式(使用工程依赖方式)
1. 手动添加依赖工程project到主工程
2. 添加Link Library
3. 添加 Header Search Path
4. 使用rnpm来添加第三次组件


## 方法
1. **将Native类导出**
	- 实现协议`RCTBridgeModule`(在类`RCTBridgeModule`中)
	- 通过宏`RCT_EXPORT_MODULE(js_name)`导出native类,`js_name`传空的时候默认为native类名
	- 通过`RCT_EXPORT_METHOD(method)`导出方法,或者使用`RCT_REMAP_METHOD(js_name, method)`导出方法并设置JS调用的方法名
	- JS端引用模块`var HW = require('react-native').NativeModules.HelloWorld;`
	
2. **dddd**
	- 但是

## 问题
- 使用`class MyProject extends Component`方法创建的类,不能使用`getInitialState`方法,需要替换为`constructor(props) {}`方法
- ES5 和 ES6 语法对照 [这里](http://bbs.reactnative.cn/topic/15/react-react-native-%E7%9A%84es5-es6%E5%86%99%E6%B3%95%E5%AF%B9%E7%85%A7%E8%A1%A8)
- 导出一个js模块,ES6写法 `export default class XXX extends Component {}`或者 `export default XXX;`, ES5写法 `modele.exports = XXX;`
- ES6取消了自动绑定`this`的功能,有两种方式可以绑定:第一,需要在 `constructor`方法手动给需要使用`this`的方法做绑定,比如:`this.方法名 = this.方法名.bind(this)`.第二,方法使用箭头函数声明函数,这样可以共享`this`变量,比如:`myfun - (para) => {}`,可以参考[这里](http://babeljs.io/blog/2015/06/07/react-on-es6-plus)
- `TouchableHighlight`组件使用,必须实现至少一个press相关函数才能有点击效果
- 通过`ref`属性获取组件的引用,有两种方式:第一种使用回调函数方式(推荐)`<View ref={(componentRef)=>{do something... like save ref }} />`,第二种使用字符串`<View ref='componentRef' />`,调用全局变量`this.refs.componentRef`来使用引用.


## React

### 初始化阶段生命周期函数
- getDefaultProps: 不同实例只有第一次被调用,实例之间共享引用
- getInitialState: 初始化每个实例特有的状态
- componentWillMount: render之前最后一次修改状态的机会
- render:只能访问 this.props 和 this.state, 只有一个顶层组件,不能返回多个组件,不允许修改状态和DOM输出.
- componentDidMount:成功render并渲染完成真实的DOM之后触发,可以修改DOM

### 运行阶段生命周期函数
- componentWillReceiveProps: 父组件修改属性触发,可以修改新属性,修改状态
- shouldComponentUpdate: 返回false会阻止render调用
- componentWillUpdate: 不能修改属性和状态
- render: 只能访问 this.props 和 this.state, 只有一个顶层组件,不能返回多个组件,不允许修改状态和DOM输出.
- componentDidUpdate: 可以修改DOM

## 学习网站

- http://reactnative.cn/ reactnative中文网
- http://reactjs.cn/  react 中文网
