# git常见命令

查看远程分支信息
```
git remote -v
```

修改远程分支地址
```
git remote set-url origin http://192.168.3.4:3000/zhunzhong/test.git
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

