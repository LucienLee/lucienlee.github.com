---
layout: post
title: "AWS EC2 快速連線方法"
date: 2013-07-10 15:57
comments: true
categories: [開發最惱人就是這個設定]
---
##前言

最近跟著 [Coursera](https://www.coursera.org/) 的 [Startup Engineering](https://class.coursera.org/startup-001) 開始學習我較不熟悉的 Linus 環境底下開發與 Deployment ，順手把註冊半年以久的 AWS 帳號進行信用卡認證，正式開通使用。

不清楚 Coursera 的朋友們可以上 [Wikipedia](http://zh.wikipedia.org/wiki/Coursera)了解詳情。簡單的說，他是由 Stanford 大學教授 Andrew Ng 和 Daphne Koller 發起的大學線上課程，上面有許多一流大學所開設的**免費**課程，可以讓大眾自由學習。

這篇文章的重點是如何快速連線 AWS EC2，雖然在 Startup Engineering 課程中有介紹如何達成，但[dm4][dm4]大大分享給我更多一點的技巧，在此分享給大家。
<!-- more -->

##原本的情況

遠端連線 EC2 的方法是藉由 `ssh` 指令進行加密連線，在 AWS 建立新的 instance 的時候，我們會得到一個 `.pem` 檔案作為連線認證使用。這時候 AWS 給我們的連線範例是：

	# @local machine

	$ cd downloads	#移動到你的 .pem 檔所在地方
	$ ssh -i yourkey.pem ubuntu@ec2-54-218-73-84.us-west-2.compute.amazonaws.com 
	
這串指令實在很麻煩，身為一個記憶力正常的凡人，看到這段指令絕對是掩面而泣。

<img src="https://lh3.googleusercontent.com/-tNSs9v6H-60/Ud0wLtSi-TI/AAAAAAAAAY0/6kEC7ufAQFs/w800-h549-no-Ut/www.hdwaller.com+Grumpy-Cat-Full-HD-Wallpaper.jpg" width="50%">   


所幸課程馬上就傳授如何縮短指令的方法。

##課程的版本

簡單來說，我們可以藉由 `.ssh/config` 檔案預先存好登入所要的資訊並給予別名，之後就可以直接打別名進行連線，系統會直接抓取 config 的資料，就不需要一再輸入。那 `.ssh/config` 要怎麼寫呢？其實他的基本格式很簡單，就像下面這般：
	
	Host 名稱(就是用來好記的別名)
		HostName 主機名字
		User 登入用戶名
		IdentityFile 驗證文件的路徑
		
實際上操作的話，以下提供課程所使用的例子：

	# @local machine
	# 首先先複製 key.pem 到 ~/.ssh 底下，並改好檔案權限
	$ mkdir -p ~/.ssh
	$ cp ~/downloads/skey.pem ~/.ssh/
	$ chmod 400 ~/.ssh/skey.pem
	$ chmod 700 ~/.ssh
	$ vim ~/.ssh/config
	# 在 config 編輯內容如下
	Host awshost1
		HostName ec2-54-218-35-71.us-west-2.compute.amazonaws.com #@後面那段
		User ubuntu #@前面那段
		IdentityFile "~/.ssh/skey.pem"
設置好之後就可以以`ssh 別名`來連線了，比如說以上的例子就是輸入`ssh awshost1`來連線。

##再也不用 .pem 了
雖然上面已經可以十分方便了，但是我們還可以再做更多一點。
上面的方法我們還是需要保留 `.pem` 檔案，事實上我們可以連本地端的 `.pem` 檔都不用就可以連線，以下就是要介紹如何跟你的 `.pem` 說拜拜。

	# @local machine 
	# 首先移動到你的 .pem 所在的地方，印出 .pem 檔的內容。記得要用你自己的檔名換掉yourkeyname
	$ cat yourkeyname.pem  
	# 印出來的內容複製起來，他會長的像是：
	$ ssh-rsa AAAAB3NzaC1yc2EAA……
		
再來連線到你 EC2 的遠端機器，把複製到的東西寫到 `~/.ssh/authorized_keys` 裡面。
	
	# @remote machine
	$ vim .ssh/authorized_keys
	# 貼上你剛剛從自己電腦複製出來的那段東西，存檔。
	
之後你就可以把你的 `.pem` 檔給刪掉啦！然後記得把你 `.ssh/config` 底下的 `IdentityFile "~/.ssh/skey.pem"` 這一行刪掉。
你最後的 `config` 應該是長這樣子的：

	Host awshost1
		HostName ec2-54-218-35-71.us-west-2.compute.amazonaws.com
		User ubuntu

很簡單吧！五分鐘不到的設定可以節省我們以後更多開發時間呢！


##參考資料

[Startup Engineering: Lecture 3: Linux and Server-Side Javascript](https://d396qusza40orc.cloudfront.net/startup/lecture_slides%2Flecture3-linux-ssjs-v2.pdf)  

感謝[dm4][dm4]大大的教學。

貓咪圖片 from [HDWaller](http://www.hdwaller.com/new-grumpy-cat-full-hd-wallpaper-4376-just-another-high-quality-hq.html)

###附註
`.pem` 全名為 Privacy Enhanced Mail，想了解更多的話可以讀 [X.509](http://en.wikipedia.org/wiki/X.509) 在 Wiki 的資料或是 [server fault 上面的討論](http://serverfault.com/questions/9708/what-is-a-pem-file-and-how-does-it-differ-from-other-openssl-generated-key-file) 。

[dm4]:http://blog.dm4.tw/