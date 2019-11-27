### 什么是工作区  (Working Directory) ？

就是电脑本地的文件夹目录，比如之前创建的 FirstGit

### 什么是版本库 (Repository) ？

工作区中的一个隐藏目录 `.git` ，这不是工作区，而是 Git 的版本库

Git 的版本库中有一个非常重要的 `暂存区 (stage or index)` 

![](https://github.com/WaringHu/MyBlog/blob/master/Git%20%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/assets/01.png)

### 向版本库添加文件的过程中发生了什么？

1. `git add`

   将文件传入暂存区

2. `git commit`

   把暂存区的文件提交到分支上

这也就是为什么我们之前讲到 Git 可以多次 `add` 再一次性 `commit`

当我们创建版本库时，Git 就会自动创建唯一的 `master` 分支，我们的项目就是存在该分支上的

### Git 是如何管理修改的？

首先我们要明白的是：**Git 所跟踪管理的其实是我们的修改而非文件**

比如：

1. 修改 `README.md`

   ```
   # Git 真的很棒
   ## 我正在学习使用 Git
   ## Git 跟踪管理的是修改而非文件
   ```

2. `git add`

3. 再次修改 `README.md`

   ```
   # Git 真的很棒
   ## 我正在学习使用 Git
   ## Git 跟踪管理的是修改而非文件
   ## Hello, World! 
   ```

4. `git commit`

这时提交到版本库的 `README.md` 的内容其实是这样的：

```
# Git 真的很棒
## 我正在学习使用 Git
## Git 跟踪管理的是修改而非文件
```

这是因为 `git commit` 只会把暂存区的修改提交至分支，而工作区不会被提交

所以如果我们要提交两次修改就可以这样做：

1. 第 1 次修改
2. `git add`
3. 第 2 次修改
4. `git add`
5. `git commit`

这也就是之前说过的多次 `add` 之后再一次性 `commit`

但你也可以修改一次就 `add` and `commit` 一次

1. 第 1 次修改
2. `git add`
3. `git commit`
4. 第 2 次修改
5. `git add`
6. `git commit`

### 如何撤销修改？

我们还是先小小的改动一下 `README.md`

```
# Git 真的很棒
## 我正在学习使用 Git
## Git 跟踪管理的是修改而非文件
## Hello, World!
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
```

~~第一种方法，直接手动删除，完事！~~

查看一下状态 (实际运用中这步非必须，此处只是为了讲解方便)

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

我们 `Git` 提示我们 `(use "git restore <file>..." to discard changes in working directory)` ，即使用 `git restore <file>` 去撤销工作区里的修改

撤销之前我们先看一下当前工作区里 `README.md` 的内容

```
$ cat README.md
# Git 真的很棒
## 我正在学习使用 Git
## Git 跟踪管理的是修改而非文件
## Hello, World!
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
```

然后使用 `git restore` 撤销修改

```
$ git restore README.md
```

现在再来查看一下工作区里 `README.md` 的内容

```
$ cat README.md
# Git 真的很棒
## 我正在学习使用 Git
## Git 跟踪管理的是修改而非文件
## Hello, World!
```

**注意：** `git restore` 只能修改工作区内未提交至暂存区的修改

另外：`git checkout -- <file>` 与 `git restore` 是一样的作用，它们都是将文件恢复到最近一次 `add` or `commit` 的状态

但是万一你想撤销的修改已经 `add` 到了暂存区怎么办呢？

这是我们修改后的 `README.md` :

```
$ cat README.md
# Git 真的很棒
## 我正在学习使用 Git
## Git 跟踪管理的是修改而非文件
## Hello, World!
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
- 我是多余的
```

现在先将它 `add` ，然后查看状态

```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
```

我们发现 `Git` 提示我们可以用 `git restore --staged <file>` 来撤销 `add` ，将暂存区的修改恢复至工作区，我们执行 `git restore --staged README.md` 语句然后再查看一下状态

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

很明显修改已经回到了工作区，我们可以使用 `git restore` 撤销修改了

**注意：** `git restore --staged` 只能将暂存区的修改恢复至工作区 ，不能直接撤销修改

另外：`git reset HEAD <file>` 也有 `git restore --staged <file>` 的效果

```
$ git reset HEAD README.md
Unstaged changes after reset:
M       README.md
```

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

那么问题又来了，如果你不但将修改 `add` 到了暂存区，还 `commit` 了，那又该怎么办？

请参考之前讲的进行 **版本回退** 

**但是！** 如果你已经将你的修改推送到了远程库，那么祝你好运！
