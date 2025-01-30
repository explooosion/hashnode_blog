---
title: "IIS - HTTP 錯誤 500.21 - Internal Server Error"
seoTitle: "IIS - HTTP 錯誤 500.21 - Internal Server Error"
seoDescription: "在 iis 上建立 webservice 所發生之錯誤訊息。"
datePublished: Mon Oct 03 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbeqbd000f09lbfqlwfz8u
slug: iis-http-50021-internal-server-error
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-03_IIS%20-%20HTTP%20%E9%8C%AF%E8%AA%A4%20500.21%20-%20Internal%20Server%20Error/banner/456.jpg
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-03_IIS%20-%20HTTP%20%E9%8C%AF%E8%AA%A4%20500.21%20-%20Internal%20Server%20Error/banner/456.jpg
tags: error, server

---

在 iis 上建立 webservice 所發生之錯誤訊息。

在 IIS 上建立 Webservice 的時候，倘若發生此錯誤訊息

HTTP 錯誤 500.21 - Internal Server Error

此一問題屬 IIS 環境套件安裝問題

[![456.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-03_IIS%20-%20HTTP%20%E9%8C%AF%E8%AA%A4%20500.21%20-%20Internal%20Server%20Error/456.jpg)](http://1.bp.blogspot.com/-ou3bHQLJNPI/UHYdT1atBzI/AAAAAAAAA3Q/I7IQp14ZOkg/s1600/456.jpg)

解決方式
----

```
%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -i
```

若使用 **v2.0.50727** 版（或其他版本），則切換至該目錄底下即可。

```
%windir%\Microsoft.NET\Framework\v2.0.50727\aspnet_regiis.exe -i
```

成功訊息
----

![1475481139_71648.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-10-03_IIS%20-%20HTTP%20%E9%8C%AF%E8%AA%A4%20500.21%20-%20Internal%20Server%20Error/1475481139_71648.png)

參考資料：[IIS HTTP 錯誤 500.21 - Internal Server Error 0x80070002](http://marco.easyusing.com/2012/10/iis-http-50021-internal-server-error.html)

有勘誤之處，不吝指教。ob'\_'ov