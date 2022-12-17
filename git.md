# git常见命令

查看远程分支信息
```
git remote -v
```

修改远程分支地址
```
git remote set-url origin http://192.168.3.4:3000/zhunzhong/test.git
git remote set-url origin http://192.168.3.4:3000/lzkj/base-swap.git
git remote set-url origin http://192.168.3.4:3000/lzkj/test-swap.git
```

查看本地所有分支
```
git branch -a
```

查看所有远程分支
```
git branch -r
```

切换到指定分支，并更新工作区域
```
git checkout dev
```

本地新建一个分支(dev)，并且切换到该分支 与远程分支(origin/dev)对应
```
git checkout -b dev origin/dev
```



从某个远程分支创建新的分支并推送到远程仓库

```
#切换到dev分支
git checkout dev

#拉取最新代码
git pull

#创建本地分支
git checkout -b dev-test

#推送到远程仓库
git push origin dev-test

#将本地分支与远程分支关联
git branch --set-upstream-to=origin/dev-test dev-test
```



分支合并（将master分支内容合并到dev分支）

```
#切换到你所在分支dev
git checkout dev

#master分支合并到dev分支
git merge master

#将本地内容push到dev分支
git push

#合并如果有冲突可以取消本次merge
git merge --abort
```



查看分支操作记录

```
git reflog
```



修改刚刚提交的commit

```
#有时候我们刚刚commit提交完，这时发现漏掉了几个文件没有添加，或者可能提交信息写错了。这时，我们可以使用带有--amend选项commit命令，修改提交信息
git commit --amend

```



取消merge、commit记录

```
找到合并前的commit-id
#还原到指定版本
git reset --hard a1d566d

#还原到上一版本（回退版本库，暂存区，工作区。（因此我们修改过的代码就没了，需要谨慎使用）
#删除工作空间改动代码，撤销commit，撤销git add 
git reset --hard HEAD~1

#撤回commit操作，本地修改或者新增的代码仍然保留。就是说本地代码没有变动
#不删除工作空间改动代码，撤销commit，不撤销git add
git reset --soft HEAD~1

#回退版本库，暂存区。(--mixed为git reset的默认参数，即当任何参数都不加的时候的参数)
#意思是：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作
#这个为默认参数,git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的
git reset HEAD~1

#合并如果有冲突可以取消本次merge
git merge --abort
   
```



git还原修改

```
还原有三种情况：

【1】只是修改了文件，没有任何 git 操作
【2】修改了文件，并提交到暂存区（即：编辑之后，进行git add 但没有 git commit -m "留言xxx"）
【3】修改了文件，并提交到仓库区（即：编辑之后，进行git add 并且 git commit -m "留言xxx"）

#情况1
git checkout -- aaa.html // 指定还原`aaa.html`文件
git checkout -- * // 还原所有文件

#情况2
git reset HEAD               // 回退到当前版本，默认是mixed
git checkout -- aaa.html

#情况3
git reset HEAD^     // 回退到上一个版本，注意看HEAD后面有个 ^HEAD^ 是回退到上个版本HEAD^^ 是回退到上上个版本HEAD~数字 是回退到数字个版本，也可以用数字1,2，3（HEAD~1,HEAD~2）
git checkout -- aaa.html
```



查看提交日志记录

```
#默认查看日志详情
#git log 默认会显示全部的详细的提交日志，提交的 ID、作者、日期、还有提交的描述。
#按下 f 键可以向下翻页，b 键可以向上翻页、 q 可以退出显示
git log 

#看简化的信息
git log --oneline

#看指定时间之前
git log --oneline --before='2019-2-18'
git log --oneline --before='1 day'
git log --oneline --after='1 week'
```

同步远程仓库所有分支

```
git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done 
git fetch --all 
git pull --all 
```

删除本地分支

```
git branch -d dev
-d是--delete的缩写,在使用--delete删除分支时,该分支必须完全和它的上游分支merge完成(了解上游分支,可以点击查看链接),如果没有上游分支,必须要和HEAD完全merge

-D是--delete --force的缩写,这样写可以在不检查merge状态的情况下删除分支

--force简写-f,作用是将当前branch重置到初始点(startpoint),如果不使用--force的话,git分支无法修改一个已经存在的分支.
```



删除远程分支

```
git push origin -d dev
删除远程分支dev
```



# git常见问题

fatal: The remote end hung up unexpectedly

```
#文件过大，设置文件缓存将Http缓存设置大一些，比如1G
git config --global http.postBuffer 1048576000
```

