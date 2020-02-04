# C Standard library

C语言的库函数进行归纳整理

### Linux 下的 C 函数库

- libc

  Linux 下的 ANSI C 函数库

- **glibc （The GNU C Library ）**

  Linux 下的 GUN C 函数库 

  link1：<https://www.gnu.org/software/libc/libc.html>

  link2：<http://www.gnu.org/software/libc/manual/>    文档

glibc是linux下面c标准库的实现，即GNU C Library。glibc本身是GNU旗下的C标准库，后来逐渐成为了Linux的标准c库，而Linux下原来的标准c库Linux libc逐渐不再被维护。Linux下面的标准c库不仅有这一个，如uclibc（https://www.uclibc.org/）、klibc，以及上面被提到的Linux libc，但是glibc无疑是用得最多的。glibc在/lib目录下的.so文件为libc.so.6。
glibc是gnu发布的libc库，也即c运行库。glibc是linux 系统中最底层的api（应用程序开发接口），几乎其它任何的运行库都会倚赖于glibc。glibc除了封装linux操作系统所提供的系统服务外，它本 身也提供了许多其它一些必要功能服务的实现，主要的如下：
（1）string，字符串处理
（2）signal，信号处理
（3）dlfcn，管理共享库的动态加载
（4）direct，文件目录操作
（5）elf，共享库的动态加载器，也即interpreter
（6）iconv，不同字符集的编码转换
（7）inet，socket接口的实现
（8）intl，国际化，也即gettext的实现
（9）io
（10）linuxthreads
（11）locale，本地化
（12）login，虚拟终端设备的管理，及系统的安全访问
（13）malloc，动态内存的分配与管理
（14）nis
（15）stdlib，其它基本功能

```shell
#安装
wget http://ftp.gnu.org/gnu/glibc/glibc-2.19.tar.gz
tar -zxf glibc-2.19.tar.gz
mkdir glibc-build
cd glibc-build
../glibc-2.19/configure --prefix=/usr/lib64/glibc-2.19
make
make install

#版本查看   ldd命令由glibc提供
ldd  --version
```

