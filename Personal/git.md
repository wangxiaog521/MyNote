# windows:
* 1. 安装git软件后需配置秘钥信息
    gitlab或github都会配有ssh信息，在本地生成秘钥信息后在setting中增加ssh key即可   

2. 首次需要配置好本地git环境
git clone git@github.com:wangxiaog521/MyNote.git

也可直接通过git pull将主干同步到本地
git pull git@github.com:wangxiaog521/MyNote.git

3. 本地新建分支，修改提交，推送到远程分支 
# 切换到主干
git checkout master

# 创建分支，名为：20170208
git checkout -b 20170208

# 本地删除分支20170208
git branch -D 20170208

# 增加
git add .

# 查看状态
git status

# 撤销文件的修改
git reset filename
git checkout filename


# 提交
git commit -a -m "comments"

# push
git push origin 20170208

git push git@github.com:wangxiaog521/MyNote.git
git push --set-upstream git@github.com:wangxiaog521/MyNote.git master
git push -f --set-upstream git@github.com:wangxiaog521/MyNote.git master



For git reference: http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

1. install git
    a. sudo apt-get install git
    b. 下载源码后解压：./config，make，sudo make install
    c. 配置本地信息
        $ git config --global user.name "Your Name"
        $ git config --global user.email "email@example.com"
        注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置


1. 在本地空文件夹内初始化git
    $ git init

2. 正常提交流程
    $ git diff # 对比当前修改与上次修改的区别，一旦add或者commit后，diff不会显示差异
    $ git add/rm filename
    $ git diff HEAD -- filename # add后可通过此命令对比差异
    $ git commit -m 'describer your change'

    $ git status # 随时check git的状态

3. 撤销流程
    a. 没有add的情况下
        $ git checkout -- filenmae
    b. 已经add
        $ git reset HEAD filename # 从缓存区移除
        $ git checkout -- filename # 即是a的操作



远程仓库

___

