# Git
- [常用命令](#Git常用命令)
- [放弃本地修改-将本地代码更新到目前远程仓库最新的代码状态](#放弃本地修改)
- [强制push](#git强制push)
- [连接远程仓库](#git连接远程仓库)
- [上传本地代码到远程仓库](#上传本地代码到远程仓库)
- [提交本地到一个子分支并合并子分支到另外一个父分支](#git提交本地到一个子分支并合并子分支到另外一个父分支)
- [拉取远端分支到本地](#拉取远端分支到本地)
- [git分支更新主干/主干更新分支](#分支更新主干)
- [更新fork仓库的master分支为源仓库的分支](#更新fork仓库的master分支为源仓库的分支)
- [丢弃全部暂存区文件](#丢弃全部暂存区文件)
- [git里commit的时候-m描述写错了修改描述信息](#git里commit的时候-m描述写错了修改描述信息)
- [git merge解决冲突](#merge解决冲突)
- [将本地master分支回退为完全与主（源）仓master一致](#将本地master分支回退为完全与主仓master一致)

#### Git常用命令
- git add -u ：提交所有tracked files 到暂存区
- git add . ：提交所有tracked files 和 untracked files 到暂存区
- git remote -v ：显示所有远程仓库
    - git remote rm origin : 删除远程仓库
    - git remote add [origin] [url] : 添加远程仓库
- **git pull**
    - 将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并：git pull origin master:brantest
    - 如果远程分支是与当前分支合并，则冒号后面的部分可以省略：git pull origin master
- git fetch：从远程下载代码库（但并不合并）
- **git push**
    - git push：如果当前分支只有一个追踪分支，那么主机名都可以省略
    - git push origin [branch_name]
    - git push -f origin br_MXJ_nmm:br_ruu_nmm_mxj：git强制push
    - 一个罕见的难以解决的错误：

```
remote: Start Binary Checking for Branch 'br_Q2Rest' by Rule 'Default Setting'  [FAILED]
remote: Error: Binary file 'deployment/SMP/diagnose/1.xml.cms' is forbidden
remote: Error: exit status 1
To ssh://isource-dg.huawei.com:2222/l30007627/CorbaAgent.git
 ! [remote rejected]     br_Q2Rest -> br_Q2Rest (pre-receive hook declined)
error: failed to push some refs to 'ssh://isource-dg.huawei.com:2222/l30007627/CorbaAgent.git'
```
        出错原因：由于我当前所在分支就是 br_Q2Rest 分支 ,所以本地和远端的参数的默认分支名都是 br_Q2Rest，完整的push 参数可以这样写：
            git push -u lhz br_Q2Rest:br_Q2Rest  
- git log -x：查看最近x个版本：
- **git resert**
    - git reset 版本号：回滚到第几个版本
    - git reset --soft HEAD^:撤销commit的提交
- **git branch**
    - git branch XXX：创建分支
    - git branch：显示所有分支
    - git branch -vv：查看本地分支对应的远程分支
- **git checkout**
    - git checkout xxx：切换到指定分支
    - git checkout -- .   （**在commit的时候**）： 撤销全部修改
    - git checkout -f：简单的放弃本地修改-还原到一开始的状态
    - git checkout [版本号] -- [文件路径]

### 放弃本地修改
- git fetch origin master
- git reset --hard origin/master
- git push -f

### 将本地master分支回退为完全与主仓master一致
- git fetch origin master
- git reset --hard upstream/master
- git push -f
    - 注：如果遇到“ ! [remote rejected]     master -> master (pre-receive hook declined)”的问题，说明该分支还是保护分支，要到设置里去修改：
    - ![image](https://github.com/InterestingHui/Programming/assets/45201681/f61ae064-dd0d-48ad-aca5-84e431090eda)


### git连接远程仓库
- 方法1：手动添加远程分支并命名
- 先在一个文件夹里右键打开git bash
- 然后初始化：git init
- 然后输入git remote add origin2 [url]
- “git remote add [name] [url]”表示添加了一个远程仓库，该仓库的网址是url，现在起一个简写加name（如果是clone就是默认是origin）
- 方法2：clone克隆一个仓库
- 先在一个目录下打开git bash
- 直接输入 git clone [url] 克隆项目到本地（不用git init）
- 如果是分支：
- eg：git fetch origin master_2021_ddjsjr
- git checkout origin/master_2021_ddjsjr -b master_2021_ddjsjr_lh

### 上传本地代码到远程仓库
- 先git status 查看红色字知道哪些进行了修改
- 然后git add 指定文件或目录上传到暂存区
- 之后git commit把暂存区文件提交到当前分支
- 再git pull 更新到项目最新版本
- 最后在git push origin xx 到远程仓库（也就是上传到xx分支，一般xx就是上面提示的最右边青蓝色括号里的目录）
- 如果push失败了
- “由于我当前所在分支就是 br_Q2Rest 分支 ,所以本地和远端的参数的默认分支名都是 br_Q2Rest 整的push 参数可以这样写: git push -u lhz br_Q2Rest:br_Q2Rest”
- http://3ms.huawei.com/km/blogs/details/9617226

### git提交本地到一个子分支并合并子分支到另外一个父分支
- git branch
- git checkout [子分支]
- git add ...
- git commit -m ".."  (别忘了 -m)
- git branch （查看所有分支）
- git checkout [父分支名]
- git pull origin [父分支名]  (先更新父分支名的代码）
- git branch
- git checkout [子分支名]
- git rebase [父分支名]
- 注意这里要保证commit的东西已经全部commit的，如果有修改的没有add上去的话，就要git checkout 文件，也就是恢复这个文件，然后在git rebase
- (本地用TorToiseGit，revert是回退到之前的版本，也就是左边的版本；Diff能解决冲突，通过
- 本地使用TortoiseGit
- Revert是回退版本，也就是返回到左边的版本
- 打开的快捷键：右键+T+Enter+v
- 打开后双击能查看版本不同，点OK能回到左边版本
- Diff是解决文件冲突
- 打开的快捷键：右键+T+Enter+Enter
- Resolve 是解决冲突：也就是当将分支合并入主干（在分支：git rebase master）的情况下解决冲突的手段
- 解决冲突文件，解决后“git add 冲突文件”进行提交
- git rebase --continue  继续解决下一个冲突，直到冲突解决完毕
- git push origin [子分支] （注意这里就是在子分支）
（这里如果push失败有可能是还得先pull 子分支的远端分支）

### 拉取远端分支到本地
- 如果本地还没拉取过该project的相关分支
    - 运行代码：git clone -b [分支名] [ssh包链接]
    - eg:
        - git clone l00693105_from_master_US2022082100007 ssh://git@codehub-dg-g.huawei.com:2222/cis/obsd/dataplus/obs-oef/oef-framework.git
- 已经拉取过该project的相关分支
    - 切到该分支上  
    - 运行代码：git fetch [远端仓库名] [分支名]:[分支名]
    - eg:
        - git fetch origin master:master 

### 分支更新主干
- 拉取主干到分支
    - git checkout master 
    - git pull 
    - git checkout dev
    - git merge master 
- 合并分支到主干
    - git checkout dev
    - git pull
    - git checkout master
    - git merge dev

### 更新fork仓库的master分支为源仓库的分支
- （如果还没添加源仓库）：git remote add upstream [源仓库ssh资源包]
- （如果已经添加，找到源仓库的仓库名，这里假设取出为upstream）：git remote -v 
- git fetch upstream
- git checkout master
- 此时到了本地的fork仓库的master分支
- git merge upstream/master
- 合并最新master
- git push
- 推到fork仓库，完成更新

### 丢弃全部暂存区文件
- git clean -dfx
- git checkout .

### git里commit的时候-m描述写错了修改描述信息
- https://blog.csdn.net/kaimo313/article/details/107942861

### merge解决冲突
- 通过Jetbrain IDE进行冲突解决，点击左上角Commit，再点击resovle confict，进行冲突解决
- 解决完成后，输入git commit，注意这次就没有-m 描述信息了，但是输入完后要在第一行新增单号
- 再git push

### 回退
- git reset --hard HEAD^ 回退到上一个版本
- git reset --hard HEAD~3 回退到历史倒数第三个版本
- git checkout commit [id]回退到指定版本
