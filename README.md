git命令

$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

git init:把这个目录变成Git可以管理的仓库

git add fileName ：将名为

git commit -m "提交说明"

git status ：查看当前版本状态

git diff fileName : 查看修改前后文件的不同

git log ：显示从最近到最远的提交日志,git log --pretty=oneline: 查看简单日志

版本：
在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

版本回退：
git reset --hard 版本标识（HEAD^...）/commit_id（版本提交编号的前几位即可） : 将版本回退到指定版本

git reflog ：查看命令历史，以便确定要回到未来的哪个版本。
$ git reflog
2c71d04 HEAD@{0}: reset: moving to 2c71d040438
480274e HEAD@{1}: reset: moving to HEAD^
2c71d04 HEAD@{2}: commit: I update this file
480274e HEAD@{3}: commit (initial): I add a txt file!


工作区（Working Directory）：就是存放版本库和代码文件的目录。

版本库（Repository）：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

暂存区（stage）：Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
								 需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

Git跟踪并管理的是修改，而非文件。那么，Git是如何跟踪修改的：每次修改，如果不add到暂存区，那就不会加入到commit中。

git checkout -- fileName : 如果修改了一个文件还没有add，那么执行checkout是可以撤销修改的。

	--场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

	--场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
	
	--场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
	
git rm fileName : 用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容.


ssh-keygen -t rsa -b 4096 -C "wdy2099@126.com" : 生成ssh-key 公钥，一路回车即可


git remote add origin https://github.com/wangdy0909/learngit.git ：添加远程库和本地库的关联

git push -u origin master ：将本地库推送到远程库，第一次用-u参数， 以后不用：git push origin master。
			
			wangdy@wangdy MINGW64 /e/learngit (master)
			$ git remote add origin https://github.com/wangdy0909/learngit.git
			
			wangdy@wangdy MINGW64 /e/learngit (master)
			$ git push -u origin master
			Counting objects: 9, done.
			Delta compression using up to 4 threads.
			Compressing objects: 100% (7/7), done.
			Writing objects: 100% (9/9), 858 bytes | 0 bytes/s, done.
			Total 9 (delta 1), reused 0 (delta 0)
			remote: Resolving deltas: 100% (1/1), done.
			To https://github.com/wangdy0909/learngit.git
			 * [new branch]      master -> master
			Branch master set up to track remote branch master from origin.


git remote：显示所有远程库

git remote rm origin ： 删除该origin远程库。

git从远程库克隆版本库：git clone git@github.com:wangdy0909/repoName.git
			
			wangdy@wangdy MINGW64 /e
			$ git clone git@github.com:wangdy0909/hello-world.git
			Cloning into 'hello-world'...
			The authenticity of host 'github.com (192.30.253.112)' can't be established.
			RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
			Are you sure you want to continue connecting (yes/no)? yes
			Warning: Permanently added 'github.com,192.30.253.112' (RSA) to the list of known hosts.
			remote: Counting objects: 7, done.
			remote: Compressing objects: 100% (4/4), done.
			remote: Total 7 (delta 1), reused 0 (delta 0), pack-reused 0
			Receiving objects: 100% (7/7), done.
			Resolving deltas: 100% (1/1), done.
			
			wangdy@wangdy MINGW64 /e
			$ ls
			'$RECYCLE.BIN'/   BaiduNetdiskDownload/   basybirdCar/   hello-world/   jiaque/   KwDownload/   learngit/  'System Volume Information'/   testtxt/   workspace/   workspaceEclipse/   新建文件夹/
			
			wangdy@wangdy MINGW64 /e
			$ cd hello-world/
			
			wangdy@wangdy MINGW64 /e/hello-world (master)
			$ ls
			README.md
			

创建和使用新分支：

	git checkout -b 分支Name : 新建并创建新分支
	
	git branch 分支Name ：新建新分支
	git branch ：查看当前分支
	
	git checkout 分支Name ：选择指定分支，此时HEAD指针指向选择的分支
	
分支开发的全部步骤：

			
			wangdy@wangdy MINGW64 /e/hello-world (master)
			$ git checkout dev  #选择dev分支
			Switched to branch 'dev'
			wangdy@wangdy MINGW64 /e/hello-world (dev)
			$ git branch #查看当前分支
			* dev
			  master
			
			wangdy@wangdy MINGW64 /e/hello-world (dev)
			$ vi README.md  #修改文件
			
			wangdy@wangdy MINGW64 /e/hello-world (dev)
			$ git add README.md #添加到缓存区
			
			wangdy@wangdy MINGW64 /e/hello-world (dev)
			$ git commit -m "use Dev update file"  #提交到版本库
			[dev 1248ce2] use Dev update file
			 1 file changed, 2 insertions(+)
			
			wangdy@wangdy MINGW64 /e/hello-world (dev)
			$ git checkout master  #返回master主分支
			Switched to branch 'master'
			Your branch is up-to-date with 'origin/master'.
			
			wangdy@wangdy MINGW64 /e/hello-world (master)
			$ git merge dev #将dev合并到当前版本库master
			Updating 6785215..1248ce2
			Fast-forward
			 README.md | 2 ++
			 1 file changed, 2 insertions(+)
			
			wangdy@wangdy MINGW64 /e/hello-world (master)
			$ git branch -d dev  #合并完成后，删除dev分支
			Deleted branch dev (was 1248ce2).
			
			wangdy@wangdy MINGW64 /e/hello-world (master)
			$ git branch  #查看分支，只剩下master
			* master




	