## git常用简短命令
```
# 在一个空文件夹中初始化git
git init

# git配置, --global为全局，不加表示只对本项目生效
git config --global user.name shawn
git config --global user.mail xxx@xxx.com
git config -l # git配置查看
git config --global --edit # 编辑全局配置
git config core.filemode false # false不关心文件的权限，true - git会将权限的改变也记录下来
git config core.safecrlf fase # 不转换
git config core.safecrlf true # 提交时转换为LF，checkout时转换为CRLF
git config core.safecrlf input # 提交时转换为LF，checkout时不转换
git config core.safecrlf true # 拒绝提交包含混合换行符的文件
git config core.safecrlf false # 允许包含不同换行符
git config core.safecrlf warn # 提交不同换行符时发出警告


# 显示工作区/暂存区与HEAD的区别
git status
git status -s # 简短显示
git status -vv # 显示所有修改的内容
git status -vv -- a.txt # 只显示a.txt文件被修改的内容
git status -uno # 不显示未托管的文件
git status -uall # 显示全子文件夹中文件的改变
git status --ignored # 显示.gitignore中被忽略的文件
git status -- a.txt/a # 只显示文件a.txt/目录a的修改情况；-- 后面跟文件

# 显示差异
git diff # 工作目录与索引之间的差异
git diff --cached # 暂存区与索引之间的差异，不用工作区比较，而用暂存区
git diff HEAD~1 # 工作目录与上一个提交之间的差异
git diff commit # 工作目录与指定commit之间的差异
git diff commit1 commit2 # 两个commit之间的差异
git diff master~5 master git-add.txt # 比较git-add文件，当前和前5个版本的差异
git diff --ignore-all-space # 比较的时候忽略所有的空格
git diff --ignore-space-at-eol # 忽略行尾的空格
git diff --ignore-space-change # 忽略空格的改变，如一个变两个
git diff --ignore-blank-lines # 忽略空行
git diff --stat # 只显示修改的信息
git diff --diff-filter=D # 只显示指定状态的修改，D-删除，A-增减，M-修改
git diff -G"common" # 只显示满足条件的改动，如只包含common关键字的修改

# 显示分支情况
git branch # 列出本地所有分支
git branch dev # 新建一个dev分支，但不切换
git branch -d/-D # 删除一个分支， D-强制删除
git branch -m # 将当前分支重命名
git branch -r # 列出远程分支
git branch -a # 列出所有分支，本地以及远程
git branch --list <pattern> # 类似grep，支付通配，"*2.0*"表示包含2.0关键字的分支
git branch -v/-vv # 列出分支详细信息
git branch -a -vv --list "*master*" # 查看本地以及远程master分支的情况
git branch --set-upstream-to=origin/master # 将本地分支与远程分支关联
git branch --contains [commit] # 包括制定commit的分支

#显示分支信息
git show-branch -a # 显示所有分支
git show-branch -r # 显示所有远程分支
git show-branch --more=<n> # 显示共同提交后的n个额外提交
git show-branch <pattern> # 只显示满足条件的分支

# 显示远程分支origin的详细信息
git remote -v
git remote update # 获取远程分支情况

# 切换分支
git checkout dev # 切换到dev分支
git checkout -b test # 创建test分支并切换到test分支
git checkout -b test [<start point>] # 从指定点开始创建分支并切换
git checkout --detach [<branch>] # 到detach点工作
git checkout -f # 强制切换
git checkout -- <file> # 恢复文件


# 将工作区修改添加到暂存区
git add . # 将所有的修改都添加到暂存区
git add -A # 效果同上
git add a.txt b.xt # 逐个将a.txt, b.txt等文件添加到暂存区
git add -- file # 只增加指定文件
git add a/\*.txt # 将目录a下面所有以txt结尾的文件全部添加到暂存区
git add -u # 只处理修改删除的文件，对于新增文件不做任何处理

# 回滚到HEAD头
git reset # 重置暂存区，工作区修改保持不变，回到HEAD
git reset HEAD~1 # 重置暂存区，工作区修改保持不变，回到上一个版本
git reset -mixed # 同上
git reset a.txt # 将文件a.txt从暂存区放回工作区
git reset --hard # 将所有托管文件全部回滚到头部，未托管的文件不会变
git reset --soft 49ce45d00196ffe1 # 工作区暂存区都不变，回滚到指定版本
git reset --soft HEAD~1 # 工作区暂存区都不变，回滚到上一个版本，两个版本差异显示在暂存区

# 提交
git commit # 第一行写title，空一行后写内容，直接退出vi编辑则放弃提交
git commit -a # 直接将修改或者删除文件提交，未托管文件不管
git commit -m 'comments' # 简短说明提交
git commit --allow-empty-message # 允许提交信息为空
git commit --amend # 修复当前提交信息, 可以提交新修改或者删除的文件，再执行此命令
git commit -v # 显示修改内容
git commit -- file-name # 只提交指定文件

# 回滚已提交的某一个版本
git revert b45b5 # 只回滚某一个提交，commit操作的逆操作，并生成一个新的提交
git revert -n b45b5 # 同上操作，不会新生成一个commit
git revert --continue # 上一步操作的继续
git revert -n master~5..master-2 # 一次回滚多个commit
git revert -n master~5 master~2 # 一次回滚多个commit

# 显示历史
git log
git log -p # 显示内容已经差异
git log -n # 显示最近n次提交
git log --stat # 显示提交的增删情况
git log --pretty=oneline # 精简显示到一行
git log --graph # 显示树结构
git log --name-only # 显示修改的文件名
git log --name-status # 显示修改文件名的方式，M还是A还是D，即修改增加还是删除
git log --abbrev-commit # 显示短的commit hash值
git log -- file-name # 只展示指定文件的历史
git log --grep='xxx' # 只展示包含关键字的提交
git log -S testNotSupportsOther # 搜索某个文件中具体改动的点相对应的提交
git log -p -L 10,12:package.json # 指定文件package.json里面10到12行被改动的提交
git log --oneline --decorate # 显示指向这个提交的引用，如标签分支
git log <since>..<until> # git log master..feature,包含了在feature分支而不在master分支中所有的提交
git log 1c12b23..8e8f8c3 # 两次提交中间的提交

# 显示操作历史
git reflog # 显示操作信息，精简到一行
git reflog show # 同上
git reflog # 等价于git log -g --abbrev-commit --pretty=oneline 
git reflog --decorate # 显示分支信息
git reflog --stat # 显示增删改统计信息
git reflog --pretty=full --no-abbrev # 以git log的方式呈现
git reflog expire # 删除过期的ref，尽量不要使用
git reflog delete # 删除ref，尽量不要使用


# 显示标签
git tag
git tag -l <patter> # 显示指定版本，支付通配符，"v1.3*"表示列出1.3打头的版本
git tag <tagname> # 创建轻量级标签，指向commit
git tag -a v1.4 -m "my version 1.4" # 创建标签并添加注解
git tag -a v1.4 9fceb02 # 根据指定commit创建标签

# 放到暂存区
git stash
git stash save "comment" # 修改放到暂存区，并添加注释
git stash list # 显示所有暂存区信息
git stash pop # 弹出头部暂存区修改
git stash show stash{0} # 显示暂存区修改的统计信息
git stash show -p stash{0} # 显示暂存区修改的具体内容
git stash pop [<stash{n}] # 弹出具体的stash，默认弹出最上面
git stash clear # 清空所有stash
git stash apply # 与pop类似，只是stash还是列表中，不会被丢弃
git stash drop # 丢弃某一个stash

# git查找，从当前工作目录后者历史提交中查找
git grep xxx
git grep -n xxx # 显示行号
git grep --name-only xxx # 只显示文件名
git grep -c xxx # 每个文件多少个匹配
git grep config 513353b8e7580df1ca6f24eccdd2cf4c126855a1 # 指定的commit上查找
git grep -e '#define' --and -e 'SORT_DIRENT' # 包含给定两个串
git grep 'time_t' -- '*.[ch]' # 在所有的*.c 和*.h中找time_t

# 查看提交对应的树
git rev-parse  9ae638fff5d378b078b77a57f154aa28bade5b27^{tree}
git cat-file -p 9ae638fff5d378b078b77a57f154aa28bade5b27

# 其他
git show HEAD # 显示对象信息
git show HEAD^{tree} # 显示树里面的内容
git show 9ae638ff:pom.xml # 显示某次提交中文件信息
git show v1.4.0.RELEASE:pom.xml # 显示某个tag下文件信息，git tag来显示tag
git ignore # 忽略文件
git mv # 移动文件/重命名，保留历史信息
git archive master | gzip > project.tar.gz # 打包master分支
    --prefix=<prefix> / 指定打包文件的前缀
    --verbose 显示进度
    - 0 指定输出的tar/zip文件
    --format=(tar or zip) 指定文件类型
```

