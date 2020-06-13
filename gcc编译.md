> step1 安装bzip2工具

```
yum -y install bzip2 #gcc依赖包需要通过该工具解压
```

> step2 下载相关包

```
wget https://mirrors.tuna.tsinghua.edu.cn/gnu/gcc/gcc-7.2.0/gcc-7.2.0.tar.gz
tar xvzf gcc-7.2.0.tar.gz
cd gcc-7.2.0
./contrib/download_prerequisites #这一步可能要很长很长时间，速度又慢
```

> step3 配置生产makefile

```
mkdir build
cd build
../configure --prefix=/usr/local/gcc-7.2.0 --enable-threads=posix --disable-checking --disable-multilib --enable-languages=c,c++
```

> step4 编译

```
make -j 8 #可根据电脑核数配置该数字，可以并行编译加快编译速度，这步可能也很慢
make install #安装到prefix配置目录下
```

> step5 查看安装是否成功

```
gcc -v  #查看gcc版本
strings /usr/lib64/libstdc++.so.6 | grep GLIBCXX  #查看我们需要的glibc版本可有安装成功
```

