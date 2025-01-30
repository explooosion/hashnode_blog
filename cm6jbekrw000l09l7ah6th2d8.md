---
title: "CSS - calc 計算應用"
seoTitle: "CSS - calc 計算應用"
seoDescription: "css3 之 calc 計算功能，請安心服用。"
datePublished: Fri Jun 03 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbekrw000l09l7ah6th2d8
slug: css-calc
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-03_CSS%20-%20calc%20%E8%A8%88%E7%AE%97%E6%87%89%E7%94%A8/banner/1464920633_34396.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-03_CSS%20-%20calc%20%E8%A8%88%E7%AE%97%E6%87%89%E7%94%A8/banner/1464920633_34396.png
tags: css3, css

---

css3 之 calc 計算功能，請安心服用。

如果今天要寫出格子狀的樣式，

除了要計算每個小格子寬度外，還要計算它的間距。

但是難免會有小數點算不完的情形，

這時可用 CSS3 中的 calc 去進行算數運算。

【calc支援說明】 
-----------

**瀏覽器**

IE10+、Firefox4+、Chrome19+、Safari6+

**運算**

\+ - \* /

**單位**

px、em、rem、%

**計算**

複合式計算

以下範例可呈現出圖中效果，

每個小格子大小及其間距都相同。

![1464920633_34396.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-06-03_CSS%20-%20calc%20%E8%A8%88%E7%AE%97%E6%87%89%E7%94%A8/1464920633_34396.png)

靠左浮動排列
------

```css
.box{
  float: left;
}
```

寬高設定
----

切成三等份，並扣除 10px 留給間距。

```css
.box{
  width: calc(100%/3 - 10px);
  height: calc(100%/3 - 10px);
}
```

間距設定
----

```css
.box{
  margin-left: calc(5px * 3 / 2);
  margin-top: calc(5px * 3 / 2);
}
```

程式結果
----

[CodePen](http://codepen.io/ta7382/pen/vKONVg)

參考資訊
----

[MINWT](http://www.minwt.com/webdesign-dev/css/11583.html)

有勘誤之處，不吝指教。ob'\_'ov