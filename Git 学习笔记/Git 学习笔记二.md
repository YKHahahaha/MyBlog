### 修改文件内容

上回说到，我们已经成功创建并提交了一个 `README.md` 文件到 `FirstGit` 版本库中

1. 修改文件

   现在我们更改 README.md 内容

	```
	# Git 真的很棒
	## 我正在学习使用 Git
	```

2. 查看版本库状态
	
	然后我们打开 `Git Bash` ，注意直接在 `FirstGit` 目录下右键打开更方便

	输入 `git status` 命令
	
	```
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
			modified:   README.md
			
	no changes added to commit (use "git add" and/or "git commit -a")
	```

3. 查看修改

	Git 提示我们 README.md 文件被修改过但是还未提交，如果想查看修改的内容，我们可以使用 ` git diff ` 命令
	
	```
	$ git diff README.md
	diff --git a/README.md b/README.md
	index 72d8b00..elc8964 100644
	--- a/README.md
	+++ b/README.md
	@@ -1,2 +1,2 @@
	-# 我正在学习 Git
	-## 这是我的第一个版本库
	\ No newline at end of file
	+# Git 真的很棒
	+## 我正在学习使用 Git
   \ No newline at end of file
	```

4. 提交修改

	现在我们提交修改，一样的 `add` and `commit` 就好了
	
	```
	$ git add README.md
	```
	
	在这时，我们可以使用 `git status` 再次确认状态
	
	```
	$ git status
	On branch master
	Changes to be commited:
	  (use "git restore --staged <file>..." to unstage)
	        modified:  README.md
	```
	
	提交修改到版本库
	
	```
	$ git commit -m "Modify README.md"
	[master 47c8512] Modify README.md
	 1 file changed, 2 insertions(+), 2 deletions(-)
	```
	
	提交完成后，我们可以再次查看版本库状态
	
	```
	$ git status
	On branch master
	nothing to commit, working tree clean
	```
	
	Git 提示没有文件可以提交，且工作目录干净

### 版本回退

1. 查看历史记录

	Git 最大的作用就是管理我们项目的版本，那么现在我想了解我的项目从建立到现在发生了哪些变化，我们可以使用 `git log` 来查看历史记录

	```
	$ git log
	commit 47c763556bfc836b37c88f52e873467e6b2c73d2 (HEAD -> master)
	Author: WaringHu <waringhu@163.com>
	Date:   Tue Nov 26 10:46:35 2019 +0800
	    Modify README.md
	commit d345b45324c355365fcde03ba3453d5df3767a8c
	Author: WaringHu <waringhu@163.com>
	Date:   Tue Nov 26 01:23:24 2019 +0800
	    Commit a readme file
	```

	我们也可以使用 `git log --pretty=oneline` 查看更简洁的历史记录

	```
	$ git log --pretty=oneline
	47c763556bfc836b37c88f52e873467e6b2c73d2 (HEAD -> master) Modify README.md
	d345b45324c355365fcde03ba3453d5df3767a8c Commit a readme file
	```

	对了，像 `47c763556bfc836b37c88f52e873467e6b2c73d2` 这种是 Git 的版本号 (`commit id`)
	
2. 回退到上一个版本

   通过查看历史记录，我们可以清除的知道当先的上一个版本是 `Commit a readme file` ，我们可以使用 `git reset HEAD^` 

   `HEAD^` 表示上一个版本，`HEAD^^` 表示上两个版本，上上上 x N 个版本就是 `HEAD~N`

   ```
   $ git reset HEAD^
   Unstaged changes after reset:
   M       README.md
   ```

   我们还可以使用 `git reset --hard HEAD^` 以便了解回退到了哪个版本

   ```
   $ git reset --hard HEAD^
   HEAD is now at d345b45324c355365fcde03ba3453d5df3767a8c Commit a readme file
   ```

3. 查看当前版本内容

   使用 `cat` 命令

   ```
   $ cat README.md
   # 我正在学习 Git
   ## 这是我的第一个版本库
   ```

### 前进到未来版本

先查看一下当先版本库历史记录

```
$ git log --pretty=oneline
d345b45324c355365fcde03ba3453d5df3767a8c (HEAD -> master) Commit a readme file
```

此时我们如果向回到 `Modify README.md` 也是可以的，这个时候就需要用到 `commit id` ，上一个版本的 `commit id` 是 `47c763556bfc836b37c88f52e873467e6b2c73d2` ，`commit id` 不用写全，Git 能自动找到

```
$ git reset --hard 47c76355
HEAD is now at 47c76355 Modify README.md
```

使用 `cat` 查看一下

```
$ cat README.md
# Git 真的很棒
## 我正在学习使用 Git
```

Git 真的是很棒呢！如果我们不记得之前的版本号怎么办呢？`git reflog` 可以帮助你查看版本变化的历史命令

```
$ git reflog
47c7635 (HEAD -> master) HEAD@{0}: reset: moving to 47c7635
d345b45 HEAD@{1}: reset: moving to HEAD^
47c7635 (HEAD -> master) HEAD@{2}: commit: Modify README.md
d345b45 HEAD@{3}: commit (initial): Commit a readme file
```
