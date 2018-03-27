---
title: 國網 / 爬蟲 / PTT - 5
tags:
  - python
  - crawler
  - PTT
  - tutorial
date: 2018-02-16 13:43:25
---


上一篇 [國網 / 爬蟲 / PTT - 4]() 已經說明如何用 Pool 快速取得所有的文章連結了，這次要用這些文章連結去取得每篇文章內文。

# 環境

- Windows 10 家用版
- python 3.6.4

我們一樣可以很直覺地用 for 取得每一篇內文，像下面這樣  
(parse_get_article 是取自上一篇所整理的函數，all_post_meta 則是取自上一篇文末的程式碼)
```python
    contents = list()
    for post_meta in all_post_meta:
        content = parse_get_article(post_meta['link'])
        contents.append(article)
```

但我們在上一篇已經知道如何使用 Pool 了，所以可以改成這樣
```python
    if __name__ == '__main__':
        post_links = [entry['link'] for entry in all_post_meta]
        all_post_content = list()
        with Pool(10) as p:
            contents = p.map(parse_get_article, post_links)
```
執行後得到的 contents 裡面就是每一篇的文章內文，現在把內文跟文章資訊拼在一起
```python
    all_post = list()
    for i in range(len(all_post_meta)):
        all_post.append({
            'title': post_list[i]['title'], 
            'link': post_list[i]['link'], 
            'date': post_list[i]['date'],
            'author': post_list[i]['author'], 
            'push': post_list[i]['push'], 
            'content': contents[i]
        })
```

如此一來 all_post 就包含所有文章的 [ 標題、網址、發布日期、作者、推文數、內文 ] 了。

PTT 爬蟲就到這邊告一段落了，前前後後共寫了五篇，文章中某些程式碼都是跟上篇或上上篇有所關連，從中間看可能會看不懂，如果可以的話還是建議從 [第一篇](https://eugene87222.github.io/2018/02/10/PTT-crawler-1/) 開始看。
