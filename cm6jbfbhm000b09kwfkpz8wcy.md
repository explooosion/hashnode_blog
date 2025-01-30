---
title: "React.js - 太弱的我，把 Hooks 點滿就對了"
seoTitle: "React.js - 太弱的我，把 Hooks 點滿就對了"
seoDescription: "都 2020 年了，還不趕快用 Hooks 參加勾肥大戰？"
datePublished: Fri Jan 10 2020 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbfbhm000b09kwfkpz8wcy
slug: reactjs-hooks
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/banner/bg2019083104.jpg
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/banner/bg2019083104.jpg
tags: hooks

---

都 2020 年了，還不趕快用 Hooks 參加勾肥大戰？

React 在 16.8 版之後納入 Hook 的功能。

[![bg2019083104.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/bg2019083104.jpg)](https://www.wangbase.com/blogimg/asset/201908/bg2019083104.jpg)

*   ref：[阮一峰 - React Hooks 入门教程](https://www.ruanyifeng.com/blog/2019/09/react-hooks.html)

前言
--

去年還在研究所打混，經過老闆再三囑咐。對於額外技術也暫時停止學習。

身為一位學術研究員，不專注於非研究領域的程式發展，也很合邏輯 QQ。

目前 CRA ( [create-react-app](https://create-react-app.dev/docs/getting-started/) ) 所使用的版號，也來到 16.12.0，

學習永遠不嫌遲，趁著一年國軍 online，趕緊補一下！

本篇文章僅簡單介紹、筆記，建議大家可以閱讀：

1.  [React 介紹 Hook](https://zh-hant.reactjs.org/docs/hooks-intro.html)
2.  [阮一峰 - React Hooks 入门教程](https://www.ruanyifeng.com/blog/2019/09/react-hooks.html)

1\. Hooks 介紹
------------

React 在 2019 年 2 月 [Release v16.8.0](https://github.com/facebook/react/releases/tag/v16.8.0)，

該版本推出了 Hooks ，鉤子 (？

可以讓我們在 functional component 進行一些 state 的控管。

儘管 Angular 已經來到 8.3 ...

儘管 Vue 已經來到 2.6 ...

但 Hooks 的名詞，勢必會影響不少生態圈（Ｘ

> _春秋百家爭鳴 大家抄來抄去 到底誰有道理 誰的比較高明_

你知道嗎？Hooks 其實就是希望能像鉤子一樣，可以隨手勾取所需工具、物品。

2\. Functional Component
------------------------

建議讀者可以直接拿官方的專案建置練習：[create-react-app](https://github.com/facebook/create-react-app)

在使用之前， Hooks 都是建構在 functional component 上，

因此建議至少先看過長什麼樣子：

```javascript
import React from 'react';

function App() {
  return (
    <div>
      Hello React With Hooks
    </div>
  );
}

export default App;
```

當然你也可以選擇使用 ES6 的 const 進行 arrow function 宣告：

```javascript
import React from 'react';

const App = () => {
  return (
    <div>
      Hello React With Hooks
    </div>
  );
}

export default App;
```

注意！ 好你現在看過了，可以繼續看下去囉！

3\. Hooks 鉤鉤種類
--------------

React 的 Hooks 基本上常見的包含：

*   useState
*   useContext
*   useReducer ( 本篇不介紹，不是懶，是忙投票 )
*   useEffect ( 本篇不介紹，不是懶，是忙投票 )

### useState

跟 setState 是同樣意思的，useState 內直接放入初始值即可。

返回陣列的第一個為當前值，第二個 setUser 則是用於設定。

```javascript
import React, { useState } from 'react';

function App() {

  const [user, setUser] = useState('Anonymous');

  return (
    <div>
      <h1 onClick={() => setUser('Robby')}>
        Hi,
        <small>{user}</small>
      </h1>
    </div>
  );
}

export default App;
```

你知道嗎？設定值的變數名稱，以最佳實踐來說，大多使用 setUser, setData 等，駝峰式的命名。

### useContext

如果我們要從父組件傳值給子子孫孫等組件，通常要 props 很多層，

而你的專案可能又包了一堆 HOC，例如：

```javascript
export default withTranslation()(connect(mapStateToProps)(Todo));
```

嚴重時會破壞你的結構，大 guy 會變成下麵這葛樣子， ( 俗稱 **Wrapper Hell** )：

[![DoD6dSSVAAAvdkO](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/DoD6dSSVAAAvdkO)](https://pbs.twimg.com/media/DoD6dSSVAAAvdkO?format=jpg&name=4096x4096)

*   Ref: [https://twitter.com/GrexQL/status/1045110734550589441](https://twitter.com/GrexQL/status/1045110734550589441)

如今！！！

只要你會丟出鉤子，稍微彎拉一下...

[![1578899498_3868.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/1578899498_3868.gif)](http://war3nobu.wltw.org/champion1)

[![1578899530_4571.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/1578899530_4571.gif)](http://war3nobu.wltw.org/champion1)

*   [信長之野望資訊站 - WL](http://war3nobu.wltw.org/cp_b01)

就能實現並解決這葛垢病！

請搭配著下方 createContext 章節閱讀。

### createContext

在使用 useContext 之前，要先認識 createContext，它是用來創建 Context 的 Provider 。

Context ？？？ 

Provider ？？？

以下使用常見的套件來比喻：

1.  react-redux 的 Provider
2.  styled-components 的 ThemeProvider 

如果這比喻不太明白，簡單說就是要從頂部灌水泥，灌資料下去喇 QQ

筆者簡單舉例父子組件傳遞值範例：

```javascript
import React from 'react';

const name = 'Robby';

function App() {

  return (
    <div>
      <User name={name} />
    </div>
  );
}

function User(props) {
  return (
    <div>{props.name}</div>
  );
}

export default App;
```

現在將試著使用 createContex 改寫看看：

引入 createContex，宣告變數 UserContext，其參數就是初始值。

```javascript
import React, { createContext } from 'react';

const name = 'Robby';

const UserContext = createContext(name);
```

接著於父子組件中使用：

在 UserContext 中，提供了 Provider 以及 Consumer，

1.  Provider：用於父層，並利用 value，來塞入指定的初始值。
2.  Consumer：顧名思義，就是用於接收子組件，內容為回傳一個 function。

請務必命名為 value，不可為其他屬性名稱。

```javascript
function App() {
  return (
    <UserContext.Provider value={name}>
      <User />
    </UserContext.Provider>
  );
}

function User() {
  return (
    <UserContext.Consumer>
      {name => name}
    </UserContext.Consumer>
  );
}
```

*   Provider 內需放入一個指定的 component，因此這邊建立一個 User 組件。
*   Consumer 內需放入一個 function，因此這邊使用一個簡易的 arrow function，

過度謹慎的你可能會想改寫...

[![1578706954_85843.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/1578706954_85843.png)](https://zh.wikipedia.org/zh-tw/%E9%80%99%E5%80%8B%E5%8B%87%E8%80%85%E6%98%8E%E6%98%8E%E8%B6%85TUEEE%E5%8D%BB%E9%81%8E%E5%BA%A6%E8%AC%B9%E6%85%8E)

沒錯，你也可以拉出來再寫一個 const arrow function。

```javascript
function User() {

  const renderName = name => {
    return name;
  }

  return (
    <UserContext.Consumer>
      {renderName}
    </UserContext.Consumer>
  );
}
```

需要注意的是，不可以在 Consumer 同層額外寫其他東西。

但你可以在 Consumer 組件中寫其他元素。

過度謹慎的你可能會不相信...

[![1578705650_64386.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/1578705650_64386.png)](https://zh.wikipedia.org/zh-tw/%E9%80%99%E5%80%8B%E5%8B%87%E8%80%85%E6%98%8E%E6%98%8E%E8%B6%85TUEEE%E5%8D%BB%E9%81%8E%E5%BA%A6%E8%AC%B9%E6%85%8E)

沒錯，如果你用以下方式寫，是有問題的。

```javascript
return (
  <UserContext.Consumer>
    {renderName}
    <div>123</div>
  </UserContext.Consumer>
);
```

沒錯，如果你用以下方式寫，是沒問題的。

```javascript
return (
  <div>
    <p>Hi, my name is</p>
    <UserContext.Consumer>
      {renderName}
    </UserContext.Consumer>
  </div>
);
```

\-

過度謹慎的你可能會越想越不對勁...

[![1578704598_81701.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/1578704598_81701.png)](https://zh.wikipedia.org/zh-tw/%E9%80%99%E5%80%8B%E5%8B%87%E8%80%85%E6%98%8E%E6%98%8E%E8%B6%85TUEEE%E5%8D%BB%E9%81%8E%E5%BA%A6%E8%AC%B9%E6%85%8E)

一開始已經在 createContext 設定過初始值：

```javascript
const UserContext = createContext(name);
```

為何在又要在 UserContext.Provider 內設定 value 初始值？

```html
<UserContext.Provider value={name}>
```

：「沒錯親愛的，是多寫了。」

如果父層省略掉 Provider ...，

那就是直接以當初 createContext 的初始值為主，

否則會優先以 Provider 的 value 為主。

```javascript
import React, { createContext } from 'react';

const name = 'Robby';

const UserContext = createContext(name);

function App() {
  return (
    <User />
  );
}

function User() {
  return (
    <UserContext.Consumer>
      {name => name}
    </UserContext.Consumer>
  );
}

export default App;
```

所以上述範例才故意這樣寫兩次。

![q7Dr5pR.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/q7Dr5pR.png)

\-

過度謹慎的你可能會想省時間...

[![1578706445_77621.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/1578706445_77621.png)](https://zh.wikipedia.org/zh-tw/%E9%80%99%E5%80%8B%E5%8B%87%E8%80%85%E6%98%8E%E6%98%8E%E8%B6%85TUEEE%E5%8D%BB%E9%81%8E%E5%BA%A6%E8%AC%B9%E6%85%8E)

每次都寫 UserContext.Consumer 也太大坨麻煩了吧？

：「沒錯親愛的，終於可以使用 useContext 了！」

useContext 必須放入經由 createContext 所建立的變數。

由於當初設定的 name 為字串，因此勾出來的時候，當然也就是字串囉！

```javascript
import React, { createContext, useContext, Fragment } from 'react';

const name = 'Robby';

const UserContext = createContext(name);

function App() {
  return (
    <User />
  );
}

function User() {
  const name = useContext(UserContext);
  return (
    <Fragment>
      {name}
    </Fragment>
  );
}

export default App;
```

你知道嗎？ 組件不想用任何元素包住子元素時， 可以使用 Fragment (片段) ，避免冗余的元素。

礙於時間不早，加上趕著早起投票。

本篇僅教學到 useState、useContext、createContext 應用。

為了不讓大家覺得筆者本篇... 過於敷衍過於廢文

最後提供一葛整合今日所學的奇淫技巧。

你知道嗎？奇淫技巧不一定代表是好的作法。

4\. useState＋useContext＋createContext
-------------------------------------

前面學到的 useContext，依照本篇的內容，目前僅能讀取，卻不能改變。

大多的使用方式為： useContext + useReducer

有興趣的人，建議可以先利用「神Ｏ海Ｏ」詢問看看有沒有文章可以看。

![1578677584_58859.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/1578677584_58859.jpg)

接著，來為大家介紹這種邪門歪道，殘害新人的範例應用，

參照剛剛的範例，我們繼續修改：

首先在上面 import 我們要使用的鉤鉤，

接著將 createContext 初始值改為 null， 因為等等要改在 component 內初始化。

```javascript
import React, { createContext, useContext, useState, Fragment } from 'react';

const UserContext = createContext(null);
```

接著我們利用 useState，建立一葛 name 的 state，

並使用 Provider 將初始值設定為陣列 \[name, setName\]。

```javascript
function App() {
  const [name, setName] = useState('Robby');

  return (
    <UserContext.Provider value={[name, setName]} >
      <User />
    </UserContext.Provider>
  );
}
```

你知道嗎？為了方便管理，可以使用物件，將 \[name, setName\] 用物件包起來，讀取時就會是物件！

最後在子組件同樣使用 useContext 提取出來。

就可以進行讀取，以及使用 setName 修改囉～

```javascript
function User() {
  const [name, setName] = useContext(UserContext);

  return (
    <Fragment>
      {name}
      <br />
      <button onClick={() => setName('Jack')}>ChangeName</button>
    </Fragment>
  );
}
```

完整程式碼如下：

```javascript
import React, { createContext, useContext, useState, Fragment } from 'react';

const UserContext = createContext(null);

function App() {
  const [name, setName] = useState('Robby');

  return (
    <UserContext.Provider value={[name, setName]} >
      <User />
    </UserContext.Provider>
  );
}

function User() {
  const [name, setName] = useContext(UserContext);

  return (
    <Fragment>
      {name}
      <br />
      <button onClick={() => setName('Jack')}>ChangeName</button>
    </Fragment>
  );
}

export default App;
```

雖然上述做法可以達到 Context 的修改，不過很少這樣使用。

你知道嗎？筆者沒有特別這樣使用過... 是不是很 GY。

因為基於 useState 所產生的值，應由所屬的 component 控管。

因此正規來說，還是會以 useContext + useReducer 的方式進行管理。

\-

最後
--

什麼是勾肥大戰？你不知道！？太弱惹喇！

[![916edd5e8389184a0131477e7511602c.JPG](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2020-01-10_React.js%20-%20%E5%A4%AA%E5%BC%B1%E7%9A%84%E6%88%91%EF%BC%8C%E6%8A%8A%20Hooks%20%E9%BB%9E%E6%BB%BF%E5%B0%B1%E5%B0%8D%E4%BA%86/916edd5e8389184a0131477e7511602c.JPG)](https://truth.bahamut.com.tw/s01/201102/916edd5e8389184a0131477e7511602c.JPG)

*   Ref：[【心得】勾肥入門教學文【1.25版】](https://forum.gamer.com.tw/Co.php?bsn=03044&sn=2277663)，

### _那麼就先這樣，投票去，ㄅㄅ！_

有勘誤之處，不吝指教。ob'\_'ov