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

解决冲突：
	当Git无法自动合并分支时，就必须首先手动解决冲突。解决冲突后，再提交，合并完成。
	发生冲突后，Git在冲突的文件中，用<<<<<<<，=======，>>>>>>>标记出不同分支的内容
	
分支管理策略：
	master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
	那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
	你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
	语法：git merge --no-ff -m "merge with no-ff" dev ：
		--表示合并dev分支，请注意--no-ff参数，表示禁用Fast forward（这种模式下，删除分支后，会丢掉分支信息。），因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。


bug分支管理：
	每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。
	但如果你在当前分支的工作还没有完成，必须先处理这个bug的时候，就需要用到：保存当前工作，先去处理bug，然后再恢复当前工作的功能。这个步骤为：
		1）git stash：把当前工作现场“储藏”起来，等以后恢复现场后继续工作。
		2）切换到bug分支，处理bug。
		3）恢复之前的工作区，
			git stash list : 查看之前保存的工作区列表。
			stash@{0}: WIP on dev: 6224937 add merge
			git stash apply : 恢复工作区，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
			git stash pop ： 恢复的同时把stash内容也删了：

Feature分支：
	开发一个新功能时候，为了不影响主分支，最好新建一个feature分支，开发完成之后，在合并到主分支。
	git branch -D <分支name> ：强行删除一个未被合并的分支。
	
多人协作：
	master分支是主分支，因此要时刻与远程同步；
	dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
	bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
	feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
	总之，按照实际情况处理即可。

标签管理：
	发布一个版本时，我们通常先在版本库中打一个标签（tag）。就类似于给版本加ID的功能，标签也是版本库的一个快照。标签就是跟某个commit关联起来，便于发布和查找。
	1）创建标签
		切换到需要打标签的分支上，
		1>.git tag <tagName> : 给最近一个commit打标签， git tag v1.0
					git tag : 查看所有标签。
					----也可以使用commit id打标签：-----
						$ git log --pretty=oneline --abbrev-commit  //先找到要打标签的commitID
						c5e00ba update README.md
						19c258a 完善README.md
						ad64802 Create README.MD
						107e5b8 rm test.txt
						c7150a2 add test.txt
						2c71d04 I update this file
						480274e I add a txt file!
						 
						$ git tag v0.8 19c258a    //给对应的commitid打标签
						
						$ git tag   //添加标签成功
						v0.8
						v1.0
		
		2>.git show <tagname> ：查看标签信息。会显示修改的详细信息包括你修改的内容。
				$ git show v1.0
				commit c5e00ba2d020159af4f5a6681467982dc4805317
				Author: wangdy <wdy2099@126.com>
				Date:   Tue Mar 21 14:51:45 2017 +0800
				
				    update README.md
				
				diff --git a/README.md b/README.md
				index 6749104..f020569 100644
				--- a/README.md
				+++ b/README.md
				@@ -154,6 +154,30 @@ git从远程库克隆版本库：git clone git@github.com:wangdy0909/repoName.gi
				                        $ git branch  #查看分支，只剩下master
				                        * master
				
				+解决冲突：
				+       当Git无法自动合并分支时，就必须首先手动解决冲突。解决冲突后，再提交，合并完成。
				+       发生冲突后，Git在冲突的文件中，用<<<<<<<，=======，>>>>>>>标记出不同分支的内
				…………… ……………… ………
		3>.git tag -a v0.1 -m "version 0.1 released" ： 给标签添加说明信息，-a指定版本名，-m添加说明信息。

	2）操作标签：
		1>.删除标签：
			git tag -d <tagname> ：删除本地标签
			git push origin :refs/tags/<tagname> ：删除远程库中的标签。
		2>.推送同步标签：
			git push origin <tagname> ：推送指定标签
			git push origin --tags ：推送全部标签
		
GitHub使用：
	1）在GitHub上，可以任意Fork开源仓库到你的远程仓库；
	2）这样就获取了Fork后的仓库的读写权限；
	3）然后你克隆到本地，修改bug或新增功能后，即可以推送pull request给官方仓库来贡献代码。

配置git：//配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。//
	配置颜色设置：git config --global color.ui true
	配置命令别名：git config --global alias.st status
	-----> git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
	-----> git last ：显示最近一次提交的信息。配置成：git config --global alias.last 'log -l'
	-----> 这个配置就根据自己的使用习惯来说了。

搭建Git服务器：
详见：
http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000

参考源：http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000 <廖大神>


	

