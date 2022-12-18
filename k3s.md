

INSTALL_K3S_SKIP_DOWNLOAD=true INSTALL_K3S_EXEC='server' K3S_DATASTORE_ENDPOINT='http://192.168.254.128:2379/' ./install.sh


# 查看子命令帮助信息
kubectl get --help

# 列出默认namespace中的所有pod
kubectl get pods

# 列出指定namespace中的所有pod
kubectl get pods --namespace=test

# 列出所有namespace中的所有pod
kubectl get pods --all-namespaces

# 列出所有pod并显示详细信息
kubectl get pods -o wide


kubectl proxy --address='0.0.0.0'  --accept-hosts='^*$'


sudo k3s kubectl delete ns kubernetes-dashboard
sudo k3s kubectl delete clusterrolebinding kubernetes-dashboard
sudo k3s kubectl delete clusterrole kubernetes-dashboard


kubectl create -f recommended.yaml
k3s kubectl create -f dashboard.admin-user.yml -f dashboard.admin-user-role.yml
sudo k3s kubectl -n kubernetes-dashboard create token admin-user
sudo k3s kubectl proxy
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/


获取server的token
cat /var/lib/rancher/k3s/server/node-token

/usr/local/bin/k3s

# k3s master节点安装

## 设置hostname
```
hostnamectl set-hostname master01
```

## k3s拷贝到指定位置
```
/usr/local/bin
```

## 安装k3s
```

NSTALL_K3S_SKIP_DOWNLOAD=true INSTALL_K3S_EXEC='server' K3S_DATASTORE_ENDPOINT='http://192.168.254.128:2379/'  ./install.sh
```

## master服务状态查询
```
systemctl status k3s
```
## master端k3s的启停
```
systemctl status k3s
systemctl restart k3s

系统服务配置文件路径：/etc/systemd/system/multi-user.target.wants

```


# k3s worker节点安装

## 设置hostname
```
hostnamectl set-hostname work01
```

## k3s拷贝到指定位置
```
/usr/local/bin
```

## 获取master节点token
```
cat /var/lib/rancher/k3s/server/node-token
```

## 安装k3s
```
NSTALL_K3S_SKIP_DOWNLOAD=true K3S_URL=https://192.168.254.128:6443  K3S_TOKEN=K10b4651ee6999e929ae03cb5e034db014ca72dff3f645a753c162b4fd055830455::server:6457f26e8e535e74905fc84e9689aed4 ./install.sh
```

## 开启kubectl集群访问
```
将 /etc/rancher/k3s/k3s.yaml 复制到位于集群外部的主机上的 ~/.kube/config。然后，将 server 字段的值替换为你 K3s Server 的 IP 或名称。现在，你可以使用 kubectl 来管理 K3s 集群。

注意:config是文件不是文件夹
```
## worker节点 加入集群
```
kubectl label node work01 node-role.kubernetes.io/worker=worker
```
## worker节点k3s服务启停
```
systemctl status k3s-agent
systemctl restart k3s-agent
系统服务的配置文件路径:/etc/systemd/system/multi-user.target.wants
```

# kubectl命令
## 集群节点操作
kubectl get node
kubectl delete node centos1

