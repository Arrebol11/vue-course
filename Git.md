1.安装GIT后
	配置命令行:
	name ：
		git config --global user.name  "wangyi"
	email:
		git config --global email "wy15140900034@163.com"

2.使用Git:
	git status		查看当前仓库状态
	git init		初始化仓库	(看一个项目是不是被git管理就看有没有.git文件)
	
3.文件状态:	顺序(暂存->未修改->已修改->暂存...)
	未跟踪(未被git管理)和跟踪状态
		跟踪状态:
			暂存:	文件已保存,尚未提交到git仓库
			未修改: 文件和git仓库中文件相同,没有修改
			已修改: 文件已经被修改,和git仓库中文件不同
			
		未跟踪 --> 暂存(跟踪状态)
				gia add <filename>	将文件切换到暂存状态
				git add * 			将所有已修改(为跟踪)的文件暂存
		暂存 -->  未修改			
				git commit -m "xx" 将暂存的文件存储到仓库中
				git commit -a -m   提交所有已修改的文件(为跟踪的文件不会提交)
		未修改 --> 已修改 
				修改代码后,会将其未修改状态更变为修改状态
				
4.常用的命令:
			git restore <filename>				重置(恢复)文件
			git restore --staged <filename> 	取消暂存状态
			
			git rm 		<filename>				删除文件
			git rm      <filename> -f  			强制删除
			
			git mv from to 						移动文件/重命名文件
			eg:	git mv .\1.txt .\2.txt			之后再提交就生效了
			
5.分支
	git在存储文件时,每一次代码的提交都会创建一个与之对应的节点,git就是通过一个一个的节点来
		记录代码的状态的。节点会构成一个树状结构.树状结构就意味着这个树会存在分支
		
		默认情况下仓库只有一个分支，命名为 master
		
		使用git时,可以创建多个分支,分支与分支之间相互独立,在一个分支上修改代码不会影响其他分支
		
		所以在开发中,都是在自己的分支上编写代码,编写完成后,再将自己的分支合并到主分支中
		
		操作:
			1.查看当前分支
				git branch
			2.创建新的分支
				git branch <branch name>
			3.删除分支
				git branch -d <branch name>
			4.切换分支
				git switch <branch name>
			5.创建并切换分支
				git switch -c <branch name>
			6.合并分支(快速合并)
				1.跳转到master
				2.git merge <要合并的分支名>
		变基(rebase):	
			开发中除了通过merge来合并分支外,还可以通过变基来完成分支的合并.
			我们通过merge合并分支时,在提交记录中会将所有的 分支创建 和 分支合并 的过程全部显示出来,这样当项目比较复杂,开发过程比较波折时,我们必须要反复的创建、合并、删除分支。这样就会是我们代码的提交记录非常混乱.
			
			原理:
				变基时发生了什么？
					1.当我们发起变基时，git会首先找到两条分支 最近的共同祖先
					2.对比当前分支 相对于祖先的 历史提交 的区别,并将它们的不同 提取出来存储到一个临时文件中
					3.将当前部分指针 指向 目标的基底
					4.以当前基底开始,重新执行历史操作
					
					变基前 		←c5←c6(指向c4的) (update)
							c4←c7←c8(master)
					变基后	c4←c7←c8←c5←c6
				
				变基和merge对于合并分支来说 最终结果是一样的！  但变基会使代码的提交记录更加清晰简洁
				
				注意:大部分情况下 合并和变基是可以互换的,但如果分支已经提交给远程仓库,那么此时就不要使用变基了
				
6.远程仓库(remote)
			目前我们对于git的所有操作都是在本地进行的。在开发中显然不是这样的,这是我们就需要一个远程的git仓库。远程的git仓库和本地的本质没什么区别,不同点在于远程仓库可以被多人同时访问使用，方便我们协同开发。在实际工作中，git的服务器通常由公司搭建内部使用或是购买一些公共的私有git服务器。学习阶段,直接使用开放的公共git仓库
			常用库:
					1.GitHub
					2.Gitee(码云)
					
			将本地库上传GitHub
			
				git remote add origin https://github.com/Arrebol11/git-demo.git
				# git remove add <remove name> <url>
				
				git branch -M main
				# git branch -M main	修改分支名字为main			
				
				git push -u origin main
				# git push 将代码上传服务器上
				
				
			将本地库上传到Gitee	//让一个文件同时绑定两个仓库,把origin名字改了,
			
			git remote add gitee https://gitee.com/wy1214451852/git-demo.git
			git push -u gitee "main"
			
			在gitee中下载别人的代码
					选择HTTP的 -> 在命令行上输入 git clone 在把gitee的链接粘上去即可
					
			
				