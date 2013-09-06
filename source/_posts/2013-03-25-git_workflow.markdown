---
layout: post
title: "[RD水電工不會修水管] Git 簡單使用情境教學"
date: 2013-03-25 15:57
comments: true
categories: [開發工具]
tags: [git, RD水電工不會修水管]
---
![](http://farm9.staticflickr.com/8524/8673251944_0e3ca1f1f3_z.jpg)

##前言

_[RD水電工不會修水管](  {{ root_url }}/tags/rdshui-dian-gong-bu-hui-xiu-shui-guan/)專欄是我在5945呼叫師傅作為RD實習生的學習分享。_

Git是一種分散式的版本控制系統，版本控制對一個開發團隊來說是不可或缺的工具。他提供了一個乾淨的方法，讓團隊內的開發、除錯、測試實驗性的新功能，不會相互干擾。另外對個人來說，他可以在你程式改爛以後，幫你時光倒流回到之前的樣子。
總結來說Git有以下幾點特色：

*	可以隨時復原到過去的版本
*	多人協作時不會覆蓋到別人的檔案
*	可以保留修改記錄，知道每個人的程式更動
*	軟體發行時，分出開發版與維護版

我認為掌握Git是培養團隊開發技巧的第一步。
Git本身雖然只是個版本控制系統，但他背後暗藏著一個良好的團隊工作流（workflow）概念。所謂__「練武不練功，老來一場空」__，掌握Git指令只是學習的第一步，更重要的是使用Git的開發心法。

對於5945呼叫師傅來說，當然也十分倚賴Git來管理團隊開發。剛加入不久5945，[TonyQ][tonyQ] 大大就分享許多讓我受益良多的經驗，我在這裡分享一點小小心得。

<!--more-->

##安裝Git

請參考 Github 官網

* [Mac setup git]
* [Windows setup git]
* [Linux setup git]


[Mac setup git]: http://help.github.com/mac-set-up-git/
[Windows setup git]: http://help.github.com/win-set-up-git/
[Linux setup git]: http://help.github.com/linux-set-up-git/


##設定
Git commit除了記錄程式的變動外，也會記錄作者的資訊，你可以預先設定你的姓名和Email：

	git config --global user.name "Your Name"
	git config --global user.email "your_email@whatever.com"

我們可以設定 Git讓他在終端機輸出時加上顏色，讓我們更方便閱讀：

	git config --global color.ui true
  
     
##讓我們開始使用Git吧！

首先我們建立一個新的Repository。

	git init

或是 Clone 現有的 Repository ，像是新剛加入別人專案時，要先把目前的程式先複製一份到本機上。你可以在Github或是Bitbucket上看到一個專案位置，把它複製起來後輸入`git clone 複製位置`，此時自己的電腦就會有一份專案檔案了。

![github](http://farm9.staticflickr.com/8522/8671665547_35020ba137_z.jpg)

	git clone git@github.com:LucienLee/5945_RD_training.git


##第一次提交就上手

`git status`可以幫助我們檢查git狀態。
在每次提交之前，很重要地是確認自己git的狀態，了解現在檔案Stage的狀況以及目前的branch，可以幫助自己避免做出意外的操作。

由於`git status`是一個非常常使用的指令，所以我們可以利用以下指令幫他加入別名，讓我們可以用自定的名字來呼叫他：

	git config --global alias.st status

如此一來，就可以用`git st`代替`git status`了。

![git status](http://farm9.staticflickr.com/8531/8671712357_27e67402d1_z.jpg)

上面表示我們正在一個名為master的branch上，然後有一些檔案更動了還沒有加入暫存區（stage）裡。

我們可以利用`git add`把檔案加到暫存區中。

	git add phase1/test/index.php

雖然我們可以直接使用`git add .`一口氣把資料夾底下所有檔案加到暫存區裡頭，但非常不建議不檢視狀態直接加，因為這樣很有可能會加入你不確定或不想追蹤的檔案們，比如說我使用`git add .`會把資料夾的Metadata－－phase1/.DS_Store加入暫存區，然而我們並不需要他。

![git add](http://farm9.staticflickr.com/8384/8671794541_128ba186c7_z.jpg)

`git add`完以後我們可以發現git狀態改變了，我們可以把暫存區的東西__『存檔』__，也就是提交，提交會建立一個節點，讓我們以後可以在需要的時候回到這個節點的狀態。我們可以利用`git commit`來提交檔案。
`git commit`後會要求你寫下commit message，讓你標示這個提交的內容是什麼，幫助你以後要回來過去的記錄點時，可以知道要選擇哪個節點。

那你也可以加上以下參數幫助 commit:

加上`-m`後在加上訊息，可以讓你直接快速提交。

	git commit -m "commite message"

加上`-am`則是可以把所有 tracked 但還未 staged 的檔案直接加入並提交，但是十分不建議使用，我們應該要清楚地知道自己提交了什麼。

	git commit -am "commite message"

加上 `-v` 會列出更動的紀錄，我們可以直接比較檔案的變動。我在5945實習中被要求使用 `-v` 來進行commit，理由是在 commit 之前__『要確認自己究竟寫了什麼東西』__，藉由重新審視來確保自己寫的程式是正確的。

	git commit -v



##在分支上開發

branch 是指分支的意思，我們可以在 git 上開多個 branch 讓不同人同時開發不同部分最後再合併（merge）起來。舉例來說，當我們要開發新功能或是要修正某個 Bug，甚至有時候想要些一些測試的程式來玩玩看，我們可以利用 branch 保持開發環境乾淨。

我可以利用 `git branch` 來開一個新的分支：

	git branch "branch name"

然後利用 `git branch` 來看我們現在有哪些分支：

![git branch](http://farm9.staticflickr.com/8393/8671903821_5e3e453547_z.jpg)

像現在我們有 master 和 x-plan 兩支，而且目前位在master上。
我們可以使用 `git checkout` 來切換所在的branch：

	git checkout "x-plan"

這樣我們就會切到 x-plan 上了。
我們可以在 x-plan 上獨立開發我們想要的東西，然後一樣在這支上面提交以後，最終我們想把 x-plan 的東西跟別人的東西合併，此時我們可以運用 `git merge` 來幫助我們合併兩條分支。
首先先切回 master 上，然後把 x-plan 合併進來：

	git checkout master
	git merge x-plan

這樣就可以在不干擾團隊其他人的情況下開發了。

另外介紹 `git stash` ，他可以把目前工作區的東西丟到暫存區裡，等之後在回來拿他。他有許多適用的時機，比如說你不想提交當前完成了一半的程式，但是卻不得不修改一個緊急 Bug ，你可以先把目前工作狀況丟到 stash ，這時候你的工作區和上次剛提交內容的狀況是一樣，所以你可以放心的修 Bug，等到修完 Bug 把程式 push 到 Server 後再把 stash 中剛剛做到一半的東西叫回來繼續。使用方法如下：

將目前所做的修改都暫存起來：

	git stash

取出最新一次的暫存：

	git stash apply

清除所有暫存：

	git stash clear


##小結

簡易的Git工作流程大概是這樣子的：

1. 有新任務出現！
2. 開新分支。
3. 切到新分支進行開發。
4. 把檔案加入 stage。
5. 提交到版本庫。
6. 合併分支。

![workflow](http://farm9.staticflickr.com/8523/8673174076_b2aa77a843_z.jpg)

至於要做到什麼進度才提交一次呢？通常是完成一個階段性的小工作，便會做一次 commit ，或是開發中間到了有小功能可以正常執行的新進展。
  
   

###參考資料

[GIT IMMERSION](https://gitimmersion-apputu.rhcloud.com/index.html)  
[Git 教育訓練課程投影片 by ihover](http://ihower.tw/blog/archives/6696)  
[Try Git](http://try.github.com/)  
[Git 情境劇](http://blog.gogojimmy.net/2012/02/29/git-scenario/)

  
_(本篇同步刊載於[5945呼叫師傅-部落格](5945.tw/blog))_
[tonyQ]:https://www.facebook.com/tonylovejava