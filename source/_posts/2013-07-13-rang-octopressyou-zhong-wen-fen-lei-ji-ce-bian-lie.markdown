---
layout: post
title: "讓Octopress有中文分類及側邊列"
date: 2013-07-13 00:18
comments: true
categories: [開發最惱人就是這個設定]
tags: [octopress]
---

##前言
Octopress 雖然號稱他可以讓人[輕鬆部屬、愉悅寫作](http://blog.xdite.net/posts/2011/10/07/what-is-octopress)，但實際上原生 Octopress 2.0 對中文的支持很差，對於與 Ruby 不是好朋友的我，沒有能力自己去改寫，只能去找網路上的 Octopress 前輩們的解法參考，然後 Copy and Paste 試試看究竟可不可以解決問題。

首先我遇到了第一個問題是**『如何使用中文分類，以及將分類顯示在側邊列』**。

很不幸地是，似乎蠻多前輩都是使用英文分類，而其他找到的解法雖然可以使用中文分類，但側編列的問題似乎並不適用於 host 在 **github** 的情況，這真是很奇怪的問題，讓我一度萌生把東西改架在 [Heroku][heroku‎] 上。

最後我參考了 [khaos](http://khaos.github.io/) 如何去讓 Octopreess 支援中文分類的作法，如法炮製地更改側邊列的 `category_sidebar.rb` 讓他成功讓我可以在 github 上的 Octopress 使用中文側邊列，有鑑於我沒有在網路上找到我的情況的解法，在此分享給大家。

<!-- more -->

##解決方法

基本上我是跟隨 [Octopress易筋经，中文分类标签][OC] 的思考方法。既然中文行不通，那就把中文換成英文拼音，以英文來存取中文檔名。實作上是利用 [stringex](https://github.com/rsl/stringex) 的 `to_url` 函式把中文分類標籤的連結位置與相應的 `category_dir` 全部換成相應的拼音。實際上當你使用 `rake new_[post|page]` 指令創建含有中文名的文章時也採用了這樣的技巧，你可以去觀察 Octopress 所建出來的 markdown 檔名，中文標題全部換為拼音顯示。

###實際實現方法

####1. 修改分類的生成方法
首先你得先讓修改分類的生成方法，使之可以使用中文。我採用 khaos 的 [Octopress易筋经，中文分类标签][OC] 這篇文章所提方法，在此轉錄他的作法：

請修改你的 `plugins/category_generator.rb`，首先在文件頭加上一句：

	require "stringex"
	
然後找到其中定義 category 目錄的部分，約在 109 行附近：
 
	self.write_category_index(File.join(dir, category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').downcase), category)
	
將其修改為：

	self.write_category_index(File.join(dir, category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').to_url.downcase), category)

再找到定義中文分類網頁標籤的部分，約是 164 行附近：

	"<a class='category' href='/#{dir}/#{item.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').downcase}/'>#{category}</a>"
	
將其修改為：
	
	"<a class='category' href='/#{dir}/#{category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').to_url.downcase}/'>#{category}</a>"
	
這樣你就完成中文分類的修改了。

####2. 加入分類到側邊欄
在修改側篇欄可以使用中文分類前得先有側邊欄分類，以下參考 [DrayChou的做法](https://github.com/DrayChou/OctopressBlog/blob/master/plugins/category_sidebar.rb) ：

首先把以下內容存到 `plugins/category_sidebar.rb` 。

{% codeblock category_sidebar.rb %}
module Jekyll
  class CategoryListTag < Liquid::Tag
    def render(context)
      html = ""
      categories = context.registers[:site].categories.keys
      categories.sort.each do |category|
        posts_in_category = context.registers[:site].categories[category].size
        html << "<li class='category'><a href='/blog/categories/#{category.downcase}/'>#{category} (#{posts_in_category})</a></li>\n"
      end
      html
    end
  end
end

Liquid::Template.register_tag('category_sidebar', Jekyll::CategoryListTag)
{% endcodeblock %}

接下來把以下內容存到 `source/_includes/asides/category_sidebar.html` 。

{% codeblock category_sidebar.html %}
<section>
  <h1>Categories</h1>
  <ul id="categories">
    {{ "{% category_sidebar " }}%}
  </ul>
</section>
{% endcodeblock %}

最後修改 `_config.yml` ，增加分類內容 `asides/category_sidebar.html` 到 `default_asides`。

{% codeblock _config.yml %}
	default_asides: [asides/category_sidebar.html, asides/recent_posts.html]
{% endcodeblock %}

這樣就完成加入側邊欄的分類列表了。

####3. 修改側邊欄支援中文分類

最後你可以藉由修改 `plugins/category_list_tag.rb` 來讓他支援中文分類。作法如下：
首先在文件頭加入：

	require "stringex"

再來找到 `category_list_tag.rb` 檔案裡的：

	html << "<li class='category'><a href='/blog/categories/#{category.downcase}/'>#{category} (#{posts_in_category})</a></li>\n"

將之換成底下這句：

	html << "<li class='category'><a href='/blog/categories/#{category.to_url.downcase}/'>#{category} (#{posts_in_category})</a></li>\n"

這樣便大功告成，打完收工。


##參考資料

[关于在64位 Windows 7 中部署中文化的Octopress](http://blog.sprabbit.com/blog/2012/03/23/octopress/)   
[Octopress博客分类添加中文支持](http://geron.heroku.com/blog/2012/03/octo-cate-cn-spo/)   
[Octopress易筋经，中文分类标签][OC]  
[DrayChou 的 Octopress 框架](https://github.com/DrayChou/OctopressBlog/)



[OC]:http://khaos.github.io/blog/2012/12/06/using-chinese-category-tags-in-octopress/
[heroku‎]:https://www.heroku.com/‎