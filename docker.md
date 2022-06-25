# 常见命令

```
#查看镜像
docker images

#将镜像保存到本地
docker save <repository>:<tag> -o <repository>.tar

#重新加载镜像
docker load -i rocketmq.tar

#如果docker载入新的镜像后repository和tag名称都为none
#那么通过tag的方法增加名字标签
docker tag <IMAGE ID> <repository>:<tag>

#构建docker镜像(其中的点代表当前路径)
docker build -f Dockerfile . -t <repository>:<tag>

#提交到镜像仓库
docker push <repository>:<tag>

#从镜像仓库拉取指定镜像
docker pull <repository>:<tag>
```

# centos系统docker安装

## 官方安装地址

```
https://docs.docker.com/install/linux/docker-ce/centos/
sudo apt-get install docker-ce docker-ce-cli containerd.io
```



## 离线安装包的地址

```
https://download.docker.com/linux/centos/7/x86_64/stable/Packages/
and download the .rpm file for the Docker version you want to install.
```

## 配置阿里云地址

```
在线安装docker时访问默认官方docker仓库地址会非常的慢，可以将仓库地址修改为阿里云的，
速度会很快,如下：
sudo add-apt-repository \
   "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu/ \
   $(lsb_release -cs) \
   stable"
```

## 安装步骤

```
1) sudo yum install /path/to/package.rpm 安装docker
2) sudo systemctl start docker 启动docker
3) sudo docker run hello-world 启动一个默认的测试docker
This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

systemctl enable docker 将docker-deamon设置为开机启动项

解决非root拥护无法访问docker
sudo groupadd docker     #添加docker用户组
sudo gpasswd -a $USER docker     #将登陆用户加入到docker用户组中
newgrp docker     #更新用户组
docker ps    #测试docker命令是否可以使用sudo正常使用

如果还不行，可以重启docker服务
systemctl restart docker

Uninstall Docker CE 卸载
sudo yum remove docker-ce
sudo rm -rf /var/lib/docker
```



# docker-compose安装

```
官方安装文档地址:https://docs.docker.com/compose/install/
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-linux-x86_64" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version 查看版本

curl -L https://get.daocloud.io/docker/compose/releases/download/1.24.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
也可以通过国内daocloud提供地址下载
```

```


# step 1: 安装必要的一些系统工具

sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# Step 2: 添加软件源信息

sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

# Step 3: 更新并安装 Docker-CE

sudo yum makecache fast
sudo yum -y install docker-ce

# Step 4: 开启Docker服务

sudo service docker start

注意：其他注意事项在下面的注释中



# 官方软件源默认启用了最新的软件，您可以通过编辑软件源的方式获取各个版本的软件包。例如官方并没有将测试版本的软件源置为可用，你可以通过以下方式开启。同理可以开启各种测试版本等。

# vim /etc/yum.repos.d/docker-ce.repo

# 将 [docker-ce-test] 下方的 enabled=0 修改为 enabled=1

#

# 安装指定版本的Docker-CE:

# Step 1: 查找Docker-CE的版本:

# yum list docker-ce.x86_64 --showduplicates | sort -r

# Loading mirror speeds from cached hostfile

# Loaded plugins: branch, fastestmirror, langpacks

# docker-ce.x86_64            17.03.1.ce-1.el7.centos            docker-ce-stable

# docker-ce.x86_64            17.03.1.ce-1.el7.centos            @docker-ce-stable

# docker-ce.x86_64            17.03.0.ce-1.el7.centos            docker-ce-stable

# Available Packages

# Step2 : 安装指定版本的Docker-CE: (VERSION 例如上面的 17.03.0.ce.1-1.el7.centos)

# sudo yum -y install docker-ce-[VERSION]

# 注意：在某些版本之后，docker-ce安装出现了其他依赖包，如果安装失败的话请关注错误信息。例如 docker-ce 17.03 之后，需要先安装 docker-ce-selinux。

# yum list docker-ce-selinux- --showduplicates | sort -r

# sudo yum -y install docker-ce-selinux-[VERSION]

# 通过经典网络、VPC网络内网安装时，用以下命令替换Step 2中的命令

# 经典网络：

# sudo yum-config-manager --add-repo http://mirrors.aliyuncs.com/docker-ce/linux/centos/docker-ce.repo

# VPC网络：

sudo yum-config-manager --add-repo http://mirrors.could.aliyuncs.com/docker-ce/linux/centos/docker-ce.repo



1. 配置镜像加速器
   针对Docker客户端版本大于 1.10.0 的用户

您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://d5lobrf9.mirror.aliyuncs.com"]
}
EOF

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
EOF

"registry-mirrors": [

​```
"https://d5lobrf9.mirror.aliyuncs.com",
"https://registry.docker-cn.com",
"http://hub-mirror.c.163.com",
"https://docker.mirrors.ustc.edu.cn"
​```

  ]

镜像加速相关文档:https://www.cnblogs.com/reasonzzy/p/11127359.html
sudo systemctl daemon-reload
sudo systemctl restart docker

3.安装网桥管理工具
yum install bridge-utils

networks:
   extnetwork:

​```
  external:
    name: dc_network
​```

创建一个网段，对应容器都使用该网段，避免虚拟网段冲突
docker network create --subnet=172.18.0.0/16 --gateway=172.18.0.1 my_network
```


