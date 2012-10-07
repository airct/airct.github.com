---
layout: post
title: "解決 Octopress 文章內出現中文的時 Rake Generate 的錯誤"
date: 2012-09-04 12:07
comments: true
categories: [git, octopress]
---

Octopress 剛安裝好，如果使用中文 **rake generate** 會出錯。 google 後的 解決方案

修改檔案 C:\Ruby193\lib\ruby\gems\1.9.1\gems\jekyll-0.11.0\lib\jekyll\convertible.rb 將原本的

	self.content = File.read(File.join(base, name))
	
修改成

	self.content = File.read(File.join(base, name), :encoding => "utf-8")
	
將文章檔案都存成 UTF-8 (檔首無 BOM)