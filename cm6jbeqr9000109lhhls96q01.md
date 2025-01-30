---
title: "Node.js - Faker 製作假資料"
seoTitle: "Node.js - Faker 製作假資料"
seoDescription: "本篇教學快速建立 json 格式之假資料。"
datePublished: Mon Oct 10 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbeqr9000109lhhls96q01
slug: nodejs-faker
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-10_Node.js%20-%20Faker%20%E8%A3%BD%E4%BD%9C%E5%81%87%E8%B3%87%E6%96%99/banner/1476080770_62409.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-10_Node.js%20-%20Faker%20%E8%A3%BD%E4%BD%9C%E5%81%87%E8%B3%87%E6%96%99/banner/1476080770_62409.png
tags: lodash

---

本篇教學快速建立 json 格式之假資料。

當前端在刻畫一些畫面時，總需要資料才能得以測試，

倘若後端的同事尚未開發完成，往往會造成開發上的延遲，

為了加速開發，我們可以利用 **[Faker](https://github.com/stympy/faker)** 快速產出指定格式之 json 資料。

一、環境安裝
------

首先請先下載建立於 Ruby上的套件管理器 [GEM](https://rubygems.org/pages/download?locale=zh-TW) ( 如同 npm 套件管理之於 node )，

完成安裝後，開啟 Ruby CMD 。

![1476080770_62409.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-10_Node.js%20-%20Faker%20%E8%A3%BD%E4%BD%9C%E5%81%87%E8%B3%87%E6%96%99/1476080770_62409.png)

下載 Faker 套件。

```ruby
gem install faker
```

通常會出現以下 SSL 驗證錯誤

[![1476080949_14304.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-10_Node.js%20-%20Faker%20%E8%A3%BD%E4%BD%9C%E5%81%87%E8%B3%87%E6%96%99/1476080949_14304.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/299cbb43-aa29-4f37-98be-8c966870bec7/1476080949_14304.png)

因為 Ruby 未包含驗證，故在 gem 服務上未通過  https 驗證，

處理方式請先至此 [cacert.pem](https://curl.haxx.se/ca/cacert.pem) 下載驗證，並在電腦上新增環境變數。

```bash
環境變數：SSL_CERT_FILE
檔案來為：C:\path\to\cacert.pem
```

![1476081197_98354.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-10_Node.js%20-%20Faker%20%E8%A3%BD%E4%BD%9C%E5%81%87%E8%B3%87%E6%96%99/1476081197_98354.png)

[![1476081254_3271.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-10_Node.js%20-%20Faker%20%E8%A3%BD%E4%BD%9C%E5%81%87%E8%B3%87%E6%96%99/1476081254_3271.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/299cbb43-aa29-4f37-98be-8c966870bec7/1476081254_3271.png)

完成後確定並重開或登出電腦，如此一來 gem 即可使用。

```ruby
gem install faker
```

[![1476081533_70433.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-10_Node.js%20-%20Faker%20%E8%A3%BD%E4%BD%9C%E5%81%87%E8%B3%87%E6%96%99/1476081533_70433.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/299cbb43-aa29-4f37-98be-8c966870bec7/1476081533_70433.png)

二、建立測試專案
--------

```bash
mkdir myfaker
```
```bash
cd myfaker
```
```bash
npm init
```
```bash
npm install faker
```

這時應該可以看到我們的 node\_modules 內多了 faker 資料夾，

為了快速建立亂數以及定義範圍，我們也安裝 [lodash](https://lodash.com/)。

```bash
npm install lodash
```

三、撰寫測試檔案
--------

建立一個檔案 fakerdata.js，檔名任意，此檔為產出 json 之用。

```javascript
var faker = require('faker');
var fs = require('fs');
var _ = require('lodash');
```

*   faker：產出假資料用
*   fs：將 json 資料匯出成 .json
*   lodash：產生亂數以及範圍數

```javascript
var range = _.range(1,5);
var data = [];
faker.locale = 'zh_TW';
```

*   range：欲產出之總筆數
*   data：存放總資料
*   faker.locale：產出資料之語言 (可使用的語言定義於 node\_modules\\faker\\lib\\locales\\ )

```javascript
range.map(index => {


    
});
```

*   建立一個 map ，依據 range 所定義之長度，進行迴圈 （不是 google map 唷）。

```javascript
range.map(index => {

    var name = faker.name.findName();

    var json = {
        name: {
            full: name,
            first: name.split(' ')[0],
            last: name.split(' ')[1],
        },
        job: {
            type: faker.name.jobType(),
            name: faker.name.jobTitle(),
            description: faker.name.jobDescriptor(),
        },
        age: _.random(18, 80, false),
    };
    
    data.push(json);
});
```

*   faker.name 中產出姓名、職稱等等
*   年齡利用 lodash 產出

```javascript
fs.writeFile('./data.json', JSON.stringify(data), function () {
        console.log('create faker data success!');
    });
```

*   最後於外層編寫 fs.writeFile，將 data 資料轉為 JSON 格式 

完整程式碼

```javascript
var faker = require('faker');
var fs = require('fs');
var _ = require('lodash');

var range = _.range(1, 5);

faker.locale = 'zh_TW';

var data = [];

range.map(index => {

    var name = faker.name.findName();

    var json = {
        name: {
            full: name,
            first: name.split(' ')[0],
            last: name.split(' ')[1],
        },
        job: {
            type: faker.name.jobType(),
            name: faker.name.jobTitle(),
            description: faker.name.jobDescriptor(),
        },
        age: _.random(18, 80, false),
    };

    data.push(json);
});

fs.writeFile('./data.json', JSON.stringify(data), function () {
    console.log('create faker data success!');
});
```

四、產出資料
------

完成後即可於專案目錄底下看到 data.json  資料。

```bash
node fakerdata.js
```

參考資料：**[ReactNativeDay12](https://github.com/horsekitlin/ReactNativeDay12) -** 台中前端社群 10/08 特別聚會 @夢種子

有勘誤之處，不吝指教。ob'\_'ov