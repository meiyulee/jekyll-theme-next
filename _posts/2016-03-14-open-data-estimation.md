---
layout: post
tags: [大數據, 巨量資料, 統計]
date: 2016-03-14 19:18
thumbnail: http://govtwit.wpengine.netdna-cdn.com/wp-content/uploads/2012/05/data_img.jpg
title: 開放性資料的估計
published: true
categories:
 - 大數據分析
---

過去傳統的計量經濟學、迴歸分析或甚至博士班之相關課程都是建構在抽樣分配、假設檢定與配適出適切的模型，因此，延伸出因分析所需的Tobit、Probit模型，而在時間序列上則由AR模型延伸出VAR等系列模型。

觀察這些模型特徵，不外乎都是建構在線性概念上，換句話說，無論有無前後期關係，模型首先就是展現分類法(可以二分、三分....)以及資料區分出線性可解釋與不可解釋部分。

<!--more-->

在「為何使用曲線化線性迴規模型」已經提到了重要的兩個觀念後，曲線化線性迴歸模型的特色上，確實與眾不同，同時也難以用紙筆來運算。即使如此，我們不得不說微積分當中的一個觀念是非常有用的，那就是

無論哪種數學模式都可以用泰勒展開式去逼近，其後再加上一個誤差即可代表那個數學模式。

通常經濟學家喜歡用兩階展開來代表，例如，名目與實質利率之間的關係。

問題是真實的資料是否用兩階展開就可以了呢？最後的那個誤差項，又被控制多少呢？

如果遇到的是研究者最常使用的開放性資料，每天(或每分鐘)都在更新的資料來說，愈細微的資料就可以用線性來衡量產生趨勢，預測下一期就會更為精準。所以，若使用的是每分鐘的資料，等於是將一天的資料切割成1440筆資料，然後由1440筆資料估計出線性規則，再由此規則，估計出明天的平均數字。

如此做，好嗎？

這問題就出在於既然是每分鐘更新的開放性資料，那麼研究者想要預測明天第一筆資料就必須將分分鐘鐘的新資料再次的放入，重跑估計與預測。好玩的是，有哪種軟體可以在一分鐘內跑完所有開放性資料，估計出來，並讓其他人使用，或者去買賣股票、網路上進行交易？

所以，當我們遇到開放性資料時，每次新的資料生成後就需要放入資料集內，重跑估計，再比對過去的實際值與估計值，每次都再調整。

而曲線化線性迴歸模型其實很像再使用細微的資料產生線性，再由線性產生曲線。

例如：某股票股價可以反映基本面，所以，先用基本面的財務比率估計股價，再由此股價以曲線方式估計真實股價。

對於開放性資料的估計不一定只能用時間變數(趨勢變數)來估計，當然也可以如上面所言的曲線化線性方式來估計。

而指數的數字則可以呈現出股價的轉折現象，這也是其他模型無法做到的部分，更是捕捉出規律性的方法之一。
