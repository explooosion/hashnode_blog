---
title: "Node.js - Express + MongoDB + Socket.IO (以聊天室為範例) -［1］"
seoTitle: "Node.js - Express + MongoDB + Socket.IO (以聊天室為範例) -［1］"
seoDescription: "express 搭配 mongodb 建立聊天室。"
datePublished: Sat Jan 27 2018 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbez3s000q0ajxfp33157v
slug: nodejs-express-mongodb-socketio-1
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/banner/1517039486_46847.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/banner/1517039486_46847.png
tags: mongodb, ui

---

express 搭配 mongodb 建立聊天室。

有鑑於先前發過相關系列文章：

*   [express + mysql](https://dotblogs.com.tw/explooosion/2016/07/18/010601)
*   [express + mssql](https://dotblogs.com.tw/explooosion/2017/05/28/012745)

當然要來一篇 MongoDB，但不會特別著重在此。

原本想說寫個 CRUD，寫著寫著就 局部最佳化了......

如果沒有安裝過 MongoDB，可以參考此篇：

*    [MongoDB - 詳細到讓人牙起來的安裝教學](https://dotblogs.com.tw/explooosion/2018/01/21/040728) 

由於內容太多了，本系列將分成上下篇說明

一、前言
----

這篇比較適合初探 [Socket.IO](https://socket.io/) 才對，並以聊天室為例子，

整體架構上為：

*   [Node.js Express](https://github.com/expressjs/express) (back-End)
*   [MongoDB](https://www.mongodb.com/) (database)
*   [Socket.IO](https://socket.io/) (time engine)
*   [Tocas UI](https://tocas-ui.com/) (css library)

這篇的完成專案放置在 [Github](https://github.com/explooosion/ChatRoom-With-SocketIO) 上，可以直接 clone 下來試試，

由於本範例沒有使用 [jQuery](https://jquery.com/)，所以可能內容會有點多惹，

如果覺得不錯，不妨給個⭐。😊

### 範例結果畫面

DEMO：[http://218.161.68.185/](http://218.161.68.185/)

[![1517039486_46847.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/1517039486_46847.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/9552ee65-8b9e-4a71-9283-84da0dde9656/1517039486_46847.png)

二、框架安裝與環境設置
-----------

### express - 安裝

本範例使用 [ejs](http://www.embeddedjs.com/) 樣板引擎。

```bash
npm install -g express-generator@4
```
```bash
express chat --view=ejs && cd./chat
```
```
npm install
```

### MongoDB - 安裝

本專案使用 [mongoose](http://mongoosejs.com/) 套件進行 [CRUD](https://zh.wikipedia.org/wiki/%E8%B3%87%E6%96%99%E6%93%8D%E7%B8%B1%E8%AA%9E%E8%A8%80)。

```bash
npm install -S mongoose
```

通常個人習慣會建立資料表的基本模型，

因此先建立一個資料夾名為 models，

裡面新增 Messages.js，此檔案用來定義 Schema。

為了方便辨識，習慣 Schema 檔與資料表相同。

![1517042347_15456.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/1517042347_15456.png)

\[ models / Messages.js \]

本表儲存聊天紀錄，欄位有三個，詳細設定可以參考 [Schema()](http://mongoosejs.com/docs/api.html#model-js)。

```javascript
const mongoose = require('mongoose');

const messagesSchema = mongoose.Schema({
    name: String,
    msg: String,
    time: Number,
});

module.exports = mongoose.model('Messages', messagesSchema);
```

*   name：使用者名稱。
*   msg：訊息內容。
*   time：發送時間。

### Socket.IO - 安裝

安裝 [socket.io](https://socket.io/)。

```bash
npm install -S socket.io
```

\[ app.js \]

於 app 下方，引入 socket.io，並使用 3001 port 進行監聽。

```javascript
/* ... 以上省略 */

var app = express();

const server = require('http').Server(app);
const io = require('socket.io')(server);

io.on('connection', (socket) => {
  console.log('a user connected');

  socket.on("disconnect", () => {
    console.log("a user go out");
  });

});

server.listen(3001);
```

*   connection：使用者連線監聽，為保留事件。
*   disconnect：使用者斷開連線，為保留事件。

\[ views / index.ejs \]

為了方便測試是否成功，我們可以在前端頁面進行通訊連線，

另外建立一個檔案 app.js (方便整理)，進行連線操作，

引入 socket.io.js 以及 app.js。

```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/socket.io/2.0.4/socket.io.js'></script>
```
```html
<script src="./javascripts/app.js"></script>
```

\[ public / javascripts / app.js \]

```javascript
socket = io.connect('ws://localhost:3001');
```

重啟服務並瀏覽網頁 [http://localhost:3000/](http://localhost:3000/)，

或是關閉網頁就可看到使用者離開訊息。

![1517044773_80293.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/1517044773_80293.png)

### Socket.IO - 廣播訊息

我們可以利用 io.emit，將訊息廣播給使用者。

簡易架構圖如下：

[![SXTFi.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/SXTFi.png)](https://stackoverflow.com/questions/36207858/socket-io-assigning-custom-socket-id)

*   當使用者發送訊息時，廣播 chat 事件。
*   當使用者離開連線時，廣播 disconnect 事件。

\[ app.js \]

```javascript
io.on('connection', (socket) => {

  console.log('a user connected');

  io.emit("message", 'Hello wWrld!');

  socket.on("disconnect", () => {
    console.log("a user go out");
  });

});
```

*   message：為廣播名稱。

\[ public / javascripts / app.js \]

用戶端監聽廣播名稱 message。

```javascript
socket = io.connect('ws://localhost:3003');

socket.on('message', (obj) => {
    console.log(obj);
});
```

開啟瀏覽器 ( [http://localhost:3000/](http://localhost:3000/) ) + F8 ，

接收伺服器廣播訊息。

![1517045376_78977.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/1517045376_78977.png)

### Socket.IO - 發送訊息

\[ app.js \]

接下來要實作用戶端發送訊息，

首先於伺服器建立事件傾聽：

```javascript
// io.on('connection', (socket) => { ...

socket.on("message", (obj) => {
  io.emit("message", '應聲蟲:' + obj);
});
```

*   當接收來自用戶端發送的訊息後，伺服器廣播回去。

\[ public / javascripts / app.js \]

```javascript
socket.emit('message', 'Hi! Robby');
```

開啟瀏覽器 ( [http://localhost:3000/](http://localhost:3000/) ) + F8 ，

使用者發送訊息，伺服器立即廣播回來。

![1517046322_70107.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-01-27_Node.js%20-%20Express%20%2B%20MongoDB%20%2B%20Socket.IO%20(%E4%BB%A5%E8%81%8A%E5%A4%A9%E5%AE%A4%E7%82%BA%E7%AF%84%E4%BE%8B)%20-%EF%BC%BB1%EF%BC%BD/1517046322_70107.png)

### Next Stop ...

### [Node.js - Express + MongoDB + Socket.IO (以聊天室為範例) -［2］](https://dotblogs.com.tw/explooosion/2018/01/27/210248)

有勘誤之處，不吝指教。ob'\_'ov