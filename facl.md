
### 设置文件other权限和默认访问权限
设置完毕后，在该目录下创建新文件，会继承父目录的权限 
```
setfacl -m o::rwx <路径>
setfacl -m d:o::rwx <路径>
```