## 查看修改内容
```
git diff # 简短显示修改内容
git status -vv # 详细显示修改内容
```

## git log高级用法
```
# 自定义格式化显示
git log --pretty=format:"%h - %an, %ar : %s"
# 具体格式有以下：
%H  提交对象（commit）的完整哈希字串
%h  提交对象的简短哈希字串
%T  树对象（tree）的完整哈希字串
%t  树对象的简短哈希字串
%P  父对象（parent）的完整哈希字串
%p  父对象的简短哈希字串
%an 作者（author）的名字
%ae 作者的电子邮件地址
%ad 作者修订日期（可以用 -date= 选项定制格式）
%ar 作者修订日期，按多久以前的方式显示
%cn 提交者(committer)的名字
%ce 提交者的电子邮件地址
%cd 提交日期
%cr 提交日期，按多久以前的方式显示
%s  提交说明

git log --since=2.weeks # 显示2周内改动
git log --since/--after # 仅显示指定时间之后的提交。
git log --until/--before # 仅显示指定时间之前的提交。
git log --author # 仅显示指定作者相关的提交。
git log --committer # 仅显示指定提交者相关的提交
git log --no-merges # 不展示merge

# 指定格式展示，指定作者，指定时间，不展示merge
git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \ --before="2008-11-01" --no-merges

```

## 所有修改全部抛弃
* 方法一
```
# 全部提交到暂存区后，再用硬重置
git add .
git reset --hard
```

* 方法二
```
# 全部回推到工作区后，再用clean命令 
git reset --hard
git clean -df
```


## 回滚版本后如何重新往回恢复
```
[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git log
commit db6f1c189b293303921a5e86446b084bb8114088
Author: Shawn Wang <xiaogang.wxg@alipay.com>
Date:   Sun Jul 29 18:49:28 2018 +0800

    commit a.txt

commit 49ce45d00196ffe164b142f78984c626961442c9
Author: Shawn Wang <xiaogang.wxg@alipay.com>
Date:   Sun Jul 29 18:18:23 2018 +0800

    second line

commit de2c2b2e51092b68787d81aa8fdcde4c7e8a8270
Author: Shawn Wang <xiaogang.wxg@alipay.com>
Date:   Sun Jul 29 17:50:27 2018 +0800

    this is first commit for git

    1.this commit add a new file to git
    2.
    3.

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git reset --soft HEAD~1

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git log
commit 49ce45d00196ffe164b142f78984c626961442c9
Author: Shawn Wang <xiaogang.wxg@alipay.com>
Date:   Sun Jul 29 18:18:23 2018 +0800

    second line

commit de2c2b2e51092b68787d81aa8fdcde4c7e8a8270
Author: Shawn Wang <xiaogang.wxg@alipay.com>
Date:   Sun Jul 29 17:50:27 2018 +0800

    this is first commit for git

    1.this commit add a new file to git
    2.
    3.

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   a.txt

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git checkout db6f1c189b293303921a5e86446b084bb8114088
Note: checking out 'db6f1c189b293303921a5e86446b084bb8114088'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at db6f1c1... commit a.txt

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git status
HEAD detached at db6f1c1
nothing to commit, working tree clean

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git branch -D master
Deleted branch master (was 49ce45d).

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git branch master

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git checkout master
Switched to branch 'master'

```

## git查看commit/tree/block信息
[相关参考文档](http://blog.xiayf.cn/2013/09/28/learning-git-internals-by-example/)
```
$ git log
commit de2c2b2e51092b68787d81aa8fdcde4c7e8a8270
Author: Shawn Wang <xiaogang.wxg@alipay.com>
Date:   Sun Jul 29 17:50:27 2018 +0800

    this is first commit for git

    1.this commit add a new file to git
    2.
    3.

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git cat-file -t de2c2b2e51092b68787d81aa8fdcde4c7e8a8270
commit

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git cat-file -p de2c2b2e51092b68787d81aa8fdcde4c7e8a8270
tree fedca787275de772ba4e0daf6b7de0780d45099f
author Shawn Wang <xiaogang.wxg@alipay.com> 1532857827 +0800
committer Shawn Wang <xiaogang.wxg@alipay.com> 1532857827 +0800

this is first commit for git

1.this commit add a new file to git
2.
3.

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git cat-file -t fedca787275de772ba4e0daf6b7de0780d45099f
tree

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git cat-file -p fedca787275de772ba4e0daf6b7de0780d45099f
100644 blob 3d96ca117018f5f610905bb5aa8499d858bc050d    readme.txt

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git cat-file -t 3d96ca117018f5f610905bb5aa8499d858bc050d
blob

[Shawn@ShawndeMacBook-Pro.local /Users/Shawn/git/github/gittest]
$ git cat-file -p 3d96ca117018f5f610905bb5aa8499d858bc050d
this is a git demo
```

## tree-ish/commit-ish
| commit-ish/tree-ish | Example |
| --- | --- |
| 1. <sha1> | f525764bf1b4e6bc41389e9a259dbc67487d6cf5 | 
| 2. <describeOutput> | v1.7.4.2-679-g3bee7fb |
| 3. <refname> | master, heads/master, refs/heads/master |
| 4. <refname>@{<data>} | master@{yesterday}, HEAD@{5 minutes ago} |
| 5. <refname>@{<n>} | master@{1} |
| 6. @{<n>} | @{1} |
| 7. @{-<n>} | @{-1} |
| 8. <refname>@{upstream} | master@{upstream}, @{u} |
| 9. <rev>^ | HEAD^, v1.5.1^0 |
| 10. <rev>~<n> | master~3 |
| 11. <rev>^{<type>} | v0.99.8^{commit} |
| 12. <rev>^{} | v0.99.8^{} |
| 13. <rev>^{/<text>} | HEAD^{/fix nasty bug} |
| 14. :/<text> | :/fix nasty bug |
| Tree-ish only | Example |
| 15. <rev>:<path> | HEAD:README, :README, master:./README |
| 16. :<n>:<path> | :0:README, :README |

```
git show HEAD^ # 直接父亲
git show a5bec^^ # 前两个提交
git show HEAD~6 # 当前头部的钱6个提交
git reflog <ref> # shows a log of where your ref has been 
git show HEAD@{0} # 当前头部
git show HEAD@{2} # second prior value of HEAD
git show master@{0} # current master
git show master@{yesterday} # where master was yesterday
git shwo master@{1.week.ago} # where master was a week ago
git show amster:a.txt # 当前master分支的a.txt文件
git show :1:a.txt # 合并基础
git show :2:a.txt # 我们的
git show :3:a.txt # 他们的
@{-n} # 前n个分支
@{n} # 访问当前branch的reflog
<rev>^{} # 当前tag所指向的对象
:/balabala # 搜索commit msg

```

## git配置比较工具git difftool
```
# difftool配置
git config --global diff.tool bc4
git config --global difftool.bc4.cmd "D:...exe" "$LOCAL" "$REMOTE"
git config --global difftool.prompt false
# mergetool配置
git config --global merge.too bc4
git config --global mergetool.bc.cmd "D:...exe" "$LOCAL" "$REMOTE" "$BASE" "$MERGED"
git config --global mergetool.bc4.trustExitCode True
```


## 合并以及rebase
* merge
```
git checkout feature
git merge master
git merge master featrue

# 合并冲突
$ git ls-files -u # 查看当前merging下冲突文件情况
100644 4e9934d5da3d77d5f1272519b2027bcfb3837242 1   a.txt # 合并之前的
100644 efeb80de5dc6ba3094ee8b99bbe93fe3860a3db7 2   a.txt # 我们的改动
100644 4754ba9c385ef94994265490c007686be12574a2 3   a.txt # 他们的改动
$ git cat-file -p 4e9934d5da3d77d5f1272519b2027bcfb3837242
adfadf`aa
$ git cat-file -p efeb80de5dc6ba3094ee8b99bbe93fe3860a3db7
modify from master
adfadf`aa
$ git cat-file -p 4754ba9c385ef94994265490c007686be12574a2
dafdad
adfadf`aa

# 也可以用tree-ish
$ git show :1:a.txt
adfadf`aa
$ git show :2:a.txt
modify from master
adfadf`aa
$ git show :3:a.txt
dafdad
adfadf`aa

# 显示差异
git diff :3:a.txt :2:a.txt

# 解决冲突
git checkout --ours -- a.txt # 就用我们的
git checkout --theirs -- a.txt # 就用他们的

git add .
git commit .
```

* rebase
```
# 用法
git rebase [-i | --interactive] [options] [--exec <cmd>] [--onto <newbase>] [<upstream> [<branch>]]
git rebase --continue | --skip | --abort | --quit | --edit-todo
    # if branch is specified, git checkout branch会自动执行
    # if the --onto option is not specified, the starting point is <upstream>

git rebase --onto old_base new_base branch # 新老rebase替换

# 简单的
git checkout featrue
git rebase master

# 复杂的
# E--F--G--H--I--J topic
git rebase --onto topic~5 topic~3 topic # E--H`--I`--J`

git rebase -i 058ad3 # 修改任意提交，交互式rebase

# 解决冲突
git add .
git rebase --continue
```

* cherry-pick
```
$ git checkout dev
Switched to branch 'dev'
$ git log -3 --pretty=oneline
4b7a83f08ec9dc175f5e33630ed2a1aebfceef64 add d
97b75a7070562f737567637d28f4ebdf412a4f28 add c
b45b51f6501cc858d4fda4cf42684d85a35e8db3 commit from master

$ git checkout master
Switched to branch 'master'
$ git log -3 --pretty=oneline
b45b51f6501cc858d4fda4cf42684d85a35e8db3 commit from master
2894c43b1fb850f07f0e275bb2395466a34e747d test
ee5f7d4c5f329355bb6f0c70a1ebba8b29e3017f add new file a
$ git cherry-pick 97b75a7070562f737567637d28f4ebdf412a4f28
[master 58cef33] add c
 Date: Sun Aug 26 20:59:35 2018 +0800
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c.txt
 $ git log -3 --pretty=oneline
58cef33b8cb6888f1dc796b396b8fdb1be1132c6 add c
b45b51f6501cc858d4fda4cf42684d85a35e8db3 commit from master
2894c43b1fb850f07f0e275bb2395466a34e747d test

```

## 使用git补丁
```
# 普通补丁
git diff > patch # 生成差异文件
git apply --check patch # 在异地校验差异文件是否可用
git apply patch # 在异地应用差异文件
git apply patch -3 # 使用三元比对来应用差异文件，类似merge，若有冲突需解决

# 专业补丁
git format-patch HEAD~1 HEAD # 比较两个节点之间的差异并生成专业补丁
git format-patch -1 HEAD # -1表示生成1个节点的提交，-n表示n个
git am 001-form-dev.patch # 表示应用补丁，可以用*，表示多个
git am -3 001-from-dev.patch # 表示使用三方合并
```

## 使用钩子
钩子存放路径： .git/hooks
* pre-commit: 钩子在键入提交信息前运行
* prepare-commit-msg: 钩子在启动提交信息编辑器之前，默认信息被创建之后运行
* commit-msg: 钩子在接收一个参数，此参数即上下文提到的，存有当前提交信息的临时文件的路径
* post-commit: 钩子在整个提交过程完成后运行


## 其他
### 常用的git gui
* gitk
* TortoiseGit
* more: git-scm.com/downloads/guis/

### git blame
git blame <filename> # 列出每一行是谁写的
git blame -L 40,60 foo # 列出foo文件的40到60行是谁写的





