# C Standard library

C语言的库函数进行归纳整理

### Linux 下的 C 函数库

- libc

  Linux 下的 ANSI C 函数库
- newlib

  newlib是一个面向嵌入式系统的c运行库。https://github.com/riscv/riscv-newlib
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





# 函数库的提供形式

#### 静态链接库

* 创建

1. 将 .c源码只编译不链接形成 .o的目标文件

2. 使用ar根据将.o文件归档成.a的归档文件

   > .a文件：  归档文件、静态链接库文件

3. 商业公司发布 .a库文件和 .h头文件来提供静态库给客户使用

   > 商业公司：不发布 .c源码

* 使用（-static）
  1. 调用
  2. 链接器 去.a 文件中拿出被调函数的.o 二进制代码段 进行链接

#### 动态链接库

* 创建

  **-**shared

  -fPIC：位置无关码，加载到内存的位置不加限制

  > .so 文件  .dll文件：动态链接库文件

* 使用（默认）

  运行时自动加载到内存中来

  **-L参数跟着的是库文件所在的目录名**

  **-l**参数就是用来**指定程序要链接的库**

  > **放在/lib和/usr/lib和/usr/local/lib里的库直接用-l参数就能链接了**，但如果库文件没放在这三个目录里，而是放在其他目录里，这时我们只用**-l**参数的话，链接还是会出错，出错信息大概是：“/usr/bin/ld: cannot find **-**lxxx”，也就是链接程序ld在那3个目录里找不到libxxx.so，这时**另外一个参数-L就派上用场了**，比如常用的X11的库，它放在/usr/X11R6/lib目录下，我们编译时就要用**-L** /usr/X11R6/lib **-**lX11参数，**-L参数跟着的是库文件所在的目录名**。再比如我们把libtest.so放在/aaa/bbb/ccc目录下，那链接参数就是**-L**/aaa/bbb/ccc **-**ltest

  固定加载目录：/usr/lib（再找这个）

  指定加载目录： 使用环境变量LD_LIBRARY_PATH (先找这个)

* ldd

  查看链接库，库能不能动态加载
