> 学习的课程是廖雪峰老师的 [Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)

### Git 是什么？

Git 是目前世界上最先进的分布式版本控制系统

### 版本控制系统是什么？

能记录项目的每次改动（包括时间、改动内容、改动的人），能让多人同时协同完成项目

### Git 是怎么诞生的？

这个不写了，就一个字，佩服！！！

对了，Git 是用 C 开发的

### 集中式版本控制系统  or  分布式版本控制系统

- 集中式版本控制系统

比如：CVS 、SVN 等，版本库集中存放在中央服务器上，进行项目时要先从中央服务其下载最新的版本库，再进行工作，然后推送至中央服务器

**缺点：**

工作时必须联网

不安全，中央服务器损坏整个项目直接完蛋

- 分布式版本控制系统

没有上述的“中央服务器”，每个人的电脑上都有一个完整的版本库，工作时不用联网，对于同一个文件 A ，甲乙都对其进行了改动，合并时甲乙只需要向对方发送自己修改部分的内容，就完成了协同合作

实际使用时会有一个服务器帮助大家实现版本库改动推送

注意：分布式版本控制系统不等于 Git

**优点：**

工作时不用联网

安全，甲电脑坏了再从乙那 Copy 一下版本库就好

还有更多强大的功能

### 安装 Git

[点我跳转]( https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496 )

下载别去官网，=》[国内镜像]( https://github.com/waylau/git-for-win )

### 创建版本库

![](https://github.com/WaringHu/MyBlog/blob/master/Git%20%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/assets/00.png)

打开 `Git Bash` ，创建一个空目录

```
$ mkdir FirstGit
$ cd FirstGit
$ pwd
/f/FirstGit
```

`pwd` 用于显示当前目录

**注意：** Windows系统下，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文 

创建 Git 版本库

```
$ git init
Initialized empty Git repository in F:/FirstGit/.git/
```

`.git` 用于跟踪管理版本库，不得手动修改

`.git` 的默认隐藏，可以使用 `ls -ah` 命令查看

**注意：** Git 版本库不是必须在非空目录下创建

### 将文件添加到版本库

注：版本控制系统能明确的记录版本库的改动，包括哪一行的代码发生了什么变化，但是对于二进制文件除外

1. 创建一个 `README.md` 文件

   ```
   # 我正在学习 Git
   ## 这是我的第一个版本库
   ```

   这个文件要放在之前创建的目录或其子目录下，否则 Git 找不到

2. 添加文件到版本库

   ```
   $ git add README.md
   ```

3. 把文件提交到版本库

   ```
   $ git commit -m "Commit a readme file"
   [master (root-commit) d213b82] Commit a readme file
    1 file changed, 2 insertions(+)
    create mode 100644 README.md
   ```

   `-m` 后的内容是对本次提交的说明

   `1 file changed` 提示有一个文件发生改动

   `2 insertions` 提示插入了两行内容

正因为有 `add` 和 `commit` 命令，所以你可以多次 `add` 一次性 `commit`

```
$ git add file0
$ git add file1 file2
$ git commit -m "Commit 3 files"
```
