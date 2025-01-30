---
title: "ASP.NET - Microsoft.ACE.OLEDB.12.0 提供者並未登錄於本機電腦上"
seoTitle: "ASP.NET - Microsoft.ACE.OLEDB.12.0 提供者並未登錄於本機電腦上"
seoDescription: "使用 asp.net 讀取 access 時所發生之問題。"
datePublished: Fri Sep 30 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbepy4000f09jvbxozftoh
slug: aspnet-microsoftaceoledb120
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-09-30_ASP.NET%20-%20Microsoft.ACE.OLEDB.12.0%20%E6%8F%90%E4%BE%9B%E8%80%85%E4%B8%A6%E6%9C%AA%E7%99%BB%E9%8C%84%E6%96%BC%E6%9C%AC%E6%A9%9F%E9%9B%BB%E8%85%A6%E4%B8%8A/banner/1475204589_45152.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-09-30_ASP.NET%20-%20Microsoft.ACE.OLEDB.12.0%20%E6%8F%90%E4%BE%9B%E8%80%85%E4%B8%A6%E6%9C%AA%E7%99%BB%E9%8C%84%E6%96%BC%E6%9C%AC%E6%A9%9F%E9%9B%BB%E8%85%A6%E4%B8%8A/banner/1475204589_45152.png

---

使用 asp.net 讀取 access 時所發生之問題。

當我們使用 asp.net 讀取資料庫時，一般我們都是連接 MSSQL

並引用 SqlClient 進行讀取

```cs
using System.Data.SqlClient;
```

倘若我們要讀取 **Access(2010)** 的時候，便會引用 OleDb

```cs
using System.Data.OleDb;
```

錯誤訊息
----

而在引用 OleDb 後，通常第一次使用會發生伺服器錯誤

「Microsoft.ACE.OLEDB.12.0 提供者並未登錄於本機電腦上」

[![1475204589_45152.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2016-09-30_ASP.NET%20-%20Microsoft.ACE.OLEDB.12.0%20%E6%8F%90%E4%BE%9B%E8%80%85%E4%B8%A6%E6%9C%AA%E7%99%BB%E9%8C%84%E6%96%BC%E6%9C%AC%E6%A9%9F%E9%9B%BB%E8%85%A6%E4%B8%8A/1475204589_45152.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/bf44662f-d2dd-4f8d-a380-9ddc1574366b/1475204589_45152.png)

處理方式
----

此一問題為基於未安裝 Access Database Engine 2010 之驅動程式。

至官方下載套件即可：**[Microsoft Access Database Engine 2010 可轉散發套件](https://www.microsoft.com/zh-tw/download/details.aspx?id=13255)**

安裝注意事項

倘若主機為 32 bit，安裝對應之 32 bit 套件即可；若為 64bit，務必兩者皆安裝，

在 64bit 安裝兩者時將發生以下訊息：

**由於目前你已經安裝32位元的office產品，因此無法安裝64位元版本的Microsoft Access Database Engine 2010，**

**若要安裝64位元的版本，請先除32位元的office產品**

此時我們透過 cmd 安裝即可避免此問題，

首先開啟 「命令提示字元Cmd」，切換至安裝檔目錄底下：

```bash
AccessDatabaseEngine_X64.exe /passive
```

跳過一閃的執行畫面即為完成安裝！

參考資料：[德瑞克：SQL Server 學習筆記](http://sharedderrick.blogspot.tw/2013/04/access-database-engine-2010-64-32.html)

有勘誤之處，不吝指教。ob'\_'ov