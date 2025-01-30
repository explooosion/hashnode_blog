---
title: "Nginx - 405 not allowed ft. Cloudflare"
seoTitle: "Nginx - 405 not allowed ft. Cloudflare"
seoDescription: "Nginx 405 not allowed 解決方式"
datePublished: Fri Oct 08 2021 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6ja3wbg000409l80ou3bje9
slug: nginx-405-not-allowed-ft-cloudflare
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2021-10-08_Nginx%20-%20405%20not%20allowed%20ft.%20Cloudflare/banner/1633700292.png
ogImage: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2021-10-08_Nginx%20-%20405%20not%20allowed%20ft.%20Cloudflare/banner/1633700292.png
tags: nginx

---

Nginx 405 not allowed 解決方式

修正 nginx 出現 405 方法拒絕

![1633700292.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2021-10-08_Nginx%20-%20405%20not%20allowed%20ft.%20Cloudflare/1633700292.png)

前言
--

本篇的錯誤發生於 [cloudflare](https://www.cloudflare.com/) 設置 [DDoS Protection](https://www.cloudflare.com/en-au/ddos-de/) 機制後發生

在 cloudflare 經過此機制後會向 server 發送 POST 事件

由於 nginx 預設禁止靜態資源配置 POST 請求

因此發生禁止的 Response

設置
--

將 nginx 設置關於 [error\_page](http://nginx.org/en/docs/beginners_guide.html) 的捕捉

\[ default.conf \]

    server {
    
        listen 80;
        listen [::]:80;
    
        return 301 https://$host$request_uri;
    }
    
    server {
    
        # ...
    
        error_page 405 =200 https://$host$request_uri;
    }

參考
--

*   [https://stackoverflow.com/questions/24415376/post-request-not-allowed-405-not-allowed-nginx-even-with-headers-included](https://stackoverflow.com/questions/24415376/post-request-not-allowed-405-not-allowed-nginx-even-with-headers-included)
*   [https://www.izhangheng.com/nginx-405-not-allowed](https://www.izhangheng.com/nginx-405-not-allowed)
*   [https://cloud.tencent.com/developer/article/1680056](https://cloud.tencent.com/developer/article/1680056)
*   [https://github.com/denysvitali/nginx-error-pages](https://github.com/denysvitali/nginx-error-pages)

有勘誤之處，不吝指教。ob'\_'ov