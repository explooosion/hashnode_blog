---
title: "Git - 在工作與私人專案中來回切換 SSH"
datePublished: Sat Jul 08 2023 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6j2ygjt000c08jx08gp04ii
slug: git
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1738226127295/bd15b3d0-129b-4171-910e-7ae352a5f799.png

---

 

將 SSH 分不同的帳號配置！

在悠閒的假日，最快樂的便是探索新技能～

![1688807175.png.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1738226120980/a05bc7a0-231e-4ee5-9bcd-8f37b67716ad.png)

前言
--

筆者 MacBook 拿來混雜工作與私人開發用，

因此經常有不同的 Repository 須對應不同的 Github Account。

如果沒設定好 SSH，就會被終端機嗆：

    ERROR: Permission to explooosion/nuxt3-boilerplate.git denied to robbywu-work.
    fatal: Could not read from remote repository.

每次在新環境都需要重新配置，

也…時常遺忘作法，所以這次將流程紀錄起來！

### 注意事項

1.  文章筆者分為 Personal 與 Work 的情境建置
2.  筆者開發環境使用 macOS

**0.環境檢查**
----------

可以先檢查自己電腦是否已經存在一些 git 使用的 SSH，

在 `~/.ssh/`目錄下檢查是否存在以下兩個檔案（類似）：

*   `id_rsa`（私鑰）
*   `id_rsa.pub`（公鑰）

如果已經存在，可以選擇刪除重新來過，

或者跳過 `1.建置金鑰`，直接到 `2.SSH 設定檔`。

**1.建置金鑰**
----------

### 1.1 私人用

新增 SSH，輸入指令。

    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

*   請將`your_email@example.com` 改為自己的私人電子郵件

輸入上述指令建立檔案與名稱時，會提示你儲存檔案。

    Generating public/private rsa key pair.
    Enter file in which to save the key (/Users/robbymac/.ssh/id_rsa): id_personal

*   可設定自己喜歡的名字。例如：`id_personal`

添加 SSH 金鑰到 SSH 代理，輸入指令。

    ssh-add ~/.ssh/id_personal

*   請指向自己的檔案路徑與名稱

複製公鑰，輸入指令。

稍後我們便可以貼到 [Github - Settings - SSH keys](https://github.com/settings/keys) 上。

    pbcopy < ~/.ssh/id_personal.pub

*   請記得要複製公鑰`.pub`
*   建立 SSH 時會自動產生私鑰匙與公鑰，公鑰預設檔名為`[私鑰].pub`

在 GitHub 上添加 SSH 金鑰，選擇 New SSH key。

[![1688804448.png.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1738226122389/8775d609-f710-419b-842b-41beeed4eaaf.png)](https://dotblogsfile.blob.core.windows.net/user/robby/6298370b-3532-4c06-ada5-677501cbfb78/1688804448.png.png)

將剛剛透過 pbcopy 指令複製的公鑰，貼到 key，並適當取一個你好識別裝置的金鑰。

*   Key type不需要變更，預設Authentication Key

![1688804478.png.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1738226123865/1543bfef-f099-4687-927f-ce496d5ee05d.png)

測試 SSH 連接，輸入指令。

    ssh -T git@github.com

![1688804743.png.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1738226125149/3f0b0927-a7f7-41ae-bdcd-51700f8106ba.png)

### 1.2 工作用

參照 「1.1 私人專案金鑰」，建立一組金鑰 id\_work、id\_work.pub

步驟很簡單，不是筆者懶了不寫文章。

**2\. SSH 設定檔**
---------------

接著我們要在這個檔案，配置 SSH 用於連接遠端主機的相關設定。

請到 ~/.ssh 目錄建立新檔案，內容如下：

可使用 vi 或者 nano 編輯，

或者用 Finder 打開，直接建立檔案，輸入指令。

    open ~/.ssh

新增 SSH 設定檔案，輸入指令。

    touch config

SSH 設定檔案內容，輸入內容。

    Host github-personal
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_person
    
    Host github-work
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_work

*   Host：可以自己設定方便識別的名稱
*   HostName：根據你的主機配置，由於 Repository 建立在 Github，因此設定 github.com 即可！
*   IdentityFile：設定你的 SSH 來源，請依據你的私人與工作用指定 私鑰

以上流程就完成建置囉！後續不再需要改動。

**3\. 設定 Repository**
---------------------

以下有兩種情境，請根據所需擇一配置。

### **3.1 新專案 Clone 指定 SSH Config Host**

在 Git 的預設設置中，當使用 SSH 協議與遠端版本控制倉庫進行通信時，它會自動讀取 ~/.ssh/config 文件中的主機配置。

這些主機配置包含了與遠端主機的連接參數，例如主機名稱、用戶名和身份證書文件等。

由於我們環境存在多個遠端主機，因此每次 Clone 需要指派對應的 Host。

使用 SSH 協議進行操作時忽略 ~/.ssh/config 文件中的任何主機配置。

設定環境變數，輸入指令。

    export GIT_SSH_COMMAND="ssh -F /dev/null"

接著 Clone 你的新專案。

    git clone ssh://github-personal:<使用者名稱>/<儲存庫名稱>.git

### 3.2 將既有專案添加指定 SSH Config

每次你有新專案，都需要設定所使用的 SSH 帳號。

請先移動到你的專案目錄，輸入指令。

    git remote set-url origin github-personal:<使用者名稱>/<儲存庫名稱>.git

*   github-personal：根據你的專案用途，輸入 SSH Config 配置的 Host 名稱。

檢查專案的 Remote，輸入指令。可以發現 remote-url 增加了 Host 名稱。

    git remote -v

![1688805918.png.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1738226125940/c5bafb6c-c539-4aef-95cf-8f41a2bb3b8a.png)

好耶！恭喜你設置完畢。

只要要記得，這兩種的專案配置就行囉！

###### 或者跟筆者一樣，重新回顧這篇文章！！

有勘誤之處，不吝指教。ob'\_'ov