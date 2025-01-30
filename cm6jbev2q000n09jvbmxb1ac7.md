---
title: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［1］醒來便是異世界"
seoTitle: "Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［1］醒來便是異世界"
seoDescription: "記錄著從 Vue 新手村出發的練功歷程..."
datePublished: Fri Jul 28 2017 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbev2q000n09jvbmxb1ac7
slug: vuejs-20-vue-1
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/banner/logo.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/banner/logo.png
tags: vue

---

記錄著從 Vue 新手村出發的練功歷程...

本篇任務指引：
-------

1.  認識世界（M）
2.  購買裝備（I）
3.  學習魔法（K）

**一、初次來到異世界**
-------------

剛醒來到 Vue 的世界，先打開地圖 （M） ，了解一下世界外觀：

[![logo.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/logo.png)](https://cn.vuejs.org/)

[尤雨溪](http://baike.baidu.com/item/%E5%B0%A4%E9%9B%A8%E6%BA%AA/2281470?fr=aladdin)是 Vue.js 的作者，

總得要熟悉一下造物者面孔：_（哪天相遇就可以要簽名_[![1501178758_40127.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/1501178758_40127.png)](https://baike.baidu.com/item/%E5%B0%A4%E9%9B%A8%E6%BA%AA/2281470?fr=aladdin)

看起來很年輕也很帥呢！

![1501336243_22608.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/1501336243_22608.png)

那麼這個世界嚮往著什麼呢？_（太懶了直接截圖）_

[![1501178848_79669.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/1501178848_79669.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/b3a5ebcb-c115-404f-aee9-a76df0434f7a/1501178848_79669.png)

我們可以推得：

作者厭倦了世俗的繁瑣，現世過於複雜龐大，

因此決定要創造出理想的伊甸園，讓居民能夠身處世外桃源。

Vue.js 跟許多框架都一樣，希望以堆積木的方式，重複使用既有的元件，

下圖這張為官方所繪製的，網頁實際上切割成很多塊，

圖中相同形狀的積木就是同一類組建，

同樣的組件可以重複使用，而不用重新建造，

而展開後就像右邊的樹狀圖一樣，是具有層次順序的樹狀結構。

[![components.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/components.png)](https://cn.vuejs.org/v2/guide/)

**二、總不能穿著睡衣**
-------------

新手村的你可能需要買一點裝備才能出城，以下為推薦的裝備：

1.  能夠使用魔法的媒介：[Visual Studio Code](https://code.visualstudio.com/)
2.  通用基礎魔法語言：[從ES6開始的JavaScript學習生活](https://eyesofkids.gitbooks.io/javascript-start-from-es6/)
3.  可以進行實驗的容器：[Chrome](https://www.google.com.tw/chrome/browser/desktop/index.html)
4.  適度的放鬆有助於學習：[Spotify](https://www.spotify.com/tw/)
5.  從造物者偷來的文件：[Vue.JS](https://cn.vuejs.org/v2/guide/)

如果以上都準備好環境了，我們就可以出城打[波利](http://gametsg.techbang.com/ro/index.php?view=npc&npc=1002)了

![8ffdcd443dec51ce205a647c4249278f.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2017-07-28_Vue.js%202.0%20-%20%E5%B8%B6%E8%91%97%20Vue%20%E6%A1%86%E6%9E%B6%E9%97%96%E8%95%A9%E7%95%B0%E4%B8%96%E7%95%8C%20-%20%EF%BC%BB1%EF%BC%BD%E9%86%92%E4%BE%86%E4%BE%BF%E6%98%AF%E7%95%B0%E4%B8%96%E7%95%8C/8ffdcd443dec51ce205a647c4249278f.png)

### Next Stop：

### [Vue.js 2.0 - 帶著 Vue 框架闖蕩異世界 - ［2］環境建置的前哨](https://dotblogs.com.tw/explooosion/2017/07/28/150538)

有勘誤之處，不吝指教。ob'\_'ov