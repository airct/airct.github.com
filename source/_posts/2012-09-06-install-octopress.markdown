---
layout: post
title: "紀錄安裝 octopress 過程"
date: 2012-09-04 12:28
comments: true
categories: [git, octopress]
---

這篇主要紀錄安裝 octopress 過程

- Install [Git](http://git-scm.com/).
- Install rbenv or [RVM](http://rubyinstaller.org/downloads/).
- Install [DevKit](http://rubyinstaller.org/downloads/).

# 安裝 Octopress #

	# git clone git://github.com/imathis/octopress.git octopress
	# cd octopress    # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes).

在 Ootopress 的目錄底下安裝 ， 但是 window 中如果是使用 git bash 有可能會出現 PATH 問題。

	# gem install bundler
	Fetching: bundler-1.2.0.gem (100%)
	Successfully installed bundler-1.2.0
	1 gem installed
	Installing ri documentation for bundler-1.2.0...
	Installing RDoc documentation for bundler-1.2.0...
	
然後 
	
	# bundle install  // 這裡在 windows 環境下出錯 ， google 之後需要安裝 DevKit
	Fetching gem metadata from http://rubygems.org/.......
	Using rake (0.9.2.2)
	Using RedCloth (4.2.9)
	Installing posix-spawn (0.3.6)
	Gem::InstallError: The 'posix-spawn' native gem requires installed build tools.

	Please update your PATH to include build tools or download the DevKit
	from 'http://rubyinstaller.org/downloads' and follow the instructions
	at 'http://github.com/oneclick/rubyinstaller/wiki/Development-Kit'
	An error occurred while installing posix-spawn (0.3.6), and Bundler cannot continue.
	Make sure that `gem install posix-spawn -v '0.3.6'` succeeds before bundling.

發生錯誤訊息，表示需要先把 gem install posix-spawn -v '0.3.6' 安裝成功能才繼續 ， 接著先切換到 DevKit 資料夾下
照著  [參考](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit)  開始安裝 DevKit

	# cd C:\Download\Devkit
	# ruby dk.rb init
	[INFO] found RubyInstaller v1.9.3 at C:/Ruby193

	Initialization complete! Please review and modify the auto-generated
	'config.yml' file to ensure it contains the root directories to all
	of the installed Rubies you want enhanced by the DevKit.


	# ruby dk.rb review
	Based upon the settings in the 'config.yml' file generated
	from running 'ruby dk.rb init' and any of your customizations,
	DevKit functionality will be injected into the following Rubies
	when you run 'ruby dk.rb install'.

	C:/Ruby193


	# ruby dk.rb install
	[INFO] Updating convenience notice gem override for 'C:/Ruby193'
	[INFO] Installing 'C:/Ruby193/lib/ruby/site_ruby/devkit.rb'

最後切回 Octopress 目錄後再執行一次

	# bundle install
	Fetching gem metadata from http://rubygems.org/.......
	Using rake (0.9.2.2)
	Using RedCloth (4.2.9)
	Installing posix-spawn (0.3.6) with native extensions
	Installing albino (1.3.3)
	Installing blankslate (2.1.2.4)
	Installing chunky_png (1.2.5)
	Installing fast-stemmer (1.0.1) with native extensions
	Installing classifier (1.3.3)
	Installing fssm (0.2.9)
	Installing sass (3.1.20)
	Installing compass (0.12.2)
	Installing directory_watcher (1.4.1)
	Installing ffi (1.0.11) with native extensions
	Installing haml (3.1.6)
	Installing kramdown (0.13.7)
	Installing liquid (2.3.0)
	Installing syntax (1.0.0)
	Installing maruku (0.6.0)
	Installing jekyll (0.11.2)
	Installing rubypython (0.5.3)
	Installing pygments.rb (0.2.13)
	Installing rack (1.4.1)
	Installing rack-protection (1.2.0)
	Installing rb-fsevent (0.9.1)
	Installing rdiscount (1.6.8) with native extensions
	Installing rubypants (0.2.0)
	Installing tilt (1.3.3)
	Installing sinatra (1.3.2)
	Installing stringex (1.4.0)
	Using bundler (1.2.0)
	Your bundle is complete! Use `bundle show [gemname]` to see where a bundled gem
	is installed.
	
最後

	# ruby --version  // 應該會是 Ruby 1.9.3 
	ruby 1.9.3p194 (2012-04-20) [i386-mingw32]
	
	
	# rake install
	## Copying classic theme into ./source and ./sass
	mkdir -p source
	cp -r .themes/classic/source/. source
	mkdir -p sass
	cp -r .themes/classic/sass/. sass
	mkdir -p source/_posts
	mkdir -p public
	
	
參考資訊

http://octopress.org/docs/setup/
