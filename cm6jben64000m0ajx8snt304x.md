---
title: "Node.js - Express + MySQL"
seoTitle: "Node.js - Express + MySQL"
seoDescription: "node.js 搭載 mysql 之新手教學，請安心服用。"
datePublished: Mon Jul 18 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jben64000m0ajx8snt304x
slug: nodejs-express-mysql
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/banner/1468772407_70928.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/banner/1468772407_70928.png
tags: express, mysql

---

node.js 搭載 mysql 之新手教學，請安心服用。

Node.js 可以搭配許多種 DataBase 應用，例如 MongoDB、MySQL、MSSQL等。

本篇介紹 MySQL 整合應用，並以 Express4 做為開發框架，

若對 node.js express 不熟悉，建議可以先看此篇介紹 [Node.js Express4](https://dotblogs.com.tw/explooosion/2016/06/11/213626)。

實作說明
----

本篇將利用 mysql 實作出 （使用者）資料表新增、刪除、修改、搜尋。

[![1468772407_70928.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468772407_70928.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/1bb17882-f7d0-4e1e-93cb-6c3b46218e8a/1468772407_70928.png)

mysql 資料表

[![1468772735_17137.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468772735_17137.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/1bb17882-f7d0-4e1e-93cb-6c3b46218e8a/1468772735_17137.png)

框架安裝
----

到專案目錄底下，建立環境並安裝（本篇採用 [ejs](https://www.npmjs.com/package/ejs) 樣板設計）。

```bash
express -e
```
```bash
npm install
```

資料庫溝通套件安裝
---------

請留意是否您的環境已經安裝好 mysql 服務，

如果尚未安裝，可以參考  [WampServer](http://www.wampserver.com/en/) 或是 [XAMPP](https://www.apachefriends.org/zh_tw/index.html)。

此套件僅為與資料庫溝通，並非包含 MySQL！

上述完成安裝後才可以使用本套件，安裝 mysql

```bash
npm install mysql
```

連線設定
----

開啟 app.js ，在 var users 下方加入 mysql 引用 。

```javascript
var users = require('./routes/users');
```
```javascript
// DataBase 
var mysql = require("mysql");

var con = mysql.createConnection({
    host: "localhost",
    user: "root",
    password: "",
    database: "test"
});

con.connect(function(err) {
    if (err) {
        console.log('connecting error');
        return;
    }
    console.log('connecting success');
});
```

*   建立 con 連線物件，並利用 connet 進行連線
*   host：連線主機
*   user：帳號
*   password：密碼
*   database：資料庫

在此 app.use(express ...) 段程式碼下方加入。

```javascript
app.use(express.static(path.join(__dirname, 'public')));
```
```javascript
// db state
app.use(function(req, res, next) {
    req.con = con;
    next();
});
```

完整 app.js 內容。

```javascript
var express = require('express');
var path = require('path');
var favicon = require('serve-favicon');
var logger = require('morgan');
var cookieParser = require('cookie-parser');
var bodyParser = require('body-parser');

var routes = require('./routes/index');
var users = require('./routes/users');

// DataBase 
var mysql = require("mysql");

var con = mysql.createConnection({
    host: "localhost",
    user: "root",
    password: "",
    database: "test"
});

con.connect(function(err) {
    if (err) {
        console.log('connecting error');
        return;
    }
    console.log('connecting success');
});

var app = express();

// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');

// uncomment after placing your favicon in /public
//app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')));
app.use(logger('dev'));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));

// db state
app.use(function(req, res, next) {
    req.con = con;
    next();
});

app.use('/', routes);
app.use('/users', users);


// catch 404 and forward to error handler
app.use(function(req, res, next) {
    var err = new Error('Not Found');
    err.status = 404;
    next(err);
});

// error handlers

// development error handler
// will print stacktrace
if (app.get('env') === 'development') {
    app.use(function(err, req, res, next) {
        res.status(err.status || 500);
        res.render('error', {
            message: err.message,
            error: err
        });
    });
}

// production error handler
// no stacktraces leaked to user
app.use(function(err, req, res, next) {
    res.status(err.status || 500);
    res.render('error', {
        message: err.message,
        error: {}
    });
});


module.exports = app;
```

SQL 應用
------

接下來進行簡單的 SELECT 語法取出資料，

編輯 index.js，在 / 根目錄 router 部分，我們將取出資料表內容。

```javascript
// home page
router.get('/', function(req, res, next) {

    var db = req.con;
    var data = "";

    db.query('SELECT * FROM account', function(err, rows) {
        if (err) {
            console.log(err);
        }
        var data = rows;

        // use index.ejs
        res.render('index', { title: 'Account Information', data: data});
    });

});
```

*   建立 var db 賦予 req.con 連線物件資訊
*   db.query( ) 為進行資料庫存取，返回結果為 err、rows
*   回傳資料 rows 以陣列格式儲存
*   在 render 部分，我們將 rows 指定到 data 變數
*   data: data，此為給予名稱 data，其內容為 data，將於 ejs 樣板部分使用

再來則是編輯首頁樣板 index.ejs。

```html
<h1>Account - List</h1>
    <table>
        <tr>
            <th>id</th>
            <th>userid</th>
            <th>password</th>
            <th>email</th>
        </tr>
        <% for ( var i = 0 ; i < data.length ; i++){ %>
            <tr>
                <td>
                    <%= data[i].id  %>
                </td>
                <td>
                    <%= data[i].userid  %>
                </td>
                <td>
                    <%= data[i].password  %>
                </td>
                <td>
                    <%= data[i].email  %>
                </td>
            </tr>
            <% } %>
    </table>
```

在 ejs 樣板設計中，利用 <% %> 可執行 javascript 語法，

我們以此方式，將資料集印出。

*   利用 data.length ，可取得資料筆數 
*   data\[i\].id：引數 i 為 DataTable 中的列索引，id 為資料表欄位名稱   

完成後加點 css 樣式，並執行環境。

```bash
npm start
```

[http://localhost:3000/](http://localhost:3000/) ，畫面為如下所示。![1468772850_01337.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468772850_01337.png)

新增資料
----

在 index.js 檔案中，加入 /add 部分跳轉至新增資料畫面，並建立一個 userAdd.ejs 樣板。

index.ejs，在首頁加入「新增」按鈕

```html
<input type='submit' value='Add' onclick="javascript: location.href='add'">
```

index.js

當進入 [http://localhost:3000/add](http://localhost:3000/add) 頁面時，render userAdd.ejs 樣板。

```javascript
// add page
router.get('/add', function(req, res, next) {

    // use userAdd.ejs
    res.render('userAdd', { title: 'Add User'});
});
```

userAdd.ejs 

form 部分，我們採用 post 方式，有別於原本 get ，將資料傳遞至 userAdd（由 router 執行）

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title></title>
</head>

<body>
    <form name="addform" action="userAdd" method="post" accept-charset="utf-8" >
        <h1>Account - Add</h1>
        <div>
            <label>userid：</label>
            <input type="text" name="userid" placeholder="userid" />
        </div>
        <div>
            <label>password：</label>
            <input type="password" name="password" placeholder="password">
        </div>
        <div>
            <label>email：</label>
            <input type="text" name="email" placeholder="email">
        </div>
        <div>
            <input type='submit' value='Submit'>
            <input type='reset' value='Reset'>
            <input type='button' value='Back' onclick="javascript: location.href='/'">
        </div>
    </form>
</body>

</html>
```

接下來為資料頁面 post 後，於 userAdd 進行資料 insert

```javascript
// add post
router.post('/userAdd', function(req, res, next) {

    var db = req.con;

    var sql = {
        userid: req.body.userid,
        password: req.body.password,
        email: req.body.email
    };

    //console.log(sql);
    var qur = db.query('INSERT INTO account SET ?', sql, function(err, rows) {
        if (err) {
            console.log(err);
        }
        res.setHeader('Content-Type', 'application/json');
        res.redirect('/');
    });

});
```

*   post 過來的資料，可利用 req.body.\[tag name\] 取得 
*   var sql 部分，將以 json 方式組成： userid 為資料表欄位名稱
*   在 mysql query 部分 " ? " ，可代表單一變數，或以 json格式表示
*   response 部分，setHeader 以 json 表示
*   並在完成 insert 後，導回首頁

完成後加點 css 如下結果：

[http://localhost:3000/](http://localhost:3000/)

![1468775034_84578.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468775034_84578.png)

[http://localhost:3000/add](http://localhost:3000/add)

![1468774886_56335.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468774886_56335.png)

編輯資料
----

在剛剛首頁 index.ejs 部分，我們追加「編輯」按鈕，並且在點擊時，進入編輯頁面

```html
<td>
　　<input type="button" name="edit" value="Edit" onclick="Edit('<%= data[i].id  %>');" />
</td>
```
```javascript
function Edit(id) {
        window.location.href = "/userEdit?id=" + id;
    }
```

*   依據 id 值加在網址後面，讓編輯頁面能以 get 方式取得 key

回到 index.js 增加 userEdit，依接收到的 id 值 串接 SQL

```javascript
// edit page
router.get('/userEdit', function(req, res, next) {

    var id = req.query.id;
    var db = req.con;
    var data = "";

    db.query('SELECT * FROM account WHERE id = ?', id, function(err, rows) {
        if (err) {
            console.log(err);
        }

        var data = rows;
        res.render('userEdit', { title: 'Edit Account', data: data });
    });

});
```

*   若要取得網址列參數，可使用 req.query.\[參數\]
*   render 部分我們將載入 userEdit 樣板（下面步驟將建立此樣板）

建立編輯頁面樣板 userEdit.ejs

```html
<form name="editform" action="userEdit" method="post" accept-charset="utf-8">
        <h1>Account - Edit</h1>
        <input type="hidden" name="id" value="<%=data[0].id  %>" />
        <div>
            <label>userid：</label>
            <input type="text" name="userid" placeholder="userid" value="<%=data[0].userid %>" readonly />
        </div>
        <div>
            <label>password：</label>
            <input type="text" name="password" placeholder="password" value="<%=data[0].password %>" />
        </div>
        <div>
            <label>email：</label>
            <input type="text" name="email" placeholder="email" value="<%=data[0].email %>">
        </div>
        <div>
            <input type='submit' value='Submit'>
            <input type='reset' value='Reset'>
            <input type='button' value='Back' onclick="javascript: window.history.back();">
        </div>
    </form>
```

*   form 部分 我們使用 post，並傳到 userEdit（下方將新增 userEdit 的 post 事件）
*   帳號 userid 部分，使用 readonly，畢竟沒有人再改帳號啊～～
*   補上一些功能按鈕：reset、back 

 在 index.js 部分，新增 post 事件

```javascript
router.post('/userEdit', function(req, res, next) {

    var db = req.con;
    var id = req.body.id;

    var sql = {
        userid: req.body.userid,
        password: req.body.password,
        email: req.body.email
    };

    var qur = db.query('UPDATE account SET ? WHERE id = ?', [sql, id], function(err, rows) {
        if (err) {
            console.log(err);
        }

        res.setHeader('Content-Type', 'application/json');
        res.redirect('/');
    });

});
```

*   post 方法使用 body進行取得 name 物件之內容
*   update 內容一樣以 json 方式儲存
*   header 部分：application/json
*   更新完畢後導回首頁 redirect('/');

完成後...一樣加點 css 給她，然後執行

```bash
npm start
```

 [http://localhost:3000/​](http://localhost:3000/)![1468851786_23541.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468851786_23541.png)

試試修改資料並更新吧~，[http://localhost:3000/userEdit?id=1](http://localhost:3000/userEdit?id=1)

![1468852150_95323.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468852150_95323.png)

刪除資料
----

完成讀取、新增、修改後，接下來是「刪除」資料功能，

我們修改首頁，仿造修改按鈕，追加一枚刪除按鈕

index.ejs

```html
<input type="button" name="delete" value="Delete" onclick="Delete('<%= data[i].id  %>');" />
```
```javascript
function Delete(id) {
        var rs = confirm('Confirm to delete?');
        if (rs) {
            window.location.href = "/userDelete?id=" + id;
        }
    }
```

樣板修改完畢後，在 index.js 裡面追加 router

```javascript
router.get('/userDelete', function(req, res, next) {

    var id = req.query.id;
    var db = req.con;

    var qur = db.query('DELETE FROM account WHERE id = ?', id, function(err, rows) {
        if (err) {
            console.log(err);
        }
        res.redirect('/');
    });
});
```

*   利用 get 方式，透過 req.query.id 將網址列的 id 參數取出
*   執行 DELETE query 
*   完成後導回首頁 redirect('/');

一樣發揮創意補上 css (被打)，然後執行

```bash
npm start
```

 [http://localhost:3000/](http://localhost:3000/)[![1468853043_08848.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468853043_08848.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/1bb17882-f7d0-4e1e-93cb-6c3b46218e8a/1468853043_08848.png)

搜尋資料
----

最後實作簡單的搜尋功能，在 index.ejs 樣板增加搜尋按鈕

```html
<div class="search">
        <label>UserId：</label>
        <input type="text" name="suserid" value="" placeholder="input the userid">
        <input type="button" name="sSearch" value="Search" onclick="Search();">
    </div>
```
```javascript
function Search() {

        var userid = document.getElementsByName('suserid')[0].value;
        window.location.href = "/?user=" + userid;;
    }
```

因搜尋是在首頁中執行，故我們修改根目錄的 router 事件

```javascript
// home page
router.get('/', function(req, res, next) {

    var db = req.con;
    var data = "";

    var user = "";
    var user = req.query.user;

    var filter = "";
    if (user) {
        filter = 'WHERE userid = ?';
    }

    db.query('SELECT * FROM account ' + filter, user, function(err, rows) {
        if (err) {
            console.log(err);
        }
        var data = rows;

        // use index.ejs
        res.render('index', { title: 'Account Information', data: data, user: user });
    });

});
```

*   若網址參數 user有資料，則 pass 給 var user
*   如果 user 有資料，則串接篩選字串
*   在 render 部分，我們補上 user:user（將搜尋條件返回頁面顯示，有點像 ASP.NET 的 PostBack 概念）

因此回到剛剛首頁樣板 index.ejs，我們在搜尋文字欄位，將剛剛取得的 user 放入

```html
<input type="text" name="suserid" value="<%=user  %>" placeholder="input the userid">
```

*   如此一來，每次搜尋完後，該欄位資料仍會顯示剛剛的文字

完成後補上奇妙的 css，然後執行

```bash
npm start
```

[http://localhost:3000/](http://localhost:3000/)

[![1468853605_50915.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468853605_50915.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/1bb17882-f7d0-4e1e-93cb-6c3b46218e8a/1468853605_50915.png)

本實作範本 + 資料表下載
-------------

範例存於小弟的 [Github](https://github.com/explooosion/Node.js-Express-With-MySQL) ，不妨給個星星吧 ><

```bash
git clone https://github.com/explooosion/Node.js-Express-With-MySQL.git
```

進入專案

```bash
cd Node.js-Express-With-MySQL
```

安裝套件

```bash
npm install
```

匯入專案資料夾內 account.sql 

[![1468854864_05415.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-07-18_Node.js%20-%20Express%20%2B%20MySQL/1468854864_05415.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/1bb17882-f7d0-4e1e-93cb-6c3b46218e8a/1468854864_05415.png)

以上為簡單的 Node.js Express + MySQL

教學範例來源為參考此篇文章：[Node.js Express connectivity with PHPMyAdmin](https://trinitytuts.com/node-js-express-connectivity-with-phpmyadmin/)

有勘誤之處，不吝指教。ob'\_'ov