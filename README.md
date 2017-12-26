车行易 H5键盘
---

## 引入键盘组件

### 通过CDN引入1.3.0版本的`css`和`js`

推荐通过CDN的方式引入键盘组件，因为这样在出现bug时统一修复。1.3.0版本的CDN键盘组件等同于通过`require`或`import引入`“~1.3.0”版本的键盘组件

```html
    <link type="text/css" rel="Stylesheet" href="//cx580.oss-cn-shenzhen.aliyuncs.com/cweb/js/cxy-keyboard-1.3.0/cxy-keyboard.css">
  <script src="//cx580.oss-cn-shenzhen.aliyuncs.com/cweb/js/cxy-keyboard-1.3.0/cxy-keyboard.js"></script>
```

### 通过require或import引入键盘组件

首先安装>=1.3.2版本的键盘组件,

```cmd
    npm install --save cxy-keyboard
```

组件是用es6写的，同时样式是通过import scss的方式引入的，所以引入键盘组件时，需要配置下webpack来实现scss的引入以及ES6的转码，这里就不一一细说

```js
    const cxyKeyboard = require('cxy-keyboard');
    // 或
    // import cxyKeyboard from 'cxy-keyboard';
```

## 常用方法：

- init
- show
- onChange
- switchKeyboard
- isShow

引入键盘js后，会存在一个全局键盘实例：`cxyKeyboard`，可通过`cxyKeyboard.init({...param})`来初始化键盘

## init

键盘初始化：`cxyKeyboard.init({...param})`

```js
cxyKeyboard.init({
    // 键盘Dom元素的Id 默认：cxyKeyboard
    domId: 'cxyKeyboard',

    // 输入框初始化
    inputs: [{
        // css选择器（不支持选input或textarea等输入标签，因为这些标签会调起系统键盘）
        selectors: '#id',

        // 无输入时的提示
        placeholder: '字母数字键盘',
        
        // 键盘的类型 默认：ABC（字母数字键盘）
        type: 'ABC',

        // 允许最大长度
        maxLength: 8,
    }]
});
```

## show

显示键盘：`cxyKeyboard.show({...param},isSwitch)`

```js
// 获取键盘的显示状态
var isShow = cxyKeyboard.isShow;

// input输入框的参数
var param = {
    selectors: '#id', // css选择器
    animation: !isShow, // 键盘不存在时则显示动画
}

// 显示键盘
cxyKeyboard.show(param, isShow);
```

## onChange

键盘输入的内容发生变化：`cxyKeyboard.onChange(value, {...param})`

```js
// 内容发生改变
cxyKeyboard.onChange = function (value, keyboardId) {
    console.log('键盘的内容：' + value);
    console.log('键盘的css选择器：' + keyboardId);
};
```

## switchKeyboard

切换键盘：`cxyKeyboard.onChange('URL')`

```js
// 切换键盘（继承当前输入框的所有内容）
cxyKeyboard.switchKeyboard('ABC');
```

## isShow

键盘处于显示键盘的标识符：`cxyKeyboard.isShow`

## 样式修改

要实现字体、行高、对齐等效果请直接在项目中重写对应的css类；

示例：

```css
.ys-keyboard-input{
    float: right; // 输入框右对齐
}
```

## 可监听的事件

- cxyKeyboard_show
- cxyKeyboard_hide
- cxyKeyboard_switchKeyboard
- cxyKeyboard_addValue
- cxyKeyboard_deleteValue

### cxyKeyboard_show

键盘显示事件：

```js
window.addEventListener('cxyKeyboard_show', function() {
    console.log('键盘显示了')
})
```

### cxyKeyboard_hide

键盘隐藏事件：

```js
window.addEventListener('cxyKeyboard_hide', function() {
    console.log('键盘隐藏了')
})
```

### cxyKeyboard_switchKeyboard

键盘切换事件：

```js
window.addEventListener('cxyKeyboard_switchKeyboard', function() {
    console.log('键盘切换了')
})
```

### cxyKeyboard_addValue

新增内容事件：

```js
window.addEventListener('cxyKeyboard_addValue', function() {
    console.log('新增内容了')
})
```

### cxyKeyboard_deleteValue

删除内容事件：

```js
window.addEventListener('cxyKeyboard_deleteValue', function() {
    console.log('删除内容了')
})
```