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

4. 版本的回退
    $ git log # 查看git的版本信息
    $ git log --pretty=oneline
    $ git reflog # 可查看git的操作记录
    $ git reset --hard HEAD^ # 回退上一个版本，HEAD^^再上一个版本
    $ git reset --hard <commit it> # 根据commit id来回滚版本

远程仓库