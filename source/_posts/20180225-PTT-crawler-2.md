---
title: '[爬蟲] PTT - 2'
date: 2018-02-13 15:31:08
tags:
  - python
  - crawler
  - PTT
  - tutorial
---

上一篇 [爬蟲 / PTT - 1](https://eugene87222.github.io/2018/02/10/PTT-crawler-1/) 已經講過怎麼取得八卦版首頁的文章列表了，忘記細節的可以回去看看，這次要來講如何取得文章內文。

# 環境

- Windows 10 家用版
- python 3.6.4

# 如何取得內文

## 取得網頁原始碼

我在八卦版上隨便挑了一篇文章，[文章傳送門](https://www.ptt.cc/bbs/Gossiping/M.1518773576.A.14A.html)，一樣使用 requests.get 並用 BeautifulSoup 包起來。
```python
	res = requests.get(
	    url='https://www.ptt.cc/bbs/Gossiping/M.1518773576.A.14A.html',
	    cookies={'over18':'1'}
	)
	html = res.text
	content = BeautifulSoup(html.text)
```

## 分析原始碼

先來看看文章頁面
![](/image/gossiping_screenshot.PNG)
整個黃色框框是 id="main-content"，我們只要裡面的紅色框框部分，也就是文章的內文。

```python
    shift = content.findAll('div',['article-metaline', 'article-metaline-right', 'push'])
    if shift:
        for elem in shift:
            elem = elem.extract()
    main_content = content.find(id='main-content')
    if main_content:
        content = main_content.text.lstrip().rstrip()
    else:
        content = 'None'
```
article-metaline、article-metaline-right 是上面 [ 作者、標題、時間 ] 那個區塊；push 則是推文的部分，這兩個部份都不要，我們可以用 extract() 來移除我們不要的部分，處理好之後 id="main-content" 裡面就只剩下紅色框框的東西了，一樣用 .text 即可取得裡面的文字，另外文章頭尾可能會有多餘的空白，可以利用 lstrip 與 rstrip 來將其移除。  
 
截至目前我們已經可以透過文章列表頁取得每篇文章的資訊 (文章連結、作者、時間等)，並且進一步取得個別的內文，下一次會介紹怎麼抓取更多頁的文章列表，並且用 python 的 standard library 來加速爬蟲。
