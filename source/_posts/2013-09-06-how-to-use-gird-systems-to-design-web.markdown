---
layout: post
title: "使用 grid system 來設計你的網頁"
date: 2013-09-06 16:47
comments: true
categories: [前端浮華, 視覺設計]
tags: [illstrator, grid system, wireframe, 網頁設計]
---
![](https://lh4.googleusercontent.com/-prmT68SGo_Y/UinLMxd3JEI/AAAAAAAAAbg/Ch62cIxQy6Q/w663-h464-no/960_grid_12_col.png)

##前言

現今網頁製作上使用 **grid system** （栅格系统）已經十分普遍，即使沒有聽過 grid system ，只要你使用過熱門前端框架－－[twitter Bootstrap](http://getbootstrap.com/) 或是 [Zurb Foundation](http://foundation.zurb.com/)， 其實你背後就已經使用過了 grid system 。  
為什麼 grid system 會這麼普遍的原因是它提供給我們了富有彈性並方便的網頁排版及模組化方法，也提供了網頁設計師與前端工程師共同溝通的語彙。
對我來說，建立網頁設計師與前端工程師共同的溝通模式是很重要的。目前在前端工程已經有相當多 grid system framework ，這個觀念在前端已經是相當普遍。但從平面設計師轉換到網頁設計師的人，一開始必須重新建立網頁排版的概念，不論是學習設計適應各種大小螢幕的設計還是建立網頁資訊流（ Normal flow ）的概念， grid system 可以幫助設計師有所依歸。
這篇文章將會簡介 grid system 以及如何在 illustrator 設計 wireframe 或是視覺稿時運用自己的 grid system 。

<!-- more -->

##什麼是 grid system 柵格系統

grid system 其實是一種平面設計方法與風格，它藉由固定的格子切割版面來設計佈局。就如下圖所示：

<a href="http://www.flickr.com/photos/jasonprini/377655327/" title="Flickr 上 Jason Prini 的 Grid systems in graphic design"><img src="http://farm1.staticflickr.com/164/377655327_e4af2afc60_z.jpg?zz=1" width="640" height="480" alt="Grid systems in graphic design"></a>


grid system 的歷史可以從17世紀說起，根據 Wikipedia [柵格系統](http://zh.wikipedia.org/w/index.php?title=%E6%A0%85%E6%A0%BC%E8%AE%BE%E8%AE%A1&variant=zh-hant) 的介紹，它是一開始字體設計的方法－－
> 1629年，法王路易十四命令成立一個管理印刷的皇家特別委員會，由數學家尼古拉斯·加宗（Nicolas Jaugeon）擔任領導。委員會提出了新字體設計建議：以羅馬體為基礎，採用方格為設計依據，每個字體方格分為64個基本方格單位，每個方格單位再分成36小格，這樣，一個印刷版面就由2304個小格組成。這是世上最早對字體和版面進行科學實驗的活動。也是柵格系統的雛形。

而之後二十世紀初現代主義萌生，此時工業革命成熟人們也進入機械的時代，但科技的進步同時也帶來一次大戰的毀滅，讓許多人生活貧困與物質匱乏。這讓此時的設計師對過去提出批判，並萌生現代主義。
而現代主義中的包浩斯( Bauhaus ) 風格追求規律理性、極簡化、功能主義的設計風格，這樣極簡的形隨機能風格，延續到了 20 世紀中期的瑞士設計風格 （ Swiss Design ）並發揚光大。由於強調極簡不使用裝飾， Swiss Design 十分強調文字編排來表現，此時網格系統在平面設計被大量使用，很快地就被推廣到全世界。

![Swiss Design from www.swissted.com](https://lh6.googleusercontent.com/-TOWlM2-pcvo/Uim8FPwCjRI/AAAAAAAAAaw/BxU08vVRkEY/w581-h454-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%25887.25.38.png)

我們可以從中理解到 grid system 本質上就是追求對齊、理性，這延續到網頁設計中，變成一種*以規律的格線來做網頁佈局*的方法。

##在網頁中的 grid system

運用在網頁的 grid system 是把一定寬度的頁面切割成數欄，並且欄與欄之間留有間隙。我們網頁上每個元素區塊，依著所需的寬度欄數由上而下排版，比如下圖是有名 [960 grid](http://960.gs/)，它把 960px 寬的區塊切成 12 欄，而我們排版時就依所需的大小對齊欄線。

![Example with 960 grid](https://lh4.googleusercontent.com/-prmT68SGo_Y/UinLMxd3JEI/AAAAAAAAAbg/Ch62cIxQy6Q/w663-h464-no/960_grid_12_col.png)

由上面的例子我們可以很清楚 grid system 如何使用，但如果我們需要自己設計 grid system 我們必須了解 grid system 的組成。grid system 主要是由欄（column）與間隙（ gutter ）所組成，另外有的時候我們並不會把元素填滿整個頁面，會在兩旁留白（grid padding），最後所有的欄、間隙與留白的寬度加總起來要等於預計設計頁面的總寬。

![grid system 的組成元素](https://lh5.googleusercontent.com/-PDuCRVnEXn4/UinVvnO77rI/AAAAAAAAAes/gPxb6K32D1E/w663-h435-no/grid.png)

整個 grid system 的計算公式如下：
	Total width = grid padding × 2 + ( column width + gutter width )× number of column - gutter width

公式最後要再減一個間隙的理由是間隙會比欄少一個，就像植樹問題一樣。以 960 grid 舉例來說， 960 grid 的各項數字是：

-	欄寬：60 px
-  間隙：20 px
-  留白：10 px

套用公式的結果：
	960 = 10 × 2 + ( 60 +20 ) × 12 - 20  
  
####為什麼要在網頁設計裡使用 grid system

了解了網頁中的 grid system 是什麼以後，但為什麼要使用 grid 來設計網頁呢？
我認為理由有三點：

1. 增加可讀性  
使用了格線佈局可以建立對齊規律的排版，我們可以把過去運用在平面設計的對齊技巧使用在網頁身上，我們可以藉由分欄拆出不同的區塊來放不同的內容，但同時個區塊間仍然整齊規律。
2. 建立網頁設計師與前端工程師的共通語彙  
當設計師與工程師都共同使用 grid system ，那在產品開發中可以從線框（ wireframe）開始，視覺設計稿到最後前端 CSS 都一脈相承，不需轉換任何比例尺寸，可以加快開發速度以及降低設計與程式的溝通成本。
3. 幫助設計師建立適應不同大小螢幕的佈局  
網頁設計跟平面設計最大的差別之一在於，網頁的**畫布**不是固定大小。平面設計常常是有一個目標大小的版面，比如說印出來的大小。設計師是直接根據最後輸出的大小在畫布上設計；然而網頁會遇到使用者螢幕大小不同，一個網頁必須自己適應在不同的螢幕上，過去固定大小的設計並不適用於流動大小的網頁了！ 設計的單位從 pixel 變成 ％，以相對比例來設計佈局。而 grid system 提供了某種程度的比例概念，可以讓設計師比較可以做到自適應式設計（ Responsive design ）。

## 在 illustrator 中運用 grid system 設計你的網頁

在平面設計的時候我們本來就會使用參考線（ guide ）來幫助我們，而我們在網頁設計中也是利用參考線來幫助我們建立 grid 。這裡我們以 [One% CSS Grid](http://onepcssgrid.mattimling.com/) 為例，我們來建立它的 grid 1200版本。
這個 grid system 是 12 欄佈局，每欄寬度為總寬 5.5%、間隙為總寬 3%。在螢幕 1280 px 的情況，實際像素大小如下：

-	欄寬：66 px
-  間隙：36 px
-  留白：46 px
-  扣掉留白總寬： 1188 px

以下會教大家如何在 illustrator 建立這樣的 grid system 參考線：

（Windows 用戶請把以下指令的 `Cmd` 當成 `Ctrl`）

1. 首先我們先建立一個寬 1280 px 的畫布，高度隨自己喜好。（示範中我使用 1600 px ）。將目前圖層取名為 `Grid`，同時打開尺規（Rule），幫助我們設計時抓大小。打開的方式是 `Cmd + R` 或是找到選單中 `View > Rules > Show Rulers`。  
![](https://lh4.googleusercontent.com/-cGyBxkiy15s/UinpDq6-mGI/AAAAAAAAAfc/aOj5ylVHnrA/w637-h360-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258810.38.09.png)

2. 使用左邊面板的矩形工具，畫出一個與畫布一樣大的矩形蓋在畫布上。  
![](https://lh6.googleusercontent.com/-1yxkdajE1Tc/Uinq7svc9KI/AAAAAAAAAf4/Vxnh-UIrnL0/w646-h201-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258810.46.48.png)

3. 用選取工具選中剛剛的矩形後，在選單列點選 `Object > Path >  Split Into Grid` （`物件 > 路徑 > 列與行`） ，開啟工作對話窗。  
![](https://lh5.googleusercontent.com/-Zs_xJwbf0rk/UinuHAn5-QI/AAAAAAAAAhQ/dpdUdZrNHp8/w436-h255-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258811.00.28.png)

4. 將選單各欄位如圖所示輸入算好的數值。  
![](https://lh4.googleusercontent.com/-ud-oKxqCVQ4/Uint6V5oDAI/AAAAAAAAAg8/cTca9fqrItU/w530-h367-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258810.59.18.png)

5. 在選取所有小矩形的狀態，按下 `Cmd + G` 把所有矩形群組起來，再使用對齊工具將所有東西置中。  
![](https://lh6.googleusercontent.com/-Mi0Bw6nc_oY/Uinvq_JYaKI/AAAAAAAAAh4/zREgOs5_i10/w542-h379-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258811.03.21.png)

6. 一樣在選取矩形的狀態，按下 `Cmd + 5` 或是點選 `View > Guide > Make Guide`，把所有小矩形變成參考線。  
![](https://lh4.googleusercontent.com/-8yLAILePKBg/Uin2Qo4t0RI/AAAAAAAAAj4/8MEhk3zeSTo/w593-h193-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258811.34.32.png)

7. 此時你就會得到 grid system 的參考線了，你可以順便鎖定參考線以防誤刪。鎖定的方法是`Cmd + Alt + ;` 或是點選 `View > Guide > Lock Guide`。  
![](https://lh5.googleusercontent.com/-THCAX56ttKk/Uin28MKqNhI/AAAAAAAAAkI/A-M1TvZFmgM/w709-h222-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258811.37.54.png)

8. 你可以藉由這些格線來設計你要的版面，我先以不同方塊來區分元素版位。  
![](https://lh5.googleusercontent.com/-FTV1YEfdnyc/Uin577Go0oI/AAAAAAAAAkc/5nzv5sexLFQ/w461-h569-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-06+%25E4%25B8%258B%25E5%258D%258811.50.51.png)

9.  最後填上一些細節，就可以完成最基礎的線框稿。  
![](https://lh3.googleusercontent.com/-Z8j_xqLHzao/Uin-Q4Snq_I/AAAAAAAAAkw/7FZ0AoP-ECw/w461-h571-no/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-09-07+%25E4%25B8%258A%25E5%258D%258812.09.13.png)


##動手試試看吧！
事實上在設計階段建立 grid system 並不難，只要算好你想要用的 grid 大小就可以讓軟體幫你生出格線，之後排版對齊就可以很方便。如果不知道要使用什麼樣的 grid 你可以去參考網路上的 grid system framework 像是 [960.gs](http://960.gs/)、 [Blueprint](http://www.blueprintcss.org/) 、[Golden Grid System](http://goldengridsystem.com/)……有非常多的框架可以選擇，趕快找一個 grid system 來實作看看吧！


###參考資料
[How to wireframe two web layouts in Illustrator using 960.gs](http://thenextweb.com/dd/2012/09/29/how-wireframe-two-web-layouts-illustrator-using-960-gs/)  
[justfont 扁平化設計與字型學](http://blog.justfont.com/2013/05/flat-design-and-typography/)  
[One % CSS Grid](http://onepcssgrid.mattimling.com/)  
[swissted](http://www.swissted.com)  