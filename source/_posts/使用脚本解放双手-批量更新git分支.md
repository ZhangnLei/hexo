---
title: 使用脚本解放双手 - 批量更新git分支
date: 2020-04-29 09:42:09
tags:
- shell
- git
---

# 使用脚本批量更新git分支

@auther `张念磊`
@date `2020/4/29`

[toc]

### 目的

使用脚本，解放双手

### 先上代码

```shell
#!/bin/bash

function readfile ()
{
 for file in `ls $1`
 do
# 判断是否是文件夹，如果是文件夹则删除文件夹中的 dev test release 分支
 if [ -d $1"/"$file ]
 then
  cd ${file}
  pwd
  git checkout master;
  git branch -D dev; git branch -D test; git branch -D release;
  # git checkout master; git pull;
  cd ..
 fi
 done
}
readfile "./"

echo '完美的运行！'
```


代码思路：
1. for循环遍历当前文件夹下的文件
2. 判断每个文件的类型是否是文件夹
3. 如果是文件夹则进入该文件夹中，
4. 切换master分支，避免下面一步时删除分支失败（git 删除分支时是不能删除当前所在的分支的，例如 当前在dev分支，执行git branch -D dev 时会提示Cannot delete branch 'dev'...）
5. 删除文件夹中的 dev test release 分支
4. 最后打印运行结束

### 使用方法

1. 准备shell
   1. 新建文本文档，将以上代码copy进来，保存命名为`clear-git-branch.sh` 一定要以`.sh`为文件后缀
   2. 将文件放在需要批量更新代码的文件夹中

文件结构大概长这样：

![image-20200429094911638](https://tva1.sinaimg.cn/large/007S8ZIlgy1geaeceaslhj30ty0h6q7s.jpg)

2. 运行脚本

   `window平台：`

   ​	方式1：双击运行shell脚本；

   ​	方式2：使用GitBash工具

   ​		先切换到存放代码的目录，然后执行代码：

   ```shell
   ./clear-git-branch.sh
   ```

   `macOS或Linux平台：`

   需先给shell脚本添加执行的权限：

   ```
   chmod +x clear-git-branch.sh
   ```

   然后运行

   ```shell
   ./clear-git-branch.sh
   ```

   

运行效果:
```shell
$ ./clear-git-branch.sh
/f/code/sycode/dcit-serxxxxxxxx
Already on 'master'
Your branch is up to date with 'origin/master'.
Deleted branch dev (was 6c999e7).
Deleted branch test (was a4238eb).
Deleted branch release (was 6603884).
Switched to a new branch 'dev'
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
Switched to a new branch 'test'
Branch 'test' set up to track remote branch 'test' from 'origin'.
Switched to a new branch 'release'
Branch 'release' set up to track remote branch 'release' from 'origin'.
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
....
```



### 注意事项

1. 该脚本会把所有仓库的分支切换到master分支，如后续开发需要自己手动切回自己的特性分支。

2. 可能会有失败的案例，当你的分支在dev/test/release且有正在编辑的代码，则会删除失败。

对于这种情况需要自行判断是否保存并加以处理。



### 大功告成

完美，哈哈。

刚开始学习shell，有错误还请大佬指出。