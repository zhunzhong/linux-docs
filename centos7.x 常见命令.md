# centos7.x 常见命令



## 查看机器基本信息

1. 查看CentOS版本：cat /etc/redhat-release
2. 查看CPU型号：cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
3. 查看物理CPU个数：cat /proc/cpuinfo | grep "physical id" | sort | uniq|wc -l
4. 查看CPU逻辑核数：cat /proc/cpuinfo | grep "processor" | wc -l
5. 查看CPU是几核：cat /proc/cpuinfo | grep "cores"|uniq

