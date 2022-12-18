# centos7.x 常见命令



## 查看机器基本信息

1. 查看CentOS版本：cat /etc/redhat-release
2. 查看CPU型号：cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
3. 查看物理CPU个数：cat /proc/cpuinfo | grep "physical id" | sort | uniq|wc -l
4. 查看CPU逻辑核数：cat /proc/cpuinfo | grep "processor" | wc -l
5. 查看CPU是几核：cat /proc/cpuinfo | grep "cores"|uniq




## 设置防火墙

1. 查看已开放的端口(默认不开放任何端口)

   ```
   firewall-cmd --list-ports
   ```

2. 开启80端口 

   ```
   firewall-cmd --zone=public(作用域) --add-port=80/tcp(端口和访问类型) --permanent(永久生效)
   ```

3. 重启防火墙 

   ```
   firewall-cmd --reload
   ```

4. 停止防火墙 

   ```
   systemctl stop firewalld.service
   ```

5. 禁止防火墙开机启动 

   ```
   systemctl disable firewalld.service
   ```

6. 删除指定端口

   ```
   firewall-cmd --zone=public(作用域) --remove-port=80/tcp(端口和访问类型) --permanent(永久生效)
   ```

## 服务器时间设置

1.查看时区
```
timedatectl
```

2.设置时区
```
timedatectl set-timezone Asia/Shanghai 
```

## 配置服务器静态ip
1.配置BOOTPROTO
```
BOOTPROTO=static #dhcp:自动分配ip，static：静态ip 
```
2.ONBOOT
```
ONBOOT=yes #开启启动必须是yes
```
3.设置IP和掩码等
```
IPADDR=192.168.254.100  #ip地址
NETWORK=255.255.255.0  #子网掩码
GATEWAY=192.168.254.1 #网关
DNS1=192.168.0.1  #域名服务器1
DNS2=8.8.8.8  #域名服务器2
```
4.重启网卡
```
systemctl restart network
```


## 配置服务器hostname
hostnamectl set-hostname centos1