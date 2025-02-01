---
title: "Hyperapp - 麻雀雖小五臟俱全的微型前端框架"
seoTitle: "Hyperapp - 麻雀雖小五臟俱全的微型前端框架"
seoDescription: "快棄坑 React、Vue、Angular 吧～～疑？"
datePublished: Sat May 26 2018 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbf3kc000o0ajx03ymaykt
slug: hyperapp
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/banner/25238911.png
tags: framework, webpack, es6

---

快棄坑 React、Vue、Angular 吧～～疑？

在變化快速的前端戰場上，隨時都有萌新出現。

身為前端工程師的你，是否能夠「輕鬆駕馭」並且能夠「轉換自如」呢？

撇開框架後的你又剩下了什麼？

冒號上括弧。

**一、前言**
--------

最近在 github 的 Following 中看到 [hyperapp](https://hyperapp.js.org/)，

感覺很有趣，於是忍不住被抓走惹玩了幾天。

### **介紹框架**

**[Hyperapp](https://hyperapp.js.org/) ([github](https://github.com/hyperapp/hyperapp))**

[![25238911](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/25238911)](https://hyperapp.js.org/)

這是一套基於 ES6 的微型的前端框架，強調「**Minimal**」、「**Pragmatic**」、「**Standalone**」。

1 kB JavaScript framework for building web applications.

該怎麼說呢 ... 如果你使用過三大前端框架，

你會發現跟他們都很像，變來變去，其實都差不多。

Hyperapp 主要拆成三大塊：

*   **state**：資料的狀態，你可以想像成  [redux](https://github.com/reduxjs/redux) 的 [store](https://redux.js.org/api-reference/store) 或是 [model](https://davidkpiano.github.io/react-redux-form/docs/guides/models.html)
*   **actions**：各種事件方法等等，這跟 [vuex](https://vuex.vuejs.org/) 的 [action](https://vuex.vuejs.org/guide/actions.html) 很像
*   **view**：組件的組成，當然也是 [Virtual DOM](https://medium.com/@deathmood/how-to-write-your-own-virtual-dom-ee74acc13060)

官方範例程式（[try it online](https://codepen.io/jorgebucaran/pen/zNxZLP?editors=0010)）：

```javascript
import { h, app } from 'hyperapp'
```
```javascript
const state = {
  count: 0
}

const actions = {
  down: value => state => ({ count: state.count - value }),
  up: value => state => ({ count: state.count + value })
}

const view = (state, actions) => (
  <div>
    <h1>{state.count}</h1>
    <button onclick={() => actions.down(1)}>-</button>
    <button onclick={() => actions.up(1)}>+</button>
  </div>
)

app(state, actions, view, document.body)
```

### **環境準備**

hyperapp 目前十分**萌新**，尚未有所謂的 [boilerplate](https://github.com/explooosion/hyperapp-boilerplate)，官方也很歡迎各種的 [PR](https://github.com/hyperapp/awesome-hyperapp)。

要賺 PR 快趁現在（Ｘ

開發環境建議使用 ES6，因此可搭配 [webpack](https://webpack.js.org/) ，

如果你沒有個人常用基於 webpack 的樣板，可以試試使用 **[webpack-es6-boilerplate](https://github.com/explooosion/webpack-es6-boilerplate)，**

這是筆者修改來自 [＠](https://github.com/jluccisano/webpack-es6-boilerplate)[jluccisano](https://github.com/jluccisano) 的樣板專案，歡迎使用～

下載專案

```bash
git clone https://github.com/explooosion/webpack-es6-boilerplate.git
```

安裝套件

```javascript
yarn install
// or
npm install
```

啟動專案

```javascript
yarn start
// or
npm start
```

瀏覽網頁

[http://localhost:9000/](http://localhost:9000/)

![1527271714_28495.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527271714_28495.png)

### **編輯器準備**

由於使用 [JSX](https://facebook.github.io/jsx/)，如果你是使用 [Visual Studio Code](https://code.visualstudio.com/)，

建議安裝 [Babel ES6/ES7](https://marketplace.visualstudio.com/items?itemName=dzannotti.vscode-babel-coloring)，然後將語言模式選擇為：JavaScript React

[![1527273374_44246.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527273374_44246.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/d69575da-a85d-4a1d-ad9e-7dadde93e270/1527273374_44246.png)

然後你的 file icon 有很高機率變成 react 的形狀 ...

![1527273507_64704.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527273507_64704.png)

**二、Hello World - [codepen](https://codepen.io/ta7382/pen/BxgXgY?editors=1010)**
--------------------------------------------------------------------------------

接下來一起把專案變成 hyperapp 的形狀吧！！

由於筆者已經是 [yarn](https://yarnpkg.com/zh-Hans/) 的形狀，因此以下 npm 指令請自行腦內轉換。

首先安裝 hyperapp 以及 jsx 的轉換工具 babel-plugin-transform-react-jsx

```bash
yarn add hyperapp -S
```
```bash
yarn add babel-plugin-transform-react-jsx -S
```

［[.babelrc](https://github.com/explooosion/hyperapp-boilerplate/blob/master/.babelrc)］

引入 jsx 的編譯套件

```json
{
  "presets": ["env", "es2015", "stage-0"],
  "plugins": [
    ["transform-react-jsx", {
      "pragma": "h"
    }]
  ]
}
```

［index.js］

請清空檔案內容然後引入 hyperapp。

```javascript
import { h, app } from 'hyperapp'
```

在 hyperapp 中，組件 entry point 需綁入 state﹑actions﹑view，

因此我們先任意給變數讓他綁進去。

```javascript
const state = {}
const actions = {}
const view = (state, actions) => (
    <div>
        <h1>Hello World</h1>
    </div>
)
```

接著我們將 entry point 指定到 id 為 app 的元素上：

```javascript
app(state, actions, view, document.querySelector('#app'))
```

［index.html］

別忘了在 html 中新增一個 id 為 app 的元素，否則就綁定不到了：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Webpack ES6 Boilerplate</title>
</head>

<body>
  <div id="app"></div>
</body>

</html>
```

這時候啟動專案

```bash
yarn start
```

就可以看到 Hello World 嚕！

![1527274406_96322.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527274406_96322.png)

**三、組件剖析**
----------

### **View**

view 負責組件的視圖，各種即將要渲染的元素，

你可能會覺得，這個寫法很眼熟 ...

［index.js］

```javascript
const view = (state, actions) => (
    <div>
        <h1>Hello World</h1>
    </div>
)
```

其實也可以寫成：

```javascript
const view = (state, actions) => {
    return (
        <div>
            <h1>Hello World</h1>
        </div>
    )
}
```

更可以寫成：

```javascript
const view = function fn(state, actions) {
    return (
        <div>
            <h1>Hello World</h1>
        </div>
    )
}
```

或是省略 function name：

```javascript
const view = function (state, actions) {
    return (
        <div>
            <h1>Hello World</h1>
        </div>
    )
}
```

警告：您寫的是 hyperapp 而不是 vue、react、angular。

而前面的 state 跟 actions 就是傳入的值，

分別存放變數的狀態與事件。

### **State - [codepen](https://codepen.io/ta7382/pen/ZogzzN)**

state 主要儲存各種變數，狀態等等。

［index.js］

比如我們初始一個變數 name 內容為 hyperapp

```javascript
const state = {
    name: 'hyperapp',
}
```

然後在 view 中取出顯示：

```javascript
const view = (state, actions) => (
    <div>
        <h1>Hello World - {state.name}</h1>
    </div>
)
```

這時候就可以看到畫面多了 hyperapp。

![1527275302_59477.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527275302_59477.png)

### **Actions - [codepen](https://codepen.io/ta7382/pen/dexbPO)**

actions 儲存各種方法事件等，以提供我們調用，

［index.js］

例如我們定義一個按鈕的 click 事件：greet

```javascript
const actions = {
    greet: () => alert('hi')
}
```

然後在 view 中補上按鈕，而 onclick 就是原生的事件，

*   你並不需要寫什麼 onClick（React）、v-on:click（Vue）、(click)（Angular）等等之類  
    （**戰框架 77777**

```javascript
const view = (state, actions) => (
    <div>
        <h1>Hello World - {state.name}</h1>
        <button type="button" onclick={actions.greet}>Greet</button>
    </div>
)
```

試著按按鈕就會噴訊息了！

![1527276089_63666.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527276089_63666.png)

補充一下，在 hyperapp 中，大量使用[匿名函式](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Functions)哦！

因此其實展開後如下，其實跟 [vue - method event](https://vuejs.org/v2/guide/events.html) 是一樣的：

```javascript
const actions = {
    greet: function () {
        alert('hi')
    }
}
```

### **實戰練習 : 按鈕事件 Actions 改變 State - [codepen](https://codepen.io/ta7382/pen/vjoBOZ)**

［index.js］

如果你想要在按鈕的事件中，更改 state 的值，可以這麼做：

```javascript
const actions = {
    greet: state => ({ name: 'hehe' })
}
```

在每個 actions 中，皆可以將 state 傳入，然後返回新的 state，

而原本的展開式如下：

```javascript
const actions = {
    greet: function (state) {
        return ({ name: 'hehe' })
    }
}
```

### **實戰練習 : 文字輸入事件 Actions 改變 State - [codepen](https://codepen.io/ta7382/pen/zjgOvx)**

［index.js］

如果希望當我們輸入文字的時候，改變 state，可以這麼做：

```javascript
const actions = {
    greet: state => ({ name: 'hehe' }),
    update: name => state => ({ name: name })
}

const view = (state, actions) => (
    <div>
        <h1>Hello World - {state.name}</h1>
        <button type="button" onclick={actions.greet}>Greet</button>
        <input type="text"
            value={state.name}
            oninput={e => actions.update(e.target.value)}
        />
    </div>
)
```

看一下瀏覽器，輸入點什麼給他看看～

[![1527277751_53944.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527277751_53944.gif)](https://dotblogsfile.blob.core.windows.net/user/incredible/d69575da-a85d-4a1d-ad9e-7dadde93e270/1527277751_53944.gif)

我們利用 oninput 去觸發輸入時的事件 actions.update，

而 oninput 是 hyperapp 所提供的，

在 update 事件中，其實用了兩次 return，原本的展開式如下：

```javascript
const actions = {
    greet: state => ({ name: 'hehe' }),
    // update: name => state => ({ name: name })
    update: function fn(name) {
        return function fn(state) {
            return ({ name: name })
        }
    }
}
```

看出來了嗎～ 所以其實傳遞進去的變數 name 是可以更改命名的，例如：myvalue。

```javascript
const actions = {
    greet: state => ({ name: 'hehe' }),
    update: myvalue => state => ({ name: myvalue })
}
```

### **實戰練習 : 解構賦值(**Destructuring Assignment**) - [codepen](https://codepen.io/ta7382/pen/RyXbrZ)**

這個在 React 中很常用到，同為 JSX 的 hyperapp 也當然如此，

如果讀者不熟悉，我們可以來練習試試看。

［index.js］

這個範例建立姓名與訊息變數在 state 中，

並且在按鈕觸發的時候將文字更新到變數中。

```javascript
const state = {
    name: '',
    message: '',
}

const actions = {
    set: ({ name, msg }) => state => ({ name: name, message: msg })
}

const view = (state, actions) => (
    <div>
        <h1>Hello World</h1>
        <h2>{state.message} {state.name}</h2>
        <button type="button"
            onclick={() => actions.set({
                name: 'Robby',
                msg: 'Hi'
            })}
        >Set</button>
    </div>
)
```

畫面如下：

![1527279129_19098.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-05-26_Hyperapp%20-%20%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8%E7%9A%84%E5%BE%AE%E5%9E%8B%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6/1527279129_19098.gif)

在這邊可以發現，在 set 事件中，傳入了兩個參數，

在這邊利用解構的方式 ({ name, msg })　將參數取出，

如果不使用解構的方式，則需要寫成：

```javascript
const actions = {
    set: props => state => ({ name: props.name, message: props.msg })
}
```

超級展開後如下：

```javascript
const actions = {
    // set: props => state => ({ name: props.name, message: props.msg })
    set: function fn(props) {
        return function fn(state) {
            return ({
                name: props.name,
                message: props.msg,
            })
        }
    }
}
```

或是：

```javascript
const actions = {
    // set: props => state => ({ name: props.name, message: props.msg })
    set: function (props) {
        return function (state) {
            return ({
                name: props.name,
                message: props.msg,
            })
        }
    }
}
```

好！到這我想大家都亂了（Ｘ

這篇就先講到這，如果有興趣，

也可以看看筆者基於 hyperapp 所做出來的 boilerplate 以及 dashboard 展示：

*   ### **[hyperapp-boilerplate](https://github.com/explooosion/hyperapp-boilerplate)**
    
*   ### **[hyperapp-dashboard](https://github.com/explooosion/hyperapp-dashboard)**
    

如果你有看到 Vue 或 React 或 Angular 的影子，切記，那是假象！

有勘誤之處，不吝指教。ob'\_'ov