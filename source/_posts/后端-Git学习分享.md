---
title: 后端 - Git学习分享
date: 2020-04-18 19:22:42
tags: 
- Git
- rebase
- cherry-pick
---

# 后端 - Git学习分享

[toc]

@auther `张念磊`
@date 2020/2/17

## 一个学习git的网站

[https://learngitbranching.js.org/](https://learngitbranching.js.org/)



```shell
# 基础
git checkout -b hotfix # 新建一个分支

git checkout C2 # 分离head
git branch -f master C2 # 将分支指向提交C2
git branch -f master HEAD^ # 将master指向HEAD的上一个节点
git branch -f master HEAD~3 # 将master指向HEAD的前面第三个节点
git reset Head^ # 撤销一次本地提交
git revert HEAD^ # 撤销一次远程提交

git rebase master # 改变代码提交的顺序
git cherry-pick C2 C3 # 将C2 C3次提交添加到当前分支 git cherry-pick 'commit id'  # 复制一个特定的提交到当前的分支
git rebase -i HEAD~4 # 交互式rebase最近的4次提交
```



![image-20200218102321108](https://tva1.sinaimg.cn/large/007S8ZIlly1gdy53zzv41j30z50q90v5.jpg)



示例 ： 把分支以图像的方式展现给用户

![image-20200218220559729](https://tva1.sinaimg.cn/large/007S8ZIlly1gdy542q42ej30ql0fggn3.jpg)



### 通关截图

![image-20200218225905225](https://tva1.sinaimg.cn/large/007S8ZIlly1gdy5414r55j30yq0rtmzv.jpg)



主要介绍的两个命令 rebase cherry-pick 

![image-20200327160103150](https://tva1.sinaimg.cn/large/007S8ZIlly1gdy53yvq4nj30q00pj0um.jpg)



## 配置别名

有没有经常敲错命令？比如`git status`

如果敲`git st`就表示`git status`那就简单多了，当然这种偷懒的办法我们是极力赞成的。

我们只需要敲一行命令，告诉Git，以后`st`就表示`status`：

```
$ git config --global alias.st status
```

好了，现在敲`git st`看看效果。

当然还有别的命令可以简写，很多人都用`co`表示`checkout`，`ci`表示`commit`，`br`表示`branch`：

```
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
```

提交就可以简写成：

```
$ git ci -m "bala bala bala..."
```

`--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。



`git log `

![image-20200327154624267](https://tva1.sinaimg.cn/large/007S8ZIlly1gdy53zj3urj317w0u0dke.jpg)


甚至还有人丧心病狂地把`lg`配置成了：

```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

来看看`git lg`的效果：

<img src="https://tva1.sinaimg.cn/large/00831rSTgy1gd8j6l772pj317w0u015d.jpg" alt="image-20200327154509668" style="zoom: 50%;" />





## 其他操作：

连接远程仓库
**git remote add origin 仓库地址**

查看远程连接
**git remote -v**

git取消与远程仓库的连接
**git remote remove origin**