---
title: "Node.js - Express + MSSQL"
seoTitle: "Node.js - Express + MSSQL"
seoDescription: "node.js 使用 express 讀取 mssql 應用。"
datePublished: Sun May 28 2017 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbesqu000n0ajx10kg7kaf
slug: nodejs-express-mssql
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/banner/1495964674_27285.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/banner/1495964674_27285.png
tags: express

---

node.js 使用 express 讀取 mssql 應用。

先前曾發過一篇使用 [express + mysql](https://dotblogs.com.tw/explooosion/2016/07/18/010601)，

本篇介紹使用 express + mssql，

若對 node.js express 不熟悉，建議可以先看此篇介紹 [Node.js Express4](https://dotblogs.com.tw/explooosion/2016/06/11/213626)。

樣版部分則改使用 [jade（pug）](https://pugjs.org)，不熟悉樣樣板使用方式可以先看看～

[![1495964674_27285.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495964674_27285.png)](https://pugjs.org/api/getting-started.html)

本篇所需資料庫以及完整範例已放置 **[Github](https://github.com/explooosion/Node.js-Express-With-MSSQL)** 上，

如果對你有所幫助，不妨丟一顆 ★ 吧~ 

![1495965291_83602.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495965291_83602.png)

實作結果畫面
------

利用 [npm mssql](https://www.npmjs.com/package/mssql)  （[Github](https://github.com/patriksimek/node-mssql)）套件，進行使用者清單列表管理，包含新增、編輯、刪除。

[![1495905016_09003.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495905016_09003.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495905016_09003.png)

資料表清單。

![1495905203_04303.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495905203_04303.png)

框架安裝
----

語法：express 專案名稱。

```
express mssqldemo
```
```bash
cd mssqldemo
```
```bash
npm install
```

資料庫套件安裝
-------

安裝 [mssql](https://github.com/patriksimek/node-mssql)。

```bash
npm install mssql
```

連線設定
----

連線內容建議移置外部另外寫，

在專案底下建立 config 資料夾，並新增一個 db.js ，

當然，資料庫的帳號密碼就是依您的環境自行修改囉！

```javascript
const db =
    {
        "user": "sa",
        "password": "e2345678",
        "server": "localhost",
        "database": "ExpressDemo"
    };

module.exports = db;
```

SQL 應用
------

[npm mssql](https://github.com/patriksimek/node-mssql) 語法部分，本篇使用較為簡易的 **Callbacks** 方式，

該套件也提供了許多種方式，若環境許可，也可以改使用：

*   Async/Await（ES7）
*   Promises（ES6）
*   Callbacks
*   Streaming

### Connect 語法說明

建立簡單的連線，使用 connect，帶入資料庫連線資訊，

結束後以 close() 關閉連線資訊。

```javascript
sql.connect(db, function (err) {

　　sql.close();
});
```

### Query 語法說明

建立一個 query，並寫入一些 sql 語法，callback 部分有 err、result，

而在 result 陣列中， result.recordset 則是我們要的資料集合，

想要了解 result 結構，直接 console.log( result ); 就能清楚明白囉！

```javascript
var request = new sql.Request();
request.query("select * from UserList", function (err, result) {

});
```

### Parameter 語法說明

通常在使用 sql 查詢，為了防止 SQL Injection，都會使用預儲式（Parameter）。

```javascript
var request = new sql.Request();
request.input('id', sql.Int, req.body.id);
request.input('username', sql.NVarChar(50), req.body.username);
```

也可簡寫成：

```javascript
var request = new sql.Request();
request.input('id', sql.Int, req.body.id)
       .input('username', sql.NVarChar(50), req.body.username)
```

需注意的是，request （get / post）過來的資料取得方式不太相同：

*   get：req.params.\[網址列參數\]
*   post：req.body.\[表單中的 name\]

而資料型別的方式也有很多種，簡單列舉幾項，選擇時須注意：

*   sql.Int
*   sql.NVarChar()
*   sql.Date
*   sql.DateTime
*   sql.Decimal
*   sql.Float

實作 - 環境前置
---------

為了方便撰寫，編輯器不妨安裝一些相關的套件吧～

個人是使用 [VScode](https://code.visualstudio.com/)，如果你也使用這個，可以參考這些套件：

[![1495961417_6383.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495961417_6383.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495961417_6383.png)

[![1495961408_58141.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495961408_58141.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495961408_58141.png)

### 本範例路由結構

路徑

說明

SQL

方法

/

首頁（根目錄）

select \* from UserList

GET

/edit/:id

編輯頁面（id primary key）

select \* from UserList where id = @id

GET

/update

此頁由 edit 頁面 post 過來的 form，以進行更新

update UserList set pwd=@pwd ...

POST

/add

route 接收到 /add 時，render add.jade 樣板

\-

GET

/add

form 將本頁資料 post 到後端進行 insert

insert into UserList (...) values (...)

POST

/delete/:id

刪除指定 id 資料

delete from UserList where id = @id

GET

所有的路由皆在 routes / index.js 編輯，方便大家理解，統一在此，

由於要進行資料庫的讀取使用，因此首先引用 MSSQL 套件。

```javascript
var express = require('express');
var router = express.Router();

var db = require('../config/db');
var sql = require('mssql');
```

引用資料庫設定檔案以及MSSQL套件

1.  db：require('../config/db')
2.  sql：require('mssql')

實作 - Select
-----------

### 【routes / index.js】

```javascript
/* GET home page. */
router.get('/', function (req, res, next) {

  sql.connect(db, function (err) {
    if (err)
      console.log(err);

    var request = new sql.Request();
    request.query("select * from UserList", function (err, result) {

      if (err) {
        console.log(err)
        res.send(err);
      }
      // var rowsCount = result.rowsAffected;
      sql.close();
      res.render('index', {
        route: 'home',
        data: result.recordset
      });

    }); // request.query
  }); // sql.conn
}); // get /
```

*   result.rowsAffected：取得的總筆數，與 result.recordset.legnth 相同
*   res.render：回傳方式帶入的樣板以及相關參數，index 就是 views / index.jade
*   route:'home'：回傳這個用意是為了讓 jade 方便判斷應載入的樣板
*   data：將取得的結果 result.recordset 指定給 data 變數

### 【views / layout.jade】

```javascript
doctype html
html
  head
    title Express With MSSQL
    link(href='/stylesheets/style.css', rel='stylesheet')
    link(href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css", rel="stylesheet")

  body
    h1 Express With MSSQL - #{route}
    p template by jade (Pug) 

    case route
      when 'home': block home
      when 'edit': block edit
      when 'add': block add
      default: block home
```

*   #{route}：從 res 回傳的變數中取得，在 jade（pug） 語法中，使用 #{ 變數 }，即可取出
*   補充上述：如果 element 沒有要塞入其他字串，則可寫成 →  h1=變數，就不需要 #{ 變數 }，例如：h1=route
*   case ... when ... default：此為 jade 語法中的條件式語法
*   block \[自訂名稱\]：此對應到 jade 檔案中，有 block \[自訂名稱\] 相同的區塊，與 ASP.NET MVC 中的 [section](http://www.cnblogs.com/willick/p/3410855.html) 之意相同

### 【views / index.jade】

```javascript
extends layout

block home
    label Total： #{data.length}
    hr
    a(href="/add", title="title").btn Add 
    table.list
      thead
        tr
          th UserName
          th UserID
          th Passwd
          th Email
          th 
      each item in data
        tr
          td= item.username
          td= item.userid
          td= Array(item.pwd.length + 1).join('*')
          td= item.email
          td  
            a(href="/edit/#{item.id}", title="Edit").icon
              i(aria-hidden="true").fa.fa-pencil-square
            a(href="/delete/#{item.id}", title="Delete" onclick="return confirm('Delete user： #{item.username} ?');").icon
              i(aria-hidden="true").fa.fa-trash
```

*   block home：呼應 layout.jade 中的 block home
*   each \[變數\] in \[陣列\]：即為我們熟悉的 for each
*   （補充）如何在 jade 中寫出帶有 attribute 或 class 的 element：  
        a( attribute=" 內容 " ).\[樣式\] \[文字內容\]  
        即為 <a attribute="內容"  class=\[樣式\] > \[文字內容\] </a>

### 啟動系統

為了方便系統 debug，建議可以使用套件 [nodemon](https://github.com/remy/nodemon)

[![687474703a2f2f6e6f64656d6f6e2e696f2f6e6f64656d6f6e2e737667](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/687474703a2f2f6e6f64656d6f6e2e696f2f6e6f64656d6f6e2e737667)](https://nodemon.io/)

全域安裝。

```bash
npm install -g nodemon
```

 安裝到當前專案，並列入 package.json 初始化安裝套件之一（即 npm install 時的安裝清單）。

```bash
npm install --save-dev nodemon
```

修改 package.json。

```javascript
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon ./bin/www"
  },
```

[![1495962264_00726.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495962264_00726.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495962264_00726.png)

執行吧~

```bash
npm run dev
```

[![1495962344_07088.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495962344_07088.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495962344_07088.png)

打開瀏覽器應該會是如下圖（畫面如有不同，應該是 css 樣式差異，本篇有提供[完整範例](https://github.com/explooosion/Node.js-Express-With-MSSQL)，css 可從此取得）

[http:localhost:3000](http://http:localhost:3000)

[![1495962442_39282.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495962442_39282.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495962442_39282.png)

實作 - Update
-----------

當點選首頁的編輯按鈕後（鉛筆圖案），會利用 get 方式到編輯頁面 http://localhost:3000/edit/id。

### 【routes / index.js】

```javascript
/* GET Edit page. */
router.get('/edit/:id/', function (req, res, next) {

  sql.connect(db, function (err) {
    if (err)
      console.log(err);

    var request = new sql.Request();
    request.input('id', sql.Int, req.params.id)
    request.query("select * from UserList where id=@id", function (err, result) {

      if (err) {
        console.log(err)
        res.send(err);
      }
      // var rowsCount = result.rowsAffected;
      sql.close();
      res.render('edit', {
        route: 'edit',
        data: result.recordset[0]
      });

    }); // request.query
  }); // sql.conn
});
```

*   我們利用 req.params.id，即可從網址列取得 id 參數
*   data：由於只會有一筆資料，因此我們直接回傳 result.recordset\[0\]

在 views / 底下新增檔案 edit.jade。

### 【views / edit.jade】

```javascript
extends layout

block edit
    label UserName： #{data.username}
    hr
    form(method='POST' action='/update')
        input(type="hidden" name="id" value=data.id)
        table.list-edit
            tr
                th UserID
                td=data.userid     
            tr
                th Passwd
                td
                    input(type="password" name="pwd" value=data.pwd).text
            tr
                th UserName
                td 
                    input(type="text" name="username" value=data.username).text
            tr
                th Email
                td
                    input(type="email" name="email" value=data.email).text
            tr
                td(colspan="2")
                    button(type="submit").btn Save
                    button(type="button" onclick="javascript: location.href='/'; ").btn Back
```

*   為了讓後端資料當前 id，暫時塞到 input hidden 中
*   form部分則會利用 post 方式到 /update

### 【routes / index.js】

```javascript
/* POST Edit page. */
router.post('/update', function (req, res, next) {

  sql.connect(db, function (err) {
    if (err)
      console.log(err);

    var request = new sql.Request();
    request.input('id', sql.Int, req.body.id)
      .input('username', sql.NVarChar(50), req.body.username)
      .input('pwd', sql.NVarChar(50), req.body.pwd)
      .input('email', sql.NVarChar(50), req.body.email)
      .query('update UserList set username=@username,pwd=@pwd,email=@email where id=@id', function (err, result) {

        if (err) {
          console.log(err);
          res.send(err);
        }
        sql.close();
        res.redirect('/');
      });
  });
});
```

*   由於資料從 form 過來，故使用 req.body 來取得表單欄位資料
*   更新完畢後直接利用 req.redirect('/')  重新導向至首頁

完成後切至畫面，當點選其中一筆資料時，就會順利地出現資料囉～

[http:localhost:3000](http://http:localhost:3000)　→　[http://localhost:3000/edit/2](http://localhost:3000/edit/2)

![1495963525_80201.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495963525_80201.png)

實作 - Insert
-----------

當點選首頁的新增按鈕後（add），會利用 get 方式到編輯頁面 http://localhost:3000/add。

### 【routes / index.js】

```javascript
/* GET Add page. */
router.get('/add', function (req, res, next) {
  res.render('add', {
    route: 'add',
  });
});
```

相關方法與 update 大同小異，至 veiws 底下新增 add.jade 。

### 【views / add.jade】

```javascript
extends layout

block add
    label Create
    hr
    form(method='POST' action='/add')
        table.list-edit
            tr
                th UserID
                td
                    input(type="text" name="userid").text
            tr
                th Passwd
                td
                    input(type="password" name="pwd").text
            tr
                th UserName
                td 
                    input(type="text" name="username").text
            tr
                th Email
                td
                    input(type="email" name="email").text
            tr
                td(colspan="2")
                    button(type="submit").btn Submit
                    button(type="button" onclick="javascript: location.href='/'; ").btn Back
```

當新增頁面提交後，會將表單 post 至後端。

### 【routes / index.js】

```javascript
/* POST Add page. */
router.post('/add', function (req, res, next) {

  sql.connect(db, function (err) {
    if (err)
      console.log(err);

    var request = new sql.Request();
    request.input('userid', sql.NVarChar(50), req.body.userid)
      .input('pwd', sql.NVarChar(50), req.body.pwd)
      .input('username', sql.NVarChar(50), req.body.username)
      .input('email', sql.NVarChar(50), req.body.email)
      .query('insert into UserList (userid, pwd, username, email) values (@userid, @pwd, @username, @email)', function (err, result) {

        if (err) {
          console.log(err);
          res.send(err);
        }
        sql.close();
        res.redirect('/');
      });
  });
});
```

實際畫面，應為空白，試著新增看看吧～

![1495963507_58112.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495963507_58112.png)

[![1495963487_91362.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495963487_91362.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495963487_91362.png)

實作 - Delete
-----------

還記得剛開始我們編寫樣板的時候，有寫到刪除的按鈕嗎～？

由於 href="/delete/id" 是 get 方法，因此在後端我們直接進行刪除，再重新導向回首頁即可。

### 【views / index.jade】

[![1495963731_84613.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495963731_84613.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495963731_84613.png)

### 【routes / index.js】

```javascript
/* GET Delete page. */
router.get('/delete/:id', function (req, res, next) {
  sql.connect(db, function (err) {
    if (err)
      console.log(err);

    var request = new sql.Request();
    request.input('id', sql.Int, req.params.id)
      .query('delete from UserList where id=@id', function (err, result) {

        if (err) {
          console.log(err);
          res.send(err);
        }
        sql.close();
        res.redirect('/');
      });
  });
});
```

實際畫面，點選垃圾桶，觸發 confirm() ，就可由 callback 決定是否繼續刪除了！

[![1495963956_92352.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495963956_92352.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/17f44570-1d97-4a9b-8fd8-786b6bb6ce6e/1495963956_92352.png)

本實作範本 + 資料表下載
-------------

範例存於小弟的 [Github](https://github.com/explooosion/Node.js-Express-With-MSSQL) [](https://github.com/explooosion/Node.js-Express-With-MySQL)

有提供資料庫，可先匯入。

![1495964604_10673.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-05-28_Node.js%20-%20Express%20%2B%20MSSQL/1495964604_10673.png)

專案 clone

```bash
git clone https://github.com/explooosion/Node.js-Express-With-MySQL.git
```

進入專案

```bash
cd express-mssql
```

安裝套件

```bash
npm install
```

使用 nodemon 執行（通常用於 debug）

```bash
npm install nodemon -g
npm run dev
```

也可使用 pm2 執行（通常用於正式發布）

```bash
npm install pm2 -g
npm start
npm stop
```

  
 

相關參考
----

[Github - node-msssql](https://github.com/patriksimek/node-mssql)

[npm mssql](https://www.npmjs.com/package/mssql)

[iT邦幫忙 - Day16 - Node.js 串接 MS-SQL Server](http://ithelp.ithome.com.tw/articles/10186139)

以上為簡單的 Node.js Express + MSSQL

有勘誤之處，不吝指教。ob'\_'ov