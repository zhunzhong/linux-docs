### 设置创建文件默认权限
在/etc/samba/smb.conf文件中，根据实际需要全局或者指定分组下面增加如下配置，即可设置

create mode = 0766
force create mode = 0766
directory mode = 0777
force directory mode = 0777
