车行易 H5键盘
---

## 支持的键盘类型

- `number`：数组键盘
- `digit`：带小数点的数字键盘
- `idcard`：身份证键盘
- `ABC`：包含数字和字母（可切换到地区键盘）
- `carNumberPre`：车牌前缀键盘（地区键盘，可切换到ABC键盘）
- `url`：url键盘 小写字母+符号
- `URL`：URL键盘 大写字母+数字

## 引入键盘组件

### 通过CDN引入1.3.0版本的`css`和`js`

推荐通过CDN的方式引入键盘组件，因为这样在出现bug时统一修复。1.3.0版本的CDN键盘组件等同于通过`require`或`import引入`“~1.3.0”版本的键盘组件

```html
<link type="text/css" rel="Stylesheet" href="//oss.cx580.com/public_script/cxy-keyboard-1.3.0/cxy-keyboard.css">
<script src="//oss.cx580.com/public_script/cxy-keyboard-1.3.0/cxy-keyboard.js"></script>
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
- hide
- onChange
- switchKeyboard
- isShow
- inputs

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

        /** 
         * 排除的正则规则（下面的正式表示只允许输入一个小数点以及只允许小数点后两位）
         * 当输入的内容与排除规则匹配时，则输入的内容无效，输入框不会显示输入的非法内容
         */
        excludeRule: /\.{1}(\d*\.+|\d{3})/i,

        // 显示键盘上方的完成按钮
        showDoneBtn: true,
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

## hide

隐藏键盘：`cxyKeyboard.hide()`

```js
// 隐藏键盘
cxyKeyboard.hide();
```

## onChange

键盘输入的内容发生变化：`cxyKeyboard.onChange(value, activeId)`

```js
// 内容发生改变
cxyKeyboard.onChange = function (value, activeId) {
    console.log('键盘的内容：' + value);
    console.log('当前活跃输入框的css选择器：' + activeId);
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

## inputs

获取当前所有输入框的信息：`cxyKeyboard.inputs`

```js
// 获取某个输入框的内容 'selectors'表示输入框的css选择器
console.log(cxyKeyboard.inputs[selectors].value);
```

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
- cxyKeyboard_done

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

### cxyKeyboard_done

点击完成按钮

```js
window.addEventListener('cxyKeyboard_done', function() {
    console.log('点击了完成按钮')
})
```

## 技术文档

[点击查看更详细的文档说明](http://47.89.11.251/static/jsdoc/CxyKeyboard.html "jsdoc文档")

## 完整的demo

[点击查看demo](http://47.89.11.251/static/demo/CxyKeyboard.html "H5键盘demo")

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8" />
    <meta name="Cache-Control" content="private">
    <meta name="format-detection" content="telephone=no" />
    <meta name="viewport" content="minimum-scale=1, initial-scale=1, maximum-scale=1, user-scalable=no" />
    <title>H5键盘demo</title>
    <style>
        * {
            user-select: none;
            -webkit-tap-highlight-color: rgba(255, 0, 0, 0);
        }

        div {
            user-select: none;
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            -webkit-tap-highlight-color: rgba(255, 0, 0, 0);
            font-size: 16px;
        }

        .input {
            margin: 20px auto;
            width: 80%;
            padding: 2px;
            min-height: 20px;
            overflow: auto;
            word-break: break-all;
            border: 1px solid #000;
            font-size: 14px;
            line-height: 1.5;
        }
    </style>
</head>

<body>
    <div id="carNumberKeyboard" class="input" onclick="show('#carNumberKeyboard')"></div>
    <div id="numberKeyboard" class="input" onclick="show('#numberKeyboard')"></div>
    <div id="digitKeyboard" class="input" onclick="show('#digitKeyboard')"></div>
    <div id="idcardKeyboard" class="input" onclick="show('#idcardKeyboard')"></div>
    <div id="urlKeyboard" class="input" onclick="show('#urlKeyboard')"></div>
	
	<link type="text/css" rel="Stylesheet" href="//oss.cx580.com/public_script/cxy-keyboard-1.3.0/cxy-keyboard.css">
    <script src="//oss.cx580.com/public_script/cxy-keyboard-1.3.0/cxy-keyboard.js"></script>
    <script>
        // 根据屏幕宽度自动设置页面的字体大小
        !function (n, e) {
            var t = n.documentElement, i = "orientationchange" in window ? "orientationchange" : "resize", d = function () {
                var n = t.clientWidth;
                if (n) {
                    var e = 50 * (n / 375);
                    e = e > 54 ? 54 : e;
                    t.style.fontSize = e + "px";
                    var s = getComputedStyle ? getComputedStyle(t, false)['fontSize'] : '';
                    s = (s.substr(0, s.length - 2)) * 1;
                    if (s && e !== s) {
                        t.style.fontSize = e * (e / s) + "px";
                    }
                }
            };
            n.addEventListener && (e.addEventListener(i, d, !1), n.addEventListener("DOMContentLoaded", d, !1))
        }(document, window);

        // 实例化键盘
        window.cxyKeyboard.init({
            inputs: [{
                selectors: '#carNumberKeyboard',
                placeholder: '车牌号码键盘(有完成按钮，限制了长度为8，且选择车牌前缀后自动切换成字母键盘，只自动切换一次)',
                type: 'carNumberPre',
                maxLength: 8,
                showDoneBtn: true,
            }, {
                selectors: '#numberKeyboard',
                placeholder: '数字键盘（限制了长度为11）',
                type: 'number',
                value: '13800000000',
                maxLength: 11,
            }, {
                selectors: '#digitKeyboard',
                placeholder: '带小数点的数字键盘（只允许小数点后两位，有完成按钮）',
                type: 'digit',
                excludeRule: /\.{1}(\d*\.+|\d{3})/i, // 只允许一位小数点 并且只允许小数点后两位
                showDoneBtn: true,
            }, {
                selectors: '#idcardKeyboard',
                placeholder: '身份证输入键盘',
                type: 'idcard',
            }, {
                selectors: '#urlKeyboard',
                placeholder: 'URL键盘（限制长度为100，有完成按钮）',
                type: 'url',
                maxLength: 100,
                showDoneBtn: true,
            }]
        });

        // 内容发生改变
        cxyKeyboard.onChange = function (value, activeId) {
            if (activeId === '#carNumberKeyboard') {
                if (!window.autoSwitchKeyboard) {
                    window.autoSwitchKeyboard = true; // 只自动帮用户切换一次键盘
                    if (value.length === 1) {
                        // 自动切换成字母键盘
                        cxyKeyboard.switchKeyboard('ABC');
                    }
                }
            }

            console.log('当前所有输入框的详细信息：', cxyKeyboard.inputs);
        };

        function show(id) {
            var isShow = cxyKeyboard.isShow;
            var param = {
                selectors: id,
                animation: !isShow, // 键盘不存在时则显示动画
            }

            // 键盘如果存在，则切换键盘。不存在则显示键盘
            cxyKeyboard.show(param, isShow);
        }
    </script>
</body>

</html>
```