---
layout: post
title: "git-branch"
date: 2012-09-07 22:27
comments: true
categories: [git]
---

# git 的指令範例 #
	
# git clone #

	# git clone git@localhost:/tmp/git/project.git ./project
	Cloning into 'project'...
	root@localhost's password: 
	remote: Counting objects: 6526, done.
	remote: Compressing objects: 100% (4573/4573), done.
	remote: Total 6526 (delta 2437), reused 5182 (delta 1549)
	Receiving objects: 100% (6526/6526), 130.08 MiB | 10.37 MiB/s, done.
	Resolving deltas: 100% (2437/2437), done.

*localhost 是 git server 的 IP 位置*  
*/tmp/git/project.git 是 git repository 的 路徑位置*


# git add #

	# git add -A 		// 將所有檔案都加入追蹤，包含刪除的檔案，新建的 ( untrack files )
	# git add . 		// 將新的和修改的檔案都加入追蹤，但不包含刪除的檔案
	# git add -u 		// 將有 track 的檔案都更新

# git branch #

列出目前有那些 branch 以及目前在那個 branch， 參數 -a 表示同時列出遠端和本地的分支  
*\* 表示目前所在的分支*

	# git branch 	
	* master
	  tmp1

	# git branch -a
	* master
	  tmp1
  	  remotes/origin/HEAD -> origin/master
      remotes/origin/master



	# git branch [new_branch_name]							// 建立本地 local branch
	# git branch -m [old_branch_name] [new_branch_name]		// 改名字 (如果有同名會失敗，改用 -M 可以強制覆蓋)						
    # git branch -D [branch_name] 								// 刪除 local branch


git branch -D -r origin/[branch_name]		// 刪除 remote branch，其中 -r 指遠端 -D 強制執行  
git push origin --delete [remote_branch]		// 比較新版本的 git 才可以使用
	
	[root@localhost repo]# git branch -a
	* master
	  remotes/origin/HEAD -> origin/master
	  remotes/origin/sample
	  remotes/origin/master
	
	[root@localhost repo]# git branch -r -D origin/sample
	Deleted remote branch origin/sample (was c0cbfd0).
	
	[root@localhost repo]# git branch -a
	* master
	  remotes/origin/HEAD -> origin/master
	  remotes/origin/master
