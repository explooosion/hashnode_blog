---
title: "Node.js - Express + MongoDB + Socket.IO (以聊天室為範例) -［2］"
seoTitle: "Node.js - Express + MongoDB + Socket.IO (以聊天室為範例) -［2］"
seoDescription: "express 搭配 mongodb 建立聊天室，後半段。"
datePublished: Sat Jan 27 2018 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbezia000709kw1uoa28au
slug: nodejs-express-mongodb-socketio-2
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/banner/1517054045_4735.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/banner/1517054045_4735.png
tags: mongodb, ui

---

express 搭配 mongodb 建立聊天室，後半段。

有鑑於先前發過相關系列文章：

*   [express + mysql](https://dotblogs.com.tw/explooosion/2016/07/18/010601)
*   [express + mssql](https://dotblogs.com.tw/explooosion/2017/05/28/012745)

如果沒有安裝過 MongoDB，可以參考此篇：

*    [MongoDB - 詳細到讓人牙起來的安裝教學](https://dotblogs.com.tw/explooosion/2018/01/21/040728) 

一、前言
----

由於內容太多了，本系列將分成上下篇說明。

範例專案放置在 [Github](https://github.com/explooosion/ChatRoom-With-SocketIO) 上，可以直接 clone 下來試試，

本篇示範的簡易專案放在 [SimpleExample](https://github.com/explooosion/ChatRoom-With-SocketIO/tree/master/SimpleExample) 裡面，可以直接查看。

上篇：[Node.js - Express + MongoDB + Socket.IO (以聊天室為範例) -［1］](https://dotblogs.com.tw/explooosion/2018/01/27/170320)

上篇利用 socket.io 進行事件廣播，

本篇將利用 mongodb，把訊息存進資料庫裡。

二、資料庫連線與訊息讀寫
------------

由於本範例資料庫的存取，只有在 socket 訊息交換時候，

因此在設計上將此部分抽離出來。

建立資料夾名為 socket，檔案名為 index.js

![1517054045_4735.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517054045_4735.png)

\[ socket / index.js \]

建立一個 SocketHander 類別：

```javascript
class SocketHander {
    constructor() {
        this.db;
    }
}
```

還記得我們前面建立了 [Schema()](http://mongoosejs.com/docs/api.html#model-js) 嗎？

將該模型引入，而時間部份使用 [moment.js](https://momentjs.com/)，方便我們進行操作。

```bash
npm install -S moment
```

\[ socket / index.js \]

```javascript
const Messages = require('../models/Messages');
const moment = require('moment');

class SocketHander {
    constructor() {
        this.db;
    }
}
```

\[ socket / index.js \]

接著建立資料庫「連線」、「儲存」和「取出」方法。

```javascript
const Messages = require('../models/Messages');
const moment = require('moment');
class SocketHander {

    constructor() {
        this.db;
    }

    connect() {
        this.db = require('mongoose').connect('mongodb://localhost:27017/chat');
        this.db.Promise = global.Promise;
    }

    getMessages() {
        return Messages.find();
    }

    storeMessages(data) {

        console.log(data);
        const newMessages = new Messages({
            name: data.name,
            msg: data.msg,
            time: moment().valueOf(),
        });

        const doc = newMessages.save();
    }
}

module.exports = SocketHander;
```

*   connect：連線部分使用到 global.Promise ( [Promises for the MongoDB Driver](http://mongoosejs.com/docs/promises.html#promises-for-the-mongodb-driver) )
*   getMessages：取資料使用 find ( [Queries](http://mongoosejs.com/docs/queries.html) )
*   storeMessages：new 一個 Messages 模型，最後使用 save ( [Models](http://mongoosejs.com/docs/models.html) ) 儲存

三、Socket.io 事件建立
----------------

\[ app.js \]

引入 socket / index.js 。

```javascript
const SocketHander = require('./socket/index');
```

通訊成功時，連線資料庫。

```javascript
io.on('connection', (socket) => {

  console.log('a user connected');

  socketHander = new SocketHander();

  socketHander.connect();

});
```

改寫 message 廣播事件，當有人傳送訊息時，將訊息寫入資料庫。

```javascript
socket.on("message", (obj) => {
  socketHander.storeMessages(obj);
  io.emit("message", obj);
});
```

\[ public / javascripts / app.js \]

到前端頁面發送訊息，測試是否被寫入資料庫內。

```javascript
let data = {
    name: 'Robby',
    msg: 'Hi~',
};

socket.emit('message', data);
```

頁面重整後，可以看到後端收到訊息，並且資料庫也確實有寫入。

![1517058847_56873.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517058847_56873.png)![1517058907_82341.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517058907_82341.png)

而用戶端也有收到訊息的廣播：

[![1517059100_9572.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517059100_9572.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/62d79cec-5070-45ce-9278-946355ce5f26/1517059100_9572.png)

四、實作【極簡】聊天系統 - 介面設計
-------------------

本實作介面使用了 [Tocas UI](https://tocas-ui.com/) 提供的 [example](https://examples.tocas-ui.com/pages/chatroom.html) 進行修改。

由於修改的部分眾多，非本文章系列重點，

因此在文章上，僅以簡易的介面方式呈現。

以下為簡易版所寫的樣式

\[ views / index.ejs \]

首先刻化好聊天系統的表單，大致簡易了一下：

```html
<body>
  <div class="chats">
    <div class="chat">
      <div class="group">
        <div class="name">Robby：</div>
        <div class="msg">Hi~</div>
      </div>
      <div class="time">11分鐘前</div>
    </div>
    <div class="chat">
      <div class="group">
        <div class="name">Robby：</div>
        <div class="msg">Hola~</div>
      </div>
      <div class="time">10分鐘前</div>
    </div>
  </div>
  <div class="message">
    <input id="name" type="text" placeholder="your name" />
    <input id="msg" type="text" placeholder="input the message" />
    <button type="button">送出</button>
  </div>
</body>
```

\[ public / stylesheets / style.css \]

```css
body {
  padding: 50px;
  font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
}

a {
  color: #00B7FF;
}

.chats {
  padding: 10px 5px;
  height: 200px;
  width: 500px;
  background: #eee;
  overflow-y: scroll;
}

.chats .chat {
  display: flex;
  margin: 5px 0;
}

.chats .chat .group {
  display: inherit;
  word-wrap: normal;
}

.chats .chat .group .name {
  padding: 0 10px;
  font-weight: bold;
}

.chats .chat .time {
  padding-left: 10px;
  font-size: 10px;
  line-height: 18px;
  color: #aaa;
}

.message {
  margin-top: 10px;
}

.message input {
  padding: 0 5px;
  height: 25px;
  width: 300px;
}

.message input:first-child {
  width: 80px;
}

.message button {
  height: 32px;
  width: 100px;
}
```

畫面大致上如下：

[![1517061054_16931.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517061054_16931.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/62d79cec-5070-45ce-9278-946355ce5f26/1517061054_16931.png)

五、實作【極簡】聊天系統 - 事件撰寫
-------------------

### 訊息發送功能

\[ public / javascripts / app.js \]

取得表單上的名稱和內容，並利用 socket.emit 發送訊息。

```javascript
document.querySelector('button').addEventListener('click', () => {
    Send();
});

function Send() {

    let name = document.querySelector('#name').value;
    let msg = document.querySelector('#msg').value;
    if (!msg && !name) {
        alert('請輸入大名和訊息');
        return;
    }
    let data = {
        name: name,
        msg: msg,
    };
    socket.emit('message', data);
    document.querySelector('#msg').value = '';
}
```

### 訊息接收功能

\[ public / javascripts / app.js \]

在 message 監聽訊息，當接收資料時，呼叫 appendData 方法。

```javascript
socket.on('message', (obj) => {
    console.log(obj);
    appendData([obj]);
});

function appendData(obj) {
}
```

回顧一下前面，這是每個人的訊息元素組成架構：

```html
<div class="chat">
  <div class="group">
    <div class="name">Robby：</div>
    <div class="msg">Hi~</div>
  </div>
  <div class="time">11分鐘前</div>
</div>
```

當有新訊息時，要 append 進去，在此可以使用 [innerHTML](https://www.w3schools.com/jsref/prop_html_innerhtml.asp) 新增元素。

```javascript
function appendData(obj) {

    let el = document.querySelector('.chats');
    let html = el.innerHTML;

    obj.forEach(element => {
        html +=
            `
            <div class="chat">
                <div class="group">
                    <div class="name">${element.name}：</div>
                    <div class="msg">${element.msg}</div>
                </div>
                <div class="time">${element.time}</div>
            </div>
            `;
    });
    el.innerHTML = html.trim();
}
```

測試發送訊息看看，你可能會疑惑，時間為何是 undefined。

因為當初在 \[ socket / index.js \] 裡面我們是存入 moment().valueOf()。

他的格式為將時間轉成 [Unix時間戳（毫秒）](https://momentjs.com/docs/#/displaying/unix-timestamp-milliseconds/)，在此用意是為了使用 [fromNow()](https://momentjs.com/docs/#/i18n/changing-locale/)。

[![1517062553_07584.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517062553_07584.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/62d79cec-5070-45ce-9278-946355ce5f26/1517062553_07584.png)

\[ views / index.ejs \]

引入 moment.js ( 後端的是npm安裝，客戶端無法讀取 )：

```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.20.1/moment.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.20.1/locale/zh-tw.js'></script>
```

\[ public / javascripts / app.js \]

因此我們把時間的部分改成：

```javascript
${moment(element.time).fromNow()}
```

發送訊息就可以看到「幾秒前」。

[![1517063085_155.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517063085_155.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/62d79cec-5070-45ce-9278-946355ce5f26/1517063085_155.png)

### 取得歷史訊息

\[ app.js \]

首先要建立一個歷史訊息的廣播。

```javascript
io.on('connection', async (socket) => {

  console.log('a user connected');

  socketHander = new SocketHander();

  socketHander.connect();

  const history = await socketHander.getMessages();

  io.emit('history', history);

  // 其他省略 ...

});
```

*   由於讀取資料庫使用了 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) ，在這邊我們使用異步函數 asnyc、await
*   建立廣播事件「history」 

\[ public / javascripts / app.js \]

客戶端的部分則是監聽「history」即可。

```javascript
socket.on('history', (obj) => {
    if (obj.length > 0) {
        appendData(obj);
    }
});
```

*   為了確定是否有讀取到歷史訊息，使用 length 判斷

實際測試，可以發現一載入畫面就有先前的訊息。

[![1517064052_5915.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517064052_5915.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/62d79cec-5070-45ce-9278-946355ce5f26/1517064052_5915.png)

### 為何別人載入的時候我會跳出歷史訊息？

如果你已經測試過兩人以上的連線測試，會發現這個問題。

同時開兩個頁面即可多人連線。

[![1517064713_66973.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517064713_66973.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/62d79cec-5070-45ce-9278-946355ce5f26/1517064713_66973.png)

*   當右邊有新連線加入，左邊原本視窗會跟著載入歷史訊息
*   這是因為廣播的時候，是針對所有人

\[ app.js \]

我們要將歷史訊息的廣播對象鎖定為當前用戶。

```javascript
// 原本舊的
// io.emit('history', history);

const socketid = socket.id;
io.to(socketid).emit('history', history);
```

*   由於連線時 socket 會自動配給 id，利用 socket.id 就可取得
*   io.to(sockerid)：可以將訊息廣播給鎖定的 id

如此一來就可以解決重複載入的問題。

### 如何讓卷軸自動捲到底？

\[ public / javascripts / app.js \]

使用 [scrollTo()](https://www.w3schools.com/jsref/met_win_scrollto.asp)、[scrollHeight](https://www.w3schools.com/jsref/prop_element_scrollheight.asp) 就可捲動到底。

```javascript
function scrollWindow() {
    let h = document.querySelector('.chats');
    h.scrollTo(0, h.scrollHeight);
}
```

然後在 appendData() 結尾處補上即可。

```javascript
function appendData(obj) {

    // 以上省略
    el.innerHTML = html.trim();
    scrollWindow();
}
```

重新整理畫面後，就可以看到卷軸自動捲到底囉～

[![1517065892_80671.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB2%EF%BC%BD/1517065892_80671.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/62d79cec-5070-45ce-9278-946355ce5f26/1517065892_80671.png)

六、後記
----

聊天的功能想必不只有訊息傳送，

也許未來可以試著增加檔案傳送、圖片顯示、超連結顯示等等，

甚至也可仿造 [Discord](https://discordapp.com/)，建立出語音平台。

範例專案放置在 [Github](https://github.com/explooosion/ChatRoom-With-SocketIO) 上，可以直接 clone 下來試試，

本篇示範的簡易專案放在 [SimpleExample](https://github.com/explooosion/ChatRoom-With-SocketIO/tree/master/SimpleExample) 裡面，可以直接查看。

大家也一起來打造屬於自己的 [LINE](https://line.me/zh-hant/) 吧！

有勘誤之處，不吝指教。ob'\_'ov