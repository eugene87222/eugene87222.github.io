---
title: 電腦動畫與特效期末專題
tags:
  - computer animation
  - NCTU
date: 2019-09-07 11:19:51
# description: ' '
---


我在大三下學期的時候修了一門多媒體所開的「電腦動畫與特效」，並製作了一個小動畫作為這堂課的期末專題，想說在這邊跟大家分享一下製作動畫時的一些心路歷程<!-- more -->。
> P.S. 因為做動畫的當下沒有打算寫這篇，所以也沒有把製作的過程截圖下來，之後有時間再把整個製作流程 run 一遍，並把截圖補上

# 製作動機

源自於 Youtube 上面用子彈射擊各種物體的慢動作影片。  
（影片相關連結：https://www.youtube.com/watch?v=_rFYhLt7Dlo）

# 目標

- 結合剛體碎裂與流體的模擬，嘗試模擬子彈射穿盛裝液體的容器的場景
- 盡可能提高動畫的擬真性
- 學習建模與動畫軟體的基本操作

# 構思

以射擊裝有液體的杯子為例，整個碰撞過程主要包含三個面向
- 子彈射擊杯子時，杯子與子彈之間的碰撞
- 子彈穿過杯中液體時，與液體間的碰撞
- 杯子碎裂後，碎片與液體之間的碰撞

如果將上述三種面向全部模擬出來的話會最接近現實的情況，但是由於硬體設備的不足以及整個模擬的過程過於複雜，後來便決定將碰撞過程拆分成兩個大面向個別處理。

## 剛體層面

先模擬子彈射擊未盛裝液體的杯子，並將模擬結果存起來。

## 流體層面

將先前的動畫模擬結果匯入到專門實作流體的軟體當中，直接將流體加入動畫中。此時因為杯子的破碎方式是固定的（先前的存檔），所以流體並不會對子彈以及杯子碎塊造成力以及位置上的影響，流體只是單純照著杯子的碎裂方式去移動。

# 實作流程

場景：子彈射擊裝有液體的酒杯
用 [Maya](https://www.autodesk.com/products/maya/overview) 作為建模以及模擬剛體碎裂的程式，並使用 [RealFlow](http://www.nextlimit.com/realflow/) 處理流體模擬。

## 在 [Maya](https://www.autodesk.com/products/maya/overview) 中模擬酒杯碎裂

首先在 [Maya](https://www.autodesk.com/products/maya/overview) 裡面建模，包含地板、牆壁、酒杯與子彈。

- 使用 [Maya](https://www.autodesk.com/products/maya/overview) 的 plugin - [Pulldownit](https://www.pulldownit.com/)，來將物體隨機碎裂成多個碎塊，在設定子彈與酒杯的物理屬性（kinematics rigid body 與 passive rigid body）。比較需要注意的是，地板與牆壁等障礙物也要設定屬性，這樣酒杯與子彈才不會穿透進地板或牆壁裡面。
- 設定子彈的 key frame，也就是設定在特定時間下，子彈的位置。設定好之後 Maya 會自行計算物體的移動速度。
- 模擬子彈射擊的過程，並將模擬出來的動畫輸出成 .sd 檔案。

## 在 [RealFlow](http://www.nextlimit.com/realflow/) 中做流體模擬

將先前製作好的動畫匯入進 [RealFlow](http://www.nextlimit.com/realflow/)。

- 使用 [RealFlow](http://www.nextlimit.com/realflow/) 當中的 emitter（有點類似水龍頭的東西，可以在容器中注入液體），並隨著杯子碎裂的方式，來流體模擬的動向。上一個環節已經說明過了，由於剛體的運動軌跡已經決定，流體並不會影響到剛體的移動方向。
- 將模擬出來的流體匯出。

## 回到 [Maya](https://www.autodesk.com/products/maya/overview) 做最後修飾

將 [RealFlow](http://www.nextlimit.com/realflow/) 製作出來的流體以及原先的杯子動畫合併在一起，並給各種物件加上材質，於場景當中加入光源。

# 完成品

影片網址：https://www.youtube.com/watch?v=VnRKnYkhNhU