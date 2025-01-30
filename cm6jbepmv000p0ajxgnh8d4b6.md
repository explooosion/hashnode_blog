---
title: "ASP.NET - UpdatePanel and JQuery Dialog Problem"
seoTitle: "ASP.NET - UpdatePanel and JQuery Dialog Problem"
seoDescription: "當你使用 UpdatePanel 以及 JQuery Dialog 發生怪異失效時..."
datePublished: Wed Sep 28 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbepmv000p0ajxgnh8d4b6
slug: aspnet-updatepanel-and-jquery-dialog-problem

---

當你使用 UpdatePanel 以及 JQuery Dialog 發生怪異失效時...

本篇於 asp.net 環境使用 DropDownList 時候，

發現無論如何設定，都無法觸發 OnSelectedIndexChanged，

起初找到要配合 UpdatePanel，而後又發現仍無法解決，

因為筆者的 UserControl 是基於 JQuery Dialog 上，

故問題牽涉到 **jquery** 上了！！！　_（摁...颱風天剛好碰到這問題，差點崩潰）_

解決方式
----

直接於 dialog 開啟的時候進行修改 javascript。

完全不需要動到 asp.net 的檔案！！！

原本

```javascript
$("#dialog").dialog("open");
```

修改

```javascript
$("#dialog").dialog("open").parent().appendTo($("form:first"));
```

後記
--

太難過啦 QQ 

是因為太感動了，這問題卡很久，相信你也能感同身受吧！！

參考資料：

[update panel inside jquery dialog div not working \[duplicate\]](http://stackoverflow.com/questions/16559629/update-panel-inside-jquery-dialog-div-not-working)

有勘誤之處，不吝指教。ob'\_'ov