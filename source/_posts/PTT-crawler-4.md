---
title: 國網 / 爬蟲 / PTT - 4
tags:
  - python
  - crawler
  - PTT
  - tutorial
date: 2018-02-15 21:14:41
---


上一篇 [國網 / 爬蟲 / PTT - 3](https://eugene87222.github.io/2018/02/14/PTT-crawler-3/) 已經說明如何透過頁數來推導出每個列表頁的網址了，這次要來針對這每個文章列表頁網址去取出每一頁的文章連結。

# 環境

- Windows 10 家用版
- python 3.6.4

先把前幾篇文章的程式碼整理一下 (目前都是以八卦版為例，想爬別的版請自行換網址)
```python
# 取得頁面原始碼
def get_page_content(URL):
    res = requests.get(
    	url=URL,
        cookies={'over18':'1'}
    )
    content = BeautifulSoup(res.text)
    return content

# 取得該版文章總頁數
def get_total_page_num(URL):
    content = get_page_content(URL)
    pagination = content.find('div', {'class':'btn-group-paging').findAll('a', {'class':'btn')
    next_page = pagination[1]['href']
    total_page = next_page.replace('/bbs/Gossiping/index', '')
    total_page = int(total_page[:-5]) + 1
	return total_page

# 取得目前文章列表頁的文章連結
def parse_get_each_row(URL):
    content = get_page_content(URL)
    rows = content.findAll('div',{'class':'r-ent'})
    posts = list()
    for row in rows:
        meta = row.find('div', 'title').find('a')
        if meta :
            posts.append({
                'link': meta['href'],
                'title': meta.text,
                'date': article.find('div', 'date').text,
                'author': article.find('div', 'author').text,
                'push': article.find('div', 'nrec').text
            })
    return posts

# 取得文章內文
def parse_get_article(URL):
    content = get_page_content(URL)
    shift = content.findAll('div',['article-metaline', 'article-metaline-right', 'push'])
    if shift:
        for elem in shift:
            elem = elem.extract()
    main_content = content.find(id='main-content')
    if main_content:
    	content = main_content.text.lstrip().rstrip()
    else:
    	content = 'None'
    return content

# 取得文章列表頁網址
def get_links(total_page, page_want_to_crawl):
    links = list()
    for i in range(total_page, total_page - page_want_to_crawl, -1):
        link = 'https://www.ptt.cc/bbs/Gossiping/index' + str(i) + '.html'
        links.append(link)
    return links
```
以上程式碼都是從前幾篇 [ 爬蟲 PTT ] 整理出來的，忘記的話可以回去看看。
假設現在八卦版總共有 500 頁，要爬 100 頁，可以先利用 get_links 取得這 100 頁文章列表頁的網址
```python
    links = get_links(500, 100)
```
links 裡面就會有 100 個網址，代表著最近 100 頁的文章列表。  
接著要透過 parse_get_each_row 取得每一個列表頁的文章連結，我們可以很直覺地用 for loop 來完成這件事
```python
    post_meta = list()
    for link in links:
        post_meta += parse_get_each_row(link)
```
但是明顯看到執行上面程式碼所需的時間跟要爬的頁數成正比，當頁數很大時候所需的時間也會大幅度增加。  
怎麼辦呢？請先看看下圖
![](/image/illus.jpg)
如果用 for loop 的話就會像右邊那樣，必須等待 A 做完了才能接著做 B 還有其他後面的 task；但是如果能像左邊那樣，把程式平行化同時處理五個 task，豈不是更有效率。
還好 python standrad library 裡面的 multiprocessing 可以做到，multiprocessing 裡面有個叫做 Pool 的東西，能夠實現上圖左邊的流程。程式碼如下
```python
    if __name__ == '__main__':
        with Pool(10) as p:
            post_meta = p.map(parse_get_each_row, links)
        all_post_meta = list()
        for each_page in post_meta:
            for each_post in each_page:
                all_post_meta.append(each_post)
```
※ 注意：如果要用 Pool 的話一定要在 \__name\__ == '\__main\__' 裡面  
可以把 Pool 裡面的數字想像成上圖左邊的分支數量，數字大正常情況下當然比較快，但是還得考慮到網路狀況、硬體限制等。我在學校自己測試的時候 for loop 比 Pool 慢了快要 10 倍，然後 5 ~ 7 行可以請讀者自己研究看看為什麼要這樣寫。

先說到這吧～目前已經可以取得我們要的頁數的所有文章連結了，並透過函數加速讓爬蟲更有效率。下一篇應該是 PTT 爬蟲最後一篇，等 PTT 系列告一段落後就會繼續往 facebook、MOBILE01 爬蟲前進，到時候在談談我做了什麼。