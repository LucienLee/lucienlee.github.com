---
layout: post
title: "[RD水電工不會修水管] 電子報一次就上手"
date: 2013-04-25 01:39
comments: true
categories: [前端浮華, RD水電工不會修水管]
tags: [電子報,EDM]
---

![e-paper](http://farm9.staticflickr.com/8532/8677674341_d95c6ae4a3_c.jpg)

##前言

_[RD水電工不會修水管](/blog/categories/rd%E6%B0%B4%E9%9B%BB%E5%B7%A5%E4%B8%8D%E6%9C%83%E4%BF%AE%E6%B0%B4%E7%AE%A1/)專欄是我在5945呼叫師傅作為RD實習生的學習分享。_

[5945呼叫師傅][5945]除了過去被動等大家來找我們來解決大眾居家生活的水電問題外，現在也想主動幫助大家擁有美好的生活空間，提出居家加值服務－－牆面彩繪，讓大家可以家裡環境好還要更好。

而隨著新服務的推出，最近發行呼叫師傅也跟著發出第一期電子報，讓用戶們可以看到自己家裡可以怎麼改造。

我在這次機會中第一次體驗到如何製作電子報，雖然他本質上就是一個 html 網頁，但是還是有些不同，以下將為各位娓娓道來電子報的小心得。

<!--more-->

##電子報與一般網頁的不同

電子報背後事實上就是 html 網頁，那究竟電子報有什麼特別的呢？
理由是[ HTML格式的email ](http://en.wikipedia.org/wiki/HTML_email)的樣式與一般網頁樣式解讀會有所落差，正確地來說 HTML email 只有 HTML 一部分的能力，而且各家電子郵件解讀 HTML email 的時候，有些地方不符合 W3C 的規範，造成電子報顯示的問題。

比如說 `<head>` 標籤是在一般 HTML 時可以放 CSS 樣式規則，但在 HTML email 裡使用這樣的方法來定義樣式卻會發生問題，有些電子郵件並不支持這樣的用法，比如說Gmail。

另外使用者用來收信的工具十分多元：桌面收信軟體、網頁介面的 Gmail、Hotmail、Yahoo……。每一家對 HTML email 的顯示能力都有些許差異，導致電子報的版型非常難以設計。  


##電子報排版設計小技巧

由於電子報有許多限制，所以也跟著產生一些原則，讓大家比較不容易製作出破版的電子報。

1. 盡量用table來編排。
	現在網頁排版主流使用div，配合浮動（float）來排版，或是利用 position 來定位。但由於 table tag 歷史悠久，它是最能被大多數 email client 辨識的 tag ，而且表格定位單純，設計幾欄他就會保留幾欄給你，比較不會出錯。不過簡單的排版還是可以使用 div ，比如說這次呼叫師傅的電子報的版型比較單純，我就使用 div 標籤。
2. 不要使用 CSS seletor，請使用inline-CSS。
	理由我在之前的例子有說過，由於各家對在 `<head>` 定義樣式支援不同，為了確保你的樣式可以被正常顯示，只好很暴力地慢慢在標籤內下樣式。
3. 圖片來源使用**絕對路徑**來設置`<img src="絕對路徑">`。
	很基本的概念，因為你的圖片不會放在各家 email client 裡。
4. 圖片要設定正確的寬高還有註解，也就是 `width` 、 `height` 和 `alt`。
	設置alt可以讓你在圖片無法顯示的時候，讓使用者還可以知道這張圖片的意思。在 email 裡許多電子郵件服務不會自動顯示圖片，而是詢問使用者是否要顯示圖片，設置 alt 可以在還沒出現圖片前，就由圖片敘述去引起使用者的興趣，讓他選擇顯示圖片。
5. 盡量不要在重要連結上使用圖片。
6. 不要使用 javascript 或 flash 。
7. 不要用 IFRAME 嵌入其他網頁。
8. 確認 HTML 的完整正確，未完成的標籤語法可能會被誤判為 SPAM 郵件。
9. [For Designer]電子報版面盡量以簡單、大方、易讀性佳為設計原則。
	設計複雜的版面不僅會造成工程師排版的困難，也可能會增加在不同 email client 上顯示畫面不一的情況。

最後，在排版時可以去確認目前各家電子郵件服務對 CSS 各種樣式的支援程度，盡量使用各家都支援的屬性。

* [CSS Support in Email Client](http://www.campaignmonitor.com/css/)

![CSS Support](https://lh4.googleusercontent.com/-YBFKvUpAWEo/UXzulQh22SI/AAAAAAAAAWQ/k-jQlkr-LHo/w898-h350/%25E8%259E%25A2%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-04-28+%25E4%25B8%258B%25E5%258D%25885.21.22.jpg)

##製作流程心得

我自己實際製作電子報大致流程如下：

- 設計稿切版
- 由外而內佈局撰寫 HTML
- 設置定位 CSS 樣式
- 設置裝飾 CSS 樣式

首先從設計師手上拿到 PSD 設計檔，利用切片工具進行切版。一邊切一邊把版面區塊分出來，並把所需圖片切出來待會使用。

![](http://farm9.staticflickr.com/8540/8678782452_dd526c3f11_c.jpg)  
（如果不會使用切版工具可以參考[這裡](http://lincyi.pixnet.net/blog/post/26530621-psd%E7%89%88%E5%9E%8B%E5%88%87%E7%89%87%E7%B6%B2%E9%A0%81%E6%95%99%E5%AD%B8~~%E4%BB%A5photoshop%E7%82%BA%E4%BE%8B)。）

根據切版時的想法，建立HTML標籤語法，把版面架構建立起來。然後從最外層開始撰寫定位樣式，盡量使用浮動或是 Normal flow 來排版。

![切割版面區塊](https://lh6.googleusercontent.com/-VgrcsFvL__s/UXz3cNAIv6I/AAAAAAAAAWg/1t2fkm2S_E0/w657-h798/%25E9%259B%25BB%25E5%25AD%2590%25E5%25A0%25B1clear2.jpg)

等到排版完成，開始補上裝飾樣式，如 `font-family` 、 `font-size` 、 `color` 、 `background` 、 `border` ……等等。

切記寫樣式時，一定要使用 inline CSS，例如：

	<p style="color:#ff0; font-size:20px; font-family:arial black;">我是電子報。</p>


##後記

等我完成電子報以後，才發現有一個非常棒的工具[CSS Inliner Tool](http://beaker.mailchimp.com/inline-css)，可以幫我們把 Embed CSS 轉成 Inline CSS ，也就是我之前花許多無謂時間精力去改寫的Inline CSS，現在只要直接用現成的CSS頁面去轉換，不到幾秒鐘，電子報或EDM就自動完成了。


###參考資料

[Yijen's blog－html電子報設計原則整理](http://blog.yam.com/hanasan/article/56605300)  
[Will 保哥－電子報網頁版型設計建議](http://blog.miniasp.com/post/2007/11/Recommandation-on-e-Newsletter-Template-design.aspx)  
[How To Code HTML Email Newsletters](http://www.reachcustomersonline.com/how-to-code-html-email-newsletters-all-new-version/?doing_wp_cron=1349149818.9325120449066162109375#step5)  

_(本篇同步刊載於[5945呼叫師傅-部落格](5945.tw/blog))_
[5945]:http://5945.tw