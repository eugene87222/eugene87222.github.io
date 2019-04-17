---
title: 用 Github 建立靜態網頁
date: 2017-10-7 14:00:49
tags: [tutorial,web development]
---

# 靜態網頁跟動態網頁的差別

## 靜態網頁

是指在網頁設計中純粹html的網頁，也是網站建設的基礎，常見的就是搭配 css 或 javascript 製作成適合觀看的網頁，網址形式大多為 .html、 .htm 、.shtml、.xml，網頁沒有後台資料庫、不含程式、不太能夠跟使用者互動。優點是相對穩定且頁面瀏覽速度快；缺點是交互性差，更新維護起來較繁瑣。

## 動態網頁

網頁除了 HTML 外還會包含其他網頁程式(ASP、Perl、PHP、JSP等)以及資料庫(SQL)，動態網頁可以透過程式語言結合資料庫的方式，設計出可互動的網頁。特點是以資料庫技術為基礎，可降低網頁維護的工作量，且因為可交互，得以實現更多功能。

## 小結論

整體看來靜態網頁比較適合內容架構簡單或是更新較不頻繁的網頁；動態網頁適合資料內容較大、更新快速的網頁，讓人可以更方便管理網站，大幅降低維護成本。這邊只是非常簡略的說明一下，如果想要更深入了解兩者的差別可以請讀者自行到網路上查找。

# 用 Gituhb 建立網頁

首先要申請一個 [Github](https://github.com/) 帳號([點我申請](https://github.com/))。

[Github](https://github.com/) 提供兩種 [Github Pages](https://pages.github.com/)，這邊只說明如何建立 "User/Organization site"，首先建立一個 repository 並且將這個 repository 命名為 username.github.io (不要真的寫 username，請改成自己的帳號名稱)，並且將 repository 設成 public，建立好直接把 index.html 等檔案放上去就好了，[Github Pages](https://pages.github.com/) 支援 html、css、javascript 與 markdown。當文件都上傳好之後，在瀏覽器上的網址列輸入 username.github.io 就可以看見剛剛建立的個人網頁了，如果發現 404 Not Found 也不用擔心，代表 Github 還在處理你的檔案，再等待一會就能看到自己獨一無二的網頁了。

當然這只是建立個人網頁的其中一種方法，這邊並沒有對 [Github](https://github.com/) 提供的 "Project site" 多做介紹，有興趣的朋友可以直接到 [Github Pages](https://pages.github.com/) 上面看看。