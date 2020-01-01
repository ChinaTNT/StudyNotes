# Git

+ 增加用户信息

  ```git
  git config --global user.name "John Doe"
  git config --global user.email johndoe@example.com
  ```

  `--local针对当前某仓库生效，优先级高于--global。就一个代码仓库而言，两个设置的效果一样`

+ 设置文本编辑器（默认使用操作系统默认的文本编辑器）

  例如使用emacs

  ```console
  git config --global core.editor emacs
  ```

+ 检查配置信息

  ```console
  $ git config --list
  user.name=John Doe
  user.email=johndoe@example.com
  color.status=auto
  color.branch=auto
  color.interactive=auto
  color.diff=auto
  ...
  $ git config user.name #查询某一项配置
  John Doe
  ```

+ 获取帮助

  ```console
  $ git help <verb>
  $ git <verb> --help
  $ man git-<verb>
  $ git help config #获得 config 命令的手册
  ```

+ 建立Git仓库

  a. 在现有目录下初始化仓库

  ```console
  $ git init
  # 添加文件并提交
  $ git add *.c #添加*.c文件 后面可以接多个文件或者文件夹
  $ git add LICENSE #添加license
  $ git commit -m 'initial project version' #提交
  ```

  b. 从服务器clone一个现有的仓库

  ```console
  $ git clone https://github.com/libgit2/libgit2 
  $ git clone https://github.com/libgit2/libgit2 mylibgit #与上面一条命令区别的是:本地仓库的名字会变更为mylibgit
  ```

  *Git 支持多种数据传输协议。 上面的例子使用的是 `https://` 协议，不过你也可以使用 `git://` 协议或者使用 SSH 传输协议，比如 `user@server:path/to/repo.git` 。*

+ 记录每次更新到仓库

  你工作目录下的每一个文件都不外乎这两种状态：已跟踪或未跟踪

  + 已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，它们的状态可能处于未修改，已修改或已放入暂存区。（ 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态。）
  + 其他均为未跟踪文件

+ 使用 Git 时文件的生命周期

![使用 Git 时文件的生命周期](lifecycle.png)

+ 检查当前文件状态

  ```console
  $ git status
  On branch master
  nothing to commit, working directory clean 
  #此时表明工作目录已经干净了
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
      new file:   README
   #只要在 Changes to be committed 这行下面的，就说明是已暂存状态。 如果此时提交，那么该文件此时此刻的版本将被留存在历史记录中。
  ```

+ 暂存已修改文件

  ```console
  # 修改了一个已被跟踪（git add过的）的文件
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
      new file:   README
  
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
      modified:   CONTRIBUTING.md
  #文件 CONTRIBUTING.md 出现在 Changes not staged for commit 这行下面，说明已跟踪文件的内容发生了变化，但还没有放到暂存区。 要暂存这次更新，需要运行 git add 命令。 这是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。 将这个命令理解为“添加内容到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。
  ```

   	 现在让我们运行 git add 将"CONTRIBUTING.md"放到暂存区，然后再看看 git status 的输出：

  ```
  $ git add CONTRIBUTING.md
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  new file:   README
  modified:   CONTRIBUTING.md
  ```

  ​	   怎么回事？ 现在 `CONTRIBUTING.md` 文件同时出现在暂存区和非暂存区。 这怎么可能呢？ 好吧，实际上 Git 只不过暂存了你运行 `git add` 命令时的版本， 如果你现在提交，`CONTRIBUTING.md` 的版本是你最后一次运行 `git add` 命令时的那个版本，而不是你运行 `git commit` 时，在工作目录中的当前版本。 所以，运行了 `git add` 之后又作了修订的文件，需要重新运行 `git add` 把最新版本重新暂存起来：  

  ```console
  $ git add CONTRIBUTING.md
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
      new file:   README
      modified:   CONTRIBUTING.md  
  ```

+ 状态简览

  ```console
  $ git status -s #等同于 git status --short
   M README #出现在右边的 M 表示该文件被修改了但是还没放入暂存区
  MM Rakefile #Rakefile 在工作区被修改并提交到暂存区后又在工作区中被修改了 （该文件修改一次后 add了一次 又修改了一次）
  A  lib/git.rb
  M  lib/simplegit.rb #出现在靠左边的 M 表示该文件被修改了并放入了暂存区
  ?? LICENSE.txt #未跟踪文件
  ```

+ 忽略文件

  

  文件 `.gitignore` 的格式规范如下：

  - 所有空行或者以 `＃` 开头的行都会被 Git 忽略。
  - 可以使用标准的 glob 模式匹配。
  - 匹配模式可以以（`/`）开头防止递归。
  - 匹配模式可以以（`/`）结尾指定目录。
  - 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（`!`）取反。

  ```console
  $ cat .gitignore
  *.[oa] #忽略所有以 .o 或 .a 结尾的文件
  *~ #忽略所有以波浪符（~）结尾的文件，许多文本编辑软件（比如 Emacs）都用这样的文件名保存副本。 
  ```

+ 查看已暂存和未暂存的修改

  要查看尚未暂存的文件更新了哪些部分，不加参数直接输入 `git diff`

  ```console
  $ git diff
  diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
  index 8ebb991..643e24f 100644
  --- a/CONTRIBUTING.md
  +++ b/CONTRIBUTING.md
  @@ -65,7 +65,8 @@ branch directly, things can get messy.
   Please include a nice description of your changes when you submit your PR;
   if we have to read the whole diff to figure out why you're contributing
   in the first place, you're less likely to get feedback and have your change
  -merged in.
  +merged in. Also, split your changes into comprehensive chunks if your patch is
  +longer than a dozen lines.
  
   If you are starting to work on a particular area, feel free to submit a PR
   that highlights your work in progress (and note in the PR title that it's
  ```

  ​		此命令比较的是工作目录中当前文件和暂存区域快照之间的差异， 也就是修改之后还没有暂存起来的变化内容。

  ```console
  #查看已暂存的将要添加到下次提交里的内容
  $ git diff --staged 
  diff --git a/README b/README
  new file mode 100644
  index 0000000..03902a1
  --- /dev/null
  +++ b/README
  @@ -0,0 +1 @@
  +My Project
  ```

+ 提交更新

  ```console
  $ git commit -m "Story 182: Fix benchmarks for speed"
  [master 463dc4f] Story 182: Fix benchmarks for speed
   2 files changed, 2 insertions(+)
   create mode 100644 README
  ```

+ 跳过使用暂存区域

  跳过add这步，直接使用git commit -a -m "提交说明"，完成本次提交。

  ```console
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
      modified:   CONTRIBUTING.md
  
  no changes added to commit (use "git add" and/or "git commit -a")
  $ git commit -a -m 'added new benchmarks'
  [master 83e38c7] added new benchmarks
   1 file changed, 5 insertions(+), 0 deletions(-)
  ```

+ 移除文件

  `git rm` 命令后面可以列出文件或者目录的名字，也可以使用 `glob` 模式。 比方说：

  ```console
  $ git rm log/\*.log
  ```

  注意到星号 `*` 之前的反斜杠 `\`， 因为 Git 有它自己的文件模式扩展匹配方式，所以我们不用 shell 来帮忙展开。 此命令删除 `log/` 目录下扩展名为 `.log` 的所有文件。 类似的比如：

  ```console
  $ git rm \*~ #该命令为删除以 `~` 结尾的所有文件。
  ```

  如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 `-f`（译注：即 force 的首字母）。 

  

  另外一种情况是，我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。 换句话说，你想让文件保留在磁盘，但是并不想让 Git 继续跟踪。 当你忘记添加 `.gitignore` 文件，不小心把一个很大的日志文件或一堆 `.a` 这样的编译生成文件添加到暂存区时，这一做法尤其有用。 为达到这一目的，使用 `--cached` 选项：

  ```console
  $ git rm --cached README
  ```

+ 移动文件

  ```console
  $ git mv README.md README
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
      renamed:    README.md -> README
  ```

# todolist 

[看到第8页查看提交历史]: https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%91%BD%E4%BB%A4%E8%A1%8C

