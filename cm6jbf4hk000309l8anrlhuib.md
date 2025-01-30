---
title: "Rust - 純白體驗只因你靠得住"
seoTitle: "Rust - 純白體驗只因你靠得住"
seoDescription: "本文適合純白初學者，想進一步認識 rust，歡迎閱讀 ..."
datePublished: Sun Jul 22 2018 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbf4hk000309l8anrlhuib
slug: rust
tags: rust

---

本文適合純白初學者，想進一步認識 rust，歡迎閱讀 ...

[![1*Hv_ATAMyCJbz4BRn58AX6g.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1*Hv_ATAMyCJbz4BRn58AX6g.png)](https://medium.com/mozilla-tech/why-rust-is-the-most-loved-language-by-developers-666add782563)

*   [Why Rust is the Most Loved Language by Developers](https://medium.com/mozilla-tech/why-rust-is-the-most-loved-language-by-developers-666add782563)

站住！你沒點錯！

只是想說最近很夯撩妹語錄 ... 🤣

最近又被 [Rust](https://www.rust-lang.org/en-US/) 撩到，只好來學學了！

本系列為閱讀相關文章後的學習心得整理，

這篇僅為基本介紹及環境安裝﹑指令使用。

而筆者為前端工程師，因此在撰寫風格與介紹思維上，

會多以前端角度介紹 ~

### 目錄：

1.  [前言](#1)
2.  [環境準備](#2)
3.  [建立第一個專案](#3)
4.  [使用 Cargo 建立專案](#4)
5.  [結論](#5)
6.  [參考資料](#6)

**一、前言**
--------

[Rust](https://www.rust-lang.org/en-US/) 算起來是萌新語言，讓我們先認識他的 LOGO：

![ra%2Cunisex_tshirt%2Cx925%2C101010%3A01c5ca27c6%2Cfront-c%2C217%2C190%2C210%2C230-bg%2Cf8f8f8.lite-1.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/ra%252Cunisex_tshirt%252Cx925%252C101010%253A01c5ca27c6%252Cfront-c%252C217%252C190%252C210%252C230-bg%252Cf8f8f8.lite-1.jpg)

欸......不是這張，差點傳教了。

#### RUST

![rust-logo-mozilla.jpg](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/rust-logo-mozilla.jpg)

最早他是由 [Mozilla](https://zh.wikipedia.org/zh-tw/Mozilla) 所主導的，而在官網可以看到這句 Slogan：

> #### Rust is a systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.

Rust 具備了速度﹑安全等特性理念，設計原則為「安全，並行，速度」，

他不需要透過 [GC](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science))，就可以達成他的目標理念。

大多用於大型的專案伺服器架構，他寫起來有點像 C++，又有點像 JavaScript，

環境的設定使用上，也與 [Node.js](https://nodejs.org/en/) 同有親切感（個人覺得相似）。

因為原設計者就是 [Brendan Eich](https://zh.wikipedia.org/zh-tw/%E5%B8%83%E8%98%AD%E7%99%BB%C2%B7%E8%89%BE%E5%85%8B) ( JavaScript 之父 )    😍 **啊 啊 啊 啊 ！！！！ ❤** 

讓我們先來淺嚐一下程式碼：

![1532237200_30404.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532237200_30404.png)

*   **fn**：就是我們熟悉的 function。
*   **main**：為主程式進入點。
*   **println**：就是 console.log 啦，用法與 C 會比較相近。

是不是感到很優美呢 ～～

![1532237581_51468.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532237581_51468.gif)

**二、環境準備**
----------

### **Rust 安裝**

筆者是 Windows 系統，對於其他環境 ... 請讀者們自行[觀落陰](https://zh.wikipedia.org/zh-tw/%E8%A7%80%E8%90%BD%E9%99%B0)了！ 👻

首先安裝 [Rust](https://www.rust-lang.org/en-US/install.html)，在官網可以直接[下載](https://win.rustup.rs)：

![1532237943_08144.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532237943_08144.png)

安裝完畢後，開啟終端機試著輸入：

```bash
rustc --version
```

![1532243811_22509.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532243811_22509.png)

以及：

```bash
cargo --version
```

![1532243821_19532.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532243821_19532.png)

出現版本資訊後表示環境安裝成功～

rustc 為 rust 的指令別名，而 cargo 則適用於管理環境套件的指令，

![Cargo-Logo-Small-c39abeb466d747f3be442698662c5260.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/Cargo-Logo-Small-c39abeb466d747f3be442698662c5260.png)

官方網址：[crates.io](https://crates.io/)

你可以想成 node.js 的 node 之於 npm。

對於想要更新或移除，使用 rustup 就可以控管，例如更新 rust：

```bash
rustup update
```

你可以想成 node.js 的 nvm。

如果你想從 node.js 角度去更加了解認識 rust，不妨看看這個專案：

*   [Rust for Node developers](https://github.com/Mercateo/rust-for-node-developers)

### IDE 安裝

筆者使用 [Visual Studio Code](https://code.visualstudio.com/) ( [點我下載](https://code.visualstudio.com/docs/?dv=win) )，

![1200px-Visual_Studio_Code_1.18_icon.svg.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1200px-Visual_Studio_Code_1.18_icon.svg.png)

也可使用別的編輯器或是 [Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads/)。

如果你選擇 vscode，可以安裝以下兩個 extension：

*   [vscode-rust-syntax](https://marketplace.visualstudio.com/items?itemName=dunstontc.vscode-rust-syntax)
*   [rls](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust)

在安裝 rls 之前，建議先執行以下指令，

如果忘了執行也沒關係，在安裝擴充套件的時候會自動安裝：

```bash
rustup update
```
```bash
rustup component add rls-preview rust-analysis rust-src
```

![1532239245_44681.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532239245_44681.png)

**三、建立第一個專案**
-------------

### **撰寫程式**

首先我們建立專案資料夾，隨意命名，方便整理而已，

筆者任意取一個為 hello 的資料夾，接著建立一份主程式檔案，命名 main.rs。

![1532238951_55692.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532238951_55692.png)

在 Rust 中，副檔名固定為 rs 結尾。

![1532240377_07007.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532240377_07007.png)

vscode 檔案主題 icon 使用 [vscode-icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)

接著輸入以下程式碼：

\[ main.rs \]

```go
fn main() {
    println!("Hello, world!");
}
```

*   **fn**：就是常見的 function。
*   **main**：所有程式的起始點，類似 C﹑C#﹑Java 等。
*   **println**：將文字印到螢幕上，不過這裡的「！」比較特別，他是巨集（[macro](http://askeing.github.io/rust-book/macros.html)），這裡暫不討論。
*   由於筆者 JS 屬於... 不寫「；」派系，在這裡要特別注意ＱＱ，一定要寫！！！

在縮排的部分，使用四個空格，不過其實不用擔心，如果你使用 vscode 也有安裝 [rls](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust)，

只要輸入組合鍵 Shift \+ Alt \+ F，就可以自動排版啦～

![1532239835_74153.gif](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532239835_74153.gif)

### 編譯並執行程式

在 vscode 中，可以透過Ctrl \+ \`呼叫出終端機。

我們開啟終端機，輸入指令編譯程式：

```bash
rustc main.rs
```

完成後應該會出現如下兩個檔案。

![1532241052_39391.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532241052_39391.png)

接著我們輸入指令執行：

```bash
main
```

![1532241109_59243.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532241109_59243.png)

如果你是 Windows 系統，那麼這裡的 main 其實等於 main.exe。

**四、使用 Cargo 建立專案**
-------------------

### **初始專案**

在 rust 中的 cargo，跟 node.js 的 npm 很像，

大部分都是使用 cargo 進行專案建置與管理。

我們透過 cargo 指令 new 建立新專案名為 world ：

```bash
cargo new world
```

*   **cargo new**：建立一個包含 cargo 檔案的專案產生指令

其實就跟 npm 的初始指令 npm init 同道理。

建立完畢後可以看到以下目錄結構：

![1532241704_24627.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532241704_24627.png)

*   **src**：main.rc 預設在 src 資料夾中的主程式進入檔案。
*   **.gitignore**：還很貼心地幫我們初始 git。
*   **Cargo.toml**：內容描述了專案的名稱﹑版本以及依賴套件等，同我們熟悉的 package.json。

不懂 Git 的朋友可以看看這系列 - [連猴子都能懂的Git入門指南](https://backlog.com/git-tutorial/tw/intro/intro1_1.html)

### 編譯專案

接著輸入指令 cargo build 編譯：

```bash
cargo build
```

[![1532242066_45383.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532242066_45383.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/96c1c3d4-5b93-48d2-ac22-0078efaf74c8/1532242066_45383.png)

完成後可以看到目錄有更多檔案了！

![1532242336_87911.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532242336_87911.png)

*   target：該目錄就是編譯後的資料夾。​
*   Cargo.lock：其實用途等同於 [package-lock.json](https://docs.npmjs.com/files/package-lock.json)

### 執行專案

上續動作都沒問題了話，就可以輸入 cargo run 執行程式：

```bash
cargo run
```

[![1532242300_29624.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2018-07-22_Rust%20-%20%E7%B4%94%E7%99%BD%E9%AB%94%E9%A9%97%E5%8F%AA%E5%9B%A0%E4%BD%A0%E9%9D%A0%E5%BE%97%E4%BD%8F/1532242300_29624.png)](https://dotblogsfile.blob.core.windows.net/user/incredible/96c1c3d4-5b93-48d2-ac22-0078efaf74c8/1532242300_29624.png)

※. 結論
-----

以上章節介紹了安裝與環境建置，對於指令的操作相信也更熟悉了！

本文主要將相關資源重新整理用自己的思維分享，

如果有興趣學習下去，不妨閱讀看看參考資料吧！

※. 參考資料
-------

*   [The Rust Programming Language](https://doc.rust-lang.org/book/second-edition/foreword.html)
    
*   [Why Rust is the Most Loved Language by Developers](https://medium.com/mozilla-tech/why-rust-is-the-most-loved-language-by-developers-666add782563)
    
*   [Rust and the Future of Systems Programming](https://medium.com/mozilla-tech/rust-and-the-future-of-systems-programming-b75fba746910)
    
*   [Rust语言教程(1) - 一门没有GC的语言](https://www.jianshu.com/p/67c94459997a)
*   [Rust 程序设计语言（第二版） 简体中文版](https://kaisery.gitbooks.io/trpl-zh-cn/content/)
    
*   [Rust 程式語言](http://askeing.github.io/rust-book/README.html#Rust%20%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80)
    
*   [Rust 維基百科，自由的百科全書](https://zh.wikipedia.org/wiki/Rust)
    
*   [Node Love Rust](https://cnodejs.org/topic/593353775b07c1b24afa0638)
    
*   [Rust for Node developers](https://github.com/Mercateo/rust-for-node-developers)
    
*   [Actix - a Rust actors framework](https://github.com/actix/actix)
    

有勘誤之處，不吝指教。ob'\_'ov