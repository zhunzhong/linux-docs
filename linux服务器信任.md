*******************
## 配置信任
将client端生成的sshkey 拷贝到server端authorized_keys 即可

```
#将公钥追加到authorized_keys文件末尾
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

```
#执行ssh命令到server如果不需要输入密码标识服务器信任配置成功
ssh root@10.4.12.3
```


********************
## 补充说明遇到如下问题可以参考
> 注1：这里不推荐用文件覆盖的方式，有些教程直接scp id_rsa.pub 到Client服务器的authorized_keys文件，会导致之前建的其他信任关系的数据被破坏，追加到末尾是更稳妥的方式；

> 注2： cat 完以后，Client服务器上刚才拷贝过来的id_rsa.pub文件就不需要了，可以删除或移动到其它地方）

> 注3：ssh-keygen 命令通过-b参数可以指定生成的密钥文件的长度，如果不指定则默认为1024，如果ssh-keygen –b 4096（最长4096），则加密程度提高，但是生成和验证时间会增加。对一般的应用来说，默认长度已经足够胜任了。如果是rsa加密方式，那么最短长度为768 byte

> 注4：authorized_keys文件的权限问题。如果按上述步骤建立关系后，仍然要验证密码，并且没有其他报错，那么需要检查一下authorized_keys文件的权限，需要作下修改： chmod g-w authorized_keys

*******************
## 删除服务器间信任关系的方法

如果想取消两台服务器之间的信任关系，直接删除公钥或私钥是没有用的，需要在Client服务器上，打开 ~/.ssh/ authorized_keys 文件，找到对应的服务器的公钥字段并删除


每个段落的开头是ssh-rsa字样，段尾是Server服务器的帐号和ip（如下图红框），需要细心的找一下后删除整段


