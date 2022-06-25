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