mysql(5.6.50)安装 [https://www.cnblogs.com/zsg88/p/7533437.html](https://)

git安装

git设置

```bash
git config --global user.name "Your name"
git config --global user.email "your email"

```

创建版本库

```bash
mkdir fileName
cd fileName
git init
```

把文件添加到版本库

```bash
git add file
git commit -m "comment"
```

查看状态

```bash
git status
```

查看修改内容

```bash
git diff
```

查看提交的历史版本信息

```bash
git log 
git log --pretty=oneline
```

版本回退

HEAD是指向当前版本

cmd中HEAD^^指上一个版本，BASH中指上两个版本

```bash
git reset --hard HEAD^^
git reset --hard HEAD~1

git reset --hard HEAD~n
```

在不同版本间切换

```bash
git reset --hard <commitID>
```

查看历史命令

```bash
git reflog
```

撤销修改

1. 工作区（没有git add），使用git checkout --file
2. 暂存区（已经git add后），使用git reset HEAD file ，再使用git checkout --file
3. 版本库（git commit 后），使用git reset 回退版本
4. 推送远程，完

删除（版本库的）文件(相对于 git add file）

```bash
git rm file
```

远程仓库github的设置

1. 主用户目录下(C:\Users\Administrator\)创建.ssh文件夹，生成自己的私钥和公钥(id_rsa和id_rsa.pub)
   ```bash
   ssh-keygen -t rsa -C "YourEmail@xxx.com"  # GIT BASH窗口
   ```
2. 在github设置的SSH Keys设置下添加公钥（id_rsa.pub文件的内容复制到Key）

已有本地库，添加github远程库

```bash
# 在github创建仓库learngit
git remote add origin git@github.com:muiz-lee/learngit.git #关联远程库 origin是远程库名  git@github.com:muiz-lee/learngit.git是远程仓库的真实地址
git push -u origin main # 第一次上传本地库内容 origin是远程库名 main是分支名，此处用master分支会一直报错，不知道为啥
git push origin main # 非第一次上传
```

```bash
git show-ref #显示远程分支
git branch -M main# 
git remote rm origin # 删除远程库origin
```

从远程库克隆

```bash
git clone git@github.com:muiz-lee/gitskills.git
```

分支

```bash
git branch # 查看分支
git branch <name> # 创建分支
git checkout <name>     git switch <name> # 切换分支
git checkout -b <name>    git switch -c <name>  # 创建并切换分支
git merge <name> # 合并某分支到当前分支
git branch -d <name> # 删除分支
git branch -D <name> # 强行删除一个没有被合并过的分支
git log --graph # 查看分支合并图

# 临时去修复bug
git stash  # 把dev分支工作区暂时没完成的暂存起来，临时去干其他
git stash list # 查看暂存
git stash apply # 暂存恢复  git stash drop # 删除暂存
git stash pop #暂存恢复且删除

git cherry-pick <commit ID> # 把bug已提交的修改同步（复制）到当前分支，避免重复劳动
```

* [ ] 尝试cherry-pick功能
* [ ] 弄清楚什么情况下会冲突 （两个合并的分支同时都做了修改）

标签

```bash
# 新建标签
git tag <name> 
git tag <name> <commitID> 
git tag -a <name> -m <comment>
# 查看标签
git tag
git  show <tagname>
# 推送标签到远程
git push <branchname> <tagname>
git push <branchname> --tags # 推送所有
# 删除标签
git tag -d <tagname>
# 删除远程标签
git push origin:refs/tsgs/<tagname>
```

github使用

1. fork
2. clone
3. pull request

自定义git

```bash
git config --global color.ui true # git显示颜色
```

忽略特殊文件

* 根目录下创建.gitignore文件
* 把需要忽略的文件加入进去
* 删除缓存(不删缓存，会无效），.gitignore文件也要放入版本库，提交
  ```bash
  git rm -r --cached .
  git add .gitignore
  git commit -m "xxx"

  # 强制添加一个被忽略的文件
  git add -f <filename>
  ```

配置别名

* 当前仓库的配置文件在 .git/config下，当前用户的配置文件在主目录.gitconfig文件中，别名配置都会显示在配置文件最后一项中

```bash
# 常用别名
git config --global alias.st status # git st = git status
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit" # git lg
```

搭建git服务器

git图形化工具 SourceTree