---
title: 用 Hexo + Github 建立靜態網頁
date: 2017-10-14 14:01:18
tags: [ tutorial, web development]
---

之前有概略介紹過靜態網頁跟 [Github Pages](https://pages.github.com/) ([傳送門](https://eugene87222.github.io/2017/10/07/build-own-website/))，這邊就不贅述了。沒有 [Github](https://github.com/join) 帳號的先申請一個([點我申請](https://github.com/))。建立一個 repository，待會會用到，並將這個 repository 命名為 username.github.io (username 請填自己的，不要真的打 username)。

# 安裝前準備

在安裝 [Hexo](https://hexo.io/) 之前得先檢查電腦上是否已經安裝 [Nodejs](https://nodejs.org/en/) 跟 [Git](https://git-scm.com/)

## [下載 Nodejs](https://nodejs.org/en/)

我下載的是 LTS 版本的，想用比較新版本的也可以選右邊的 Current

## [下載 Git](https://git-scm.com/downloads)

直接照著它的預設值去安裝就可以了  
安裝好之後打開 Git bash 設定一下環境

```
	git config --global user.email "you@example.com"
	git config --global user.name "Your Name"
```

# 安裝 [Hexo](https://hexo.io/)

上述程式都安裝好之後就可以透過 [Git](https://git-scm.com/) 來安裝 [Hexo](https://hexo.io/) 了，  
先建立一個資料夾(存放你的網站的所有檔案)，  
打開 Git bash 到剛剛建立的資料夾路徑下執行

```
    npm install -g hexo-cli
```
輸入以下指令查看安裝版本

```
	hexo -v
```
我目前的安裝版本如下：

```
	hexo: 3.3.9
	hexo-cli: 1.0.3
	os: Windows_NT 10.0.15063 win32 x64
	http_parser: 2.7.0
	node: 6.11.3
	v8: 5.1.281.107
	uv: 1.11.0
	zlib: 1.2.11
	ares: 1.10.1-DEV
	icu: 58.2
	modules: 48
	openssl: 1.0.2l
```

接著依序輸入下列指令

```
	hexo init      # 初始化 blog
	npm install    # 安裝相關套件
	hexo g
	hexo s
```

打開瀏覽器在網址列輸入 [http://localhost:4000/](http://localhost:4000/) 就能看到剛建立的網頁了，裡面會有一篇預設的文章。

## [Hexo](https://hexo.io/) 常用指令

```
	hexo g         # hexo generate (產生靜態文件，會在 Hexo 根目錄
				    產生 public 資料夾)
	hexo s         # hexo server   (啟動本地伺服器，用於預覽網頁)
	hexo d         # hexo deploy   (將文件部屬到雲端，例如：Github)
	hexo s -g      # 產生靜態網頁後開啟本地伺服器
	hexo d -g      # 產生靜態網頁後部屬到雲端
```

```
	hexo new <postname>       # 建立新文章
	hexo new page <pagename>  # 建立新頁面
```

## 更換主題

可以從網路上找主題或到 [Hexo Theme](https://hexo.io/themes/) 上面挑選自己喜歡的，然後到那個主題的 Github repository 去把它 clone 下來。指令如下：

```
	hexo clean
	git clone <repository url> themes/<theme name>
```

之後要修改 [Hexo](https://hexo.io/) 目錄下的 \_config.yml 文件，將其中的 theme 屬性改成你剛剛 clone 的主題名稱。

每個主題應該都會有一個 README.md 檔案，會寫如何配置主題，因為每個主題的配置都不盡相同，細節部分就請讀者自行到該主題的 Github repository 上面去看看。

# 配置 [Github Pages](https://pages.github.com/)

> 20190104 更新：前陣子發現說明文件好像有更新，deploy 的步驟變得比較簡單。
> [詳情請點我](https://hexo.io/docs/deployment)

打開 Git bash 輸入

```
	ssh-keygen -t rsa -b 4096 -C "你的 email"
```

Windows 系統預設是在 user/username/.ssh 下會產生兩個檔案，id_rsa 和 id_rsa.pub，然後到 [Github 設定 SSH key 的頁面](https://github.com/settings/keys)新增一個 key，key 的內容就把 id_rsa.pub 裡面的內容複製貼上即可。

## 設定 [Hexo](https://hexo.io/)

用文字編輯器打開 [Hexo](https://hexo.io/) 目錄下的 \_config.yml 文件，找到文件下方的 deploy 並且修改成

```
	deploy:
	  type: git
	  repo: git@github.com:<username>/<username>.github.io.git
	  branch: master
```

打開 Git bash 安裝擴充套件

```
	npm install hexo-deployer-git --save
```

之後到 [Hexo](https://hexo.io/) 目錄下執行

```
	hexo d  # hexo deploy
```

即可部署到 [Github](https://github.com/) 上面。

以上大概就是使用 [Hexo](https://hexo.io/) 跟 [Github Pages](https://pages.github.com/) 建立 fadfas sfasdfasd 靜態網頁的基本流程，因為只是說明如何建立，讀者如果想要有更深入的了解可以到 [Hexo](https://hexo.io/) 官方網頁去自行研究。