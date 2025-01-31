---
title: 大數據分析下的一個母體平均數/一個母體變異數區間估計
description: 
author: 李玫郁
date: 2022-04-14
categories:
 - 大數據分析
tags: [統計]
image: 
layout: post
---

# 1. 統計學VS大數據分析的區間估計

當樣本服從特定母體分配，從中獨立抽取$n$個隨機樣本，這些樣本滿足

- 母體為常態分配
- 樣本間彼此獨立
- 樣本數不大時，根據統計學的區間估計和假設檢定對母體平均數和母體變異數進行分析

不過大數據分析的區間估計則是在取得數據後須先確定數據或經變數轉換後新隨機變數的機率分配，再使用母體平均數/母體變異數和已確定之母體分配，模擬得到臨界值。最後才照著一個母體平均數或一個母體變異數的區間估計公式計算得到區間。



# 2. 大數據分析下使用一個母體平均數區間估計的要求

對於我們取得的大數據想執行一個母體平均數的區間估計，需要先為數據計算出母體平均數的機率分配後，執行區間估計。那麼我們就得先完成數據分析流程的第一和第二步驟。

## 2.1. 數據分析流程第一步驟

在數據分析的第一步驟中，我們優先計算敘述統計的係數，以及確認是否滿足隨機性和無自我相關。自我相關的檢定是使用Durbin-Watson檢定判斷數據輸入次序是否存在自我相關。若P值 < 0.01，代表我們拒絕虛無假設，即數據之間不具獨立性，已違反區間估計假設，不須做一個母體平均數或一個母體變異數的區間估計。特別是母體變異數的信賴區間已不具有代表性。

## 2.2. 數據分析流程第二步驟

在第二步驟地尋找數據機率模型時，使用適合度檢定判斷數據的母體分配，若發生P值 < 0.0001，代表拒絕虛無假設，就得改用曲線配適(Curve fitting)裡頭的估計隨機變數方程式來代替適合度檢定結果。

為什麼我們得進行數據分析的第二步驟呢？對數據的統計量進行區間估計或假設檢定都須要先確定抽樣分配。而我們可以將統計量視為數據的變數轉換，成為新的隨機變數，為此隨機變數找到對應之母體機率分配。此母體機率分配的重要性在於可以計算臨界值，代入區間估計或檢定。

這點與傳統的統計分析不相同，卻是真實統計分析該做到的。既然統計分析的主體是「統計量」或「估計量」或「檢定量」，那就需要為它找出抽樣分配得到正確的臨界值。

# 3. 數據說明

- 模擬常態分配，平均數=100，標準差=10
- 樣本數 = 100

# 4. 執行後的報表解讀

## 4.1. 敘述統計

| 係數名稱 | 係數值 |
| :----: | :----: |
| 樣本平均數 | 101.82498 |
| 幾何平均數 | 101.27021 |
| 調和平均數 | 100.68671 |
| 樣本變異數 | 109.81160 |
| 樣本標準差 | 10.47910 |
| 偏態 | -0.25138 |
| 峰態 | 3.92542 |
| 平均絕對離差 | 8.01835 |
| 全距 | 60.79455 |
|CV | 0.10291 |

## 4.2. 適合度檢定

- 虛無假設：母體分配服從Hyperbolic secant ($\mu =101.824977, \sigma = 10.479103$)
- 對立假設：反對虛無假設

自由度 = 4，卡方檢定統計量=1.780000 (P值= 0.775787)

根據P值可知無法拒絕虛無假設，因此我們得到母體分配服從Hyperbolic secant ($\mu =101.824977, \sigma = 10.479103$)，期望值 = $E(X)=101.8264010771$；變異數=$Var(X)=109.9249156065$。

## 4.3. 自我相關檢定

- 樣本自我相關係數 = 0.004658
- 虛無假設：自我相關係數=0
- Durbin-Watson檢定統計量=1.843534
- 雙尾P值=42.8574000%

根據P值可知無法拒絕虛無假設，因此我們無法拒絕虛無假設的自我相關係數=0。

## 4.4. 一個母體平均數區間估計

根據區間估計的計算公式可得到

- 99% CI for E(X)  [99.0964941307, 104.5572712423]
- 95% CI for E(X)  [99.7511443368, 103.9026991311]
- 90% CI for E(X)  [100.0853698650, 103.5670933831]

使用的臨界值表為 $Z=\frac{\overline{X}-\theta}{S(\overline{X})}$

| $P(Z \leq$ 臨界值 $)$ | 臨界值對應的機率 |
| :----: | :----: |
| -2.603737 | 0.005 |
| -2.346124 | 0.010 |
| -1.979018 | 0.025 |
| -1.660073 | 0.050 |
| -1.294570 | 0.100 |
| 1.293401 | 0.900 |
| 1.662467 | 0.950 |
| 1.982729 | 0.975 |
| 2.355823 | 0.990 |
| 2.607374 | 0.995 |

## 4.5. 一個母體變異數區間估計

根據區間估計的計算公式可得到

- 99% CI for Var(X)  [67.2494282673, 187.8488286021]
- 95% CI for Var(X)  [75.9854596567, 165.5587599055]
- 90% CI for Var(X)  [80.8622743251, 155.3468379110]

使用的臨界值表為 $Z=\frac{(n-1) \times S_{X}^{2}}{Var(X)}$

| $P(Z \leq$ 臨界值 $)$ | 臨界值對應的機率 |
| :----: | :----: |
| 57.872858 | 0.005 |
| 60.934377 | 0.010 |
| 65.664592 | 0.025 |
| 69.981138 | 0.050 |
| 75.243103 | 0.100 |
| 125.074365 | 0.900 |
| 134.442774 | 0.950 |
| 143.071432 | 0.975 |
| 153.856827 | 0.990 |
| 161.657114 | 0.995 |

# 5. 小結

在《統計學不能做為大數據分析的工具》一書中提供大數據分析的軟體。其第二項功能即可做統計分析。我們仍是根據數據分析流程進行，為數據做統計分析中的區間估計和假設檢定。大數據分析和統計分析的最大差異來自

- 先找數據或數據轉換後新隨機變數的機率分配
- 模擬找出臨界值

因為有屬於數據或數據轉換後新變數的臨界值，再計算一個母體平均數或一個母體變異數的區間估計就容易許多。

不過，我們是否能夠相信這樣的信賴區間取決於數據分析流程第一步驟的隨機性檢定和自我相關檢定，特別是自我相關檢定得到存在自我相關的結果，則一個母體變異數的區間估計無法真正代表母體變異數。

此時，你需要對數據進行去除自我相關，才能讓數據滿足統計分析或大數據分析的區間估計要求，讓信賴區間具有代表性。