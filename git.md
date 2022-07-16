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
