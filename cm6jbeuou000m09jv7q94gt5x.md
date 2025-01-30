---
title: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［0］獻上祝福的轉生"
seoTitle: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［0］獻上祝福的轉生"
seoDescription: "記錄著從 Vue 新手村出發的練功歷程..."
datePublished: Fri Jul 28 2017 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbeuou000m09jv7q94gt5x
slug: vuejs-20-vue-0
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB0%EF%BC%BD%E7%8D%BB%E4%B8%8A%E7%A5%9D%E7%A6%8F%E7%9A%84%E8%BD%89%E7%94%9F/banner/0001577645.JPG
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB0%EF%BC%BD%E7%8D%BB%E4%B8%8A%E7%A5%9D%E7%A6%8F%E7%9A%84%E8%BD%89%E7%94%9F/banner/0001577645.JPG
tags: vue

---

記錄著從 Vue 新手村出發的練功歷程...

學習框架是一件令人頭痛又興奮的事情，有種種可能原因：

1.  沒有接觸過前端框架
2.  要捨棄先前使用框架的經驗
3.  對於自主學習研究並不擅長
4.  技術更新太快跟不上節奏

一、前言
----

最近個人在自我學習，挑選了目前主流之一的前端框架 [Vue.JS](https://vuejs.org/)，

本篇為個人學習歷程，同時希望寫成一系列的文章，

以最最最新手的介紹方式，跟大家「**分享**」如何使用，

這個系列個人希望以「認識」的角度去學習，

而不是那種希望在幾周內學會，然後快速上手上戰場，最後有一堆搞不完的 bug。

如果是白手起家拓荒者，本人推薦這篇文章：[PTT - Soft\_Job \[心得\] 前端入門心得](https://www.ptt.cc/bbs/Soft_Job/M.1453137664.A.52D.html)

自我學習是一件很奧妙的事情，「學習但不代表一定要使用它」，

很多框架都有相同的地方，我們只要取得他的精隨理念、設計模式就足夠了！

在這之前，這個標題可能有些人很熟悉，

主要其實是來自：[《帶著智慧型手機闖蕩異世界》](https://zh.wikipedia.org/wiki/%E5%B8%B6%E8%91%97%E6%99%BA%E6%85%A7%E5%9E%8B%E6%89%8B%E6%A9%9F%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%E3%80%82)[．](http://myself-bbs.com/thread-42760-1-1.html)

[![0001577645.JPG](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB0%EF%BC%BD%E7%8D%BB%E4%B8%8A%E7%A5%9D%E7%A6%8F%E7%9A%84%E8%BD%89%E7%94%9F/0001577645.JPG)](https://p2.bahamut.com.tw/M/2KU/45/0001577645.JPG)

Q：為什麼要選擇它來作為本標題相似的系列呢？

A：因為主角適應性很強，別人只能學習少樣屬性技能，但他卻可以學習所有屬性，

　　所以希望大家也能夠無視框架的不同，然後能順心的打遍天下！_（這明明是主角外掛吧！？_

如果你對於現有能力感到茫然，不知該如何下手，

可以試著閱讀本系列文章。

[![1501228900_30443.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB0%EF%BC%BD%E7%8D%BB%E4%B8%8A%E7%A5%9D%E7%A6%8F%E7%9A%84%E8%BD%89%E7%94%9F/1501228900_30443.jpg)](https://dotblogsfile.blob.core.windows.net/user/incredible/da44a4ff-aecd-4ccc-9062-a55f1a6b58e8/1501228900_30443.jpg)

同時也會以淺顯易懂的方式，記錄著個人的學習歷程。

[![1501228905_27399.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB0%EF%BC%BD%E7%8D%BB%E4%B8%8A%E7%A5%9D%E7%A6%8F%E7%9A%84%E8%BD%89%E7%94%9F/1501228905_27399.jpg)](https://dotblogsfile.blob.core.windows.net/user/incredible/da44a4ff-aecd-4ccc-9062-a55f1a6b58e8/1501228905_27399.jpg)

二、風格指引
------

為了讓大家比較好理解，個人希望以不同的手法表達，以下幾點說明：

1.  可能會有點宅宅的味道_（爽喇！_
2.  圖文並茂
3.  重點處以黃色標記
4.  可能會有部分顏文字
5.  具有連結的文字都是 [\_blank](http://www.w3school.com.cn/html5/att_a_target.asp) 效果
6.  閱讀視角以進入遊戲世界內為主
7.  有點中二_（臭 87 的感覺_

三、開始吧
-----

讓我們開始吧．．．！

![1483618782-3554651433.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB0%EF%BC%BD%E7%8D%BB%E4%B8%8A%E7%A5%9D%E7%A6%8F%E7%9A%84%E8%BD%89%E7%94%9F/1483618782-3554651433.png)

### Next Stop：

### [Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［1］醒來便是異世界](https://dotblogs.com.tw/explooosion/2017/07/28/024451)

有勘誤之處，不吝指教。ob'\_'ov