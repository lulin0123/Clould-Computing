# Linux系统管理

## 主讲:王锦堃

## 一、Linxu系统概述

Linux是一个开源的操作系统**内核**，现在市面上常见的基于Linux内核开发的Linux操作系统有Ubuntu、Red Hat、CentOS等。

+ LInux系统的特点
  + 开源
  + 多用户和多任务
    + Linux支持多用户和多任务，这意味着多个用户可以在同一台计算机上同时运行不同的程序，而且他们之间不会产生干扰
    + 这使得Linux成为了服务器和大型计算机的理想选择
  + 稳定性和可靠性
    + Linux内核非常稳定，能够连续运行数月甚至数年而不需要重新启动
  + 可定制性
    + 用户可以自由的修改其源代码，可以灵活的适用各种场景，满足客户的需求
  + 安全性
  + 多平台支持

## 二、Linux常用命令

### 1、目录结构

```shell
[root@localhost ~]# 
root 当前登陆操作系统的用户名
localhost 当前计算机名称 默认叫做localhost
~ 当前光标所在的文件夹名称 ~代表当前登陆用户的初始地址
# 后面可以编写需要执行的命令
```

+ Linux没有盘符的概念 只有一个目录体系`/`
+ 所有的内容全部全部都是从`/`开始存储的
+ `/`在Linux操作系统中被我们称之为**根目录**

![](./image/10.png)

### 2、目录和文件的操作

+ 查看当前路径

```shell
#展示当前光标所在的目录路径
[root@localhost ~]# pwd
/root
```

+ 展示列表

```shell
#展示当前目录中的文件或者目录（不包括隐藏内容）
[root@localhost ~]# ls
anaconda-ks.cfg
#展示当前目录中所有的文件或者目录（包括隐藏内容）
#.     表示当前目录本身
#..    表示上一级目录（当前目录所在的目录）
[root@localhost ~]# ls -a
.  ..  anaconda-ks.cfg  .bash_logout  .bash_profile  .bashrc  .cshrc  .tcshrc
#作用和-a一致 省略.和..
[root@localhost ~]# ls -A
anaconda-ks.cfg  .bash_logout  .bash_profile  .bashrc  .cshrc  .tcshrc
#展示详情
[root@localhost ~]# ls -l
总用量 4
-rw-------. 1 root root 1241 10月 10 15:54 anaconda-ks.cfg
#展示详情 更具体展示文件的大小 -h 必须和 -l一起使用
[root@localhost ~]# ls -h -l
总用量 4.0K
-rw-------. 1 root root 1.3K 10月 10 15:54 anaconda-ks.cfg
#命令佩戴的指令可以根据需求组合使用
[root@localhost ~]# ls -l -h -a
总用量 24K
dr-xr-x---.  2 root root  114 10月 10 15:54 .
dr-xr-xr-x. 17 root root  224 10月 10 15:52 ..
-rw-------.  1 root root 1.3K 10月 10 15:54 anaconda-ks.cfg
-rw-r--r--.  1 root root   18 12月 29 2013 .bash_logout
-rw-r--r--.  1 root root  176 12月 29 2013 .bash_profile
-rw-r--r--.  1 root root  176 12月 29 2013 .bashrc
-rw-r--r--.  1 root root  100 12月 29 2013 .cshrc
-rw-r--r--.  1 root root  129 12月 29 2013 .tcshrc
[root@localhost ~]# ls -lha
总用量 24K
dr-xr-x---.  2 root root  114 10月 10 15:54 .
dr-xr-xr-x. 17 root root  224 10月 10 15:52 ..
-rw-------.  1 root root 1.3K 10月 10 15:54 anaconda-ks.cfg
-rw-r--r--.  1 root root   18 12月 29 2013 .bash_logout
-rw-r--r--.  1 root root  176 12月 29 2013 .bash_profile
-rw-r--r--.  1 root root  176 12月 29 2013 .bashrc
-rw-r--r--.  1 root root  100 12月 29 2013 .cshrc
-rw-r--r--.  1 root root  129 12月 29 2013 .tcshrc
```

+ 创建目录

```shell
#只能创建单层目录
[root@localhost ~]# mkdir day02
[root@localhost ~]# ls
anaconda-ks.cfg  day02
[root@localhost ~]# mkdir day02/a
[root@localhost ~]# ls
anaconda-ks.cfg  day02
[root@localhost ~]# mkdir day02/a/b/c
mkdir: 无法创建目录"day02/a/b/c": 没有那个文件或目录
#级联创建
[root@localhost ~]# mkdir -p day02/a/b/c
#可以一次创建多个目录 目录名称之间以空格隔开
[root@localhost ~]# mkdir day03 day04 day05
[root@localhost ~]# ls
anaconda-ks.cfg  day02  day03  day04  day05
```

+ 切换目录

```shell
#相对路径 以目录名称开头 或者以./ 都表示从当前位置开始寻找
#绝对路径 以/开头 表示完整路径 从根目录开始寻找
[root@localhost ~]# cd day02
[root@localhost day02]# cd ..
[root@localhost ~]# cd /root
```

+ 创建文件

```shell
[root@localhost ~]# cd day02
[root@localhost day02]# touch a.txt
[root@localhost day02]# ls
a  a.txt
[root@localhost day02]# cd ..
#可以通过指定路径创建文件
[root@localhost ~]# touch /root/day02/a/1.txt
#多个文件之间以空格隔开
[root@localhost ~]# touch 1.txt 2.txt
```

+ 删除目录和文件

```shell
[root@localhost ~]# cd day02
[root@localhost day02]# ls
a  a.txt
#删除文件
[root@localhost day02]# rm a.txt
rm：是否删除普通空文件 "a.txt"？y
[root@localhost day02]# ls
a
[root@localhost day02]# cd ..
[root@localhost ~]# pwd
/root
#-r删除目录
[root@localhost ~]# rm -r day03
rm：是否删除目录 "day03"？y
[root@localhost ~]# ls
anaconda-ks.cfg  day02  day04  day05
#强制删除 不需要手动确认
[root@localhost ~]# rm -r -f day04
[root@localhost ~]# rm -rf day05
[root@localhost ~]# ls
anaconda-ks.cfg  day02
```

+ 移动修改目录和文件

```shell
[root@localhost b]# mv c /root/day02
[root@localhost b]# ls
[root@localhost b]# cd /root/day02/
[root@localhost day02]# ls
a  c
[root@localhost day02]# mv /root/day02/a/b /root/day02
[root@localhost day02]# ls
a  b  c
[root@localhost day02]# cd a
[root@localhost a]# ls
1.txt
[root@localhost a]# mv 1.txt /root/day02
[root@localhost a]# cd ..
[root@localhost day02]# ls
1.txt  a  b  c
[root@localhost day02]# mv 1.txt hello.txt
[root@localhost day02]# ls
a  b  c  hello.txt
```

+ 复制目录和文件

```shell
[root@localhost day02]# cp hello.txt a
[root@localhost day02]# ls
a  b  c  hello.txt
[root@localhost day02]# cd a
[root@localhost a]# ls
hello.txt
#复制目录需要加-r
[root@localhost day02]# cp a b
cp: 略过目录"a"
[root@localhost day02]# cp -r a b
[root@localhost day02]# ls
a  b  c  hello.txt
```

+ 清屏

```shell
[root@localhost b]# clear
```

### 3、查找目录和文件

`find`命令是Linux操作系统中的一个非常强大的查找命令，可以根据目标的名称、类型、大小等不同属性进行查找。

`find [查找范围] [条件表达式]`

+ 查找范围
  + 指定需要从哪一个目录查找指定的文件
+ 条件表达式
  + 决定需要查找符合哪些条件的文件
  + `-name`
    + 按照指定的文件名进行查询
  + `-size`
    + 根据指定的大小进行查询
  + `-type`
    + 根据类型进行查询

```shell
[root@localhost day03]# find /root/day03 -name "*.txt"
/root/day03/2.txt
/root/day03/1.txt
/root/day03/3.txt
[root@localhost day03]# find /root/day03 -size +10
[root@localhost day03]# find /root/day03 -size -10
[root@localhost day03]# find /root/day03 -type f
/root/day03/2.txt
/root/day03/1.txt
/root/day03/3.txt
[root@localhost day03]# find /root/day03 -type d
/root/day03
/root/day03/a
/root/day03/b
#-a 且  -o 或
[root@localhost day03]# find /root/day03 -name "*.txt" -a -size -10 -a -type d
[root@localhost day03]# find /root/day03 -name "*.txt" -a -size -10 -o -type d
/root/day03
/root/day03/2.txt
/root/day03/1.txt
/root/day03/3.txt
/root/day03/a
/root/day03/b
```

## 三、vi 编辑器

### 1、模式切换

相当于windows操作系统中的记事本

`vi 文件名`

+ 命令模式
  + 打开文件后 默认为该模式
  + 光标移动 删除 查找 添加等命令操作
+ 输入模式
  + 输入内容
+ 末行模式
  + 保存文件、退出编辑....

以上3种模式可以进行切换

![](./image/11.png)

### 2、末行模式

+ 保存文件
  + `w`
  + `w 绝对路径` 如果我们直接使用`vi`命令 可以编辑一个不存在的文件 保存时需要指定文件的存放位置以及文件名
+ 退出编辑器
  + `q`
  + `q!`不保存强制退出
  + 在vi编辑器模式下 如果没有正规保存文件 系统出现故障退出了vi编辑器 此时vi编辑器会自动备份文件
  + 出现一个`.文件名.swp`的文件 并且我们编辑原文件时会给出错误提示
  + 如果出现了以上情况我们将`.swp`文件先删除 再继续操作原文件
+ 打开新文件
  + `e 新文件名` vi编辑器会切换到指定的新文件继续进行操作
+ 加入其它文件的内容
  + `r 文件名` 将指定的文件的内容完整的追加到当前文件的内容中
+ 替换文件内容
  + `[指定范围] sub/旧的内容/新的内容/g`
  + 指定范围
    + 默认替换当前光标所在的行中的内容
    + % 全文替换
    + n,m 替换第n行到第m行中的内容

### 3、命令模式

+ 翻页移动
  + ctrl + f 下一页
  + ctrl + b 上一页
+ 行内快速跳转
  + `0`或`^`将光标跳转到行首
  + `$`将光标上跳转到行尾
+ 行间快速跳转
  + `gg`跳转到第1行
  + `G`跳转到最后一行
  + `nG`n是一个指定的数值`1,2,3,4` 表示跳转到第n行
+ 删除
  + `x`删除单个字符
  + `dd`删除光标所在的行
  + `ndd`n是一个指定的数值 表示往下删n行
  + `d^`   将行首到当前光标位置的内容全部删除
  + `d$`  将光标当前位置到行尾的内容全部删除
+ 复制
  + `yy`复制当前行整行的内容
  + `nyy`n是一个指定的数值 表示复制n行
+ 粘贴
  + `p`
  + 删除和复制的操作都会将内容存放到**剪切板**中
  + p就是将剪切板中的内容粘贴到当前位置
+ 撤销上一步操作
  + `u`
+ 保存并退出
  + `ZZ`
+ 查找内容
  + `/查找的内容`
  + 在查询结果中 按n键可以查看下一个目标

## 四、Linux文件管理

### 1、Linux系统结构

Linux操作系统中的目录和文件被组成了一个**树形目录结构**，所有的分区、文件等都具有一个相同的起始位置（**根目录**）

+ boot
  + 此目录是系统内核存放的目录
+ bin
  + 这一目录存放了所有用户都可以执行的命令
+ sbin
  + 存放了管理命令，这些命令一般是只有管理员才可以使用
+ home
  + 所有普通用户的默认工作目录
  + 每有一个用户账号就会在该目录中分配一个独立的操作空间
+ root
  + root账号的操作目录
+ etc
  + 主要存放系统的配置文件

### 2、查看以及检索文件

+ 查看文件
  + `cat 文件名` 全文展示
  + `more` 分页展示
    + 回车 下拉
    + 空格 下一页
    + b 上一页
    + q 退出查看
  + `head` 
    + 查看文件的头部信息 默认展示前10行
    + `-n` 指定展示前几行
  + `tail` 
    + 查看文件的尾部信息

### 3、控制台输出

```shell
#将原本需要输出到控制台中的内容重定向到指定的文件中
echo 111 >> 6.txt
```

### 4、统计和检索文件内容

+ `wc`
  + `Word Count`

```shell
[root@localhost day03]# wc 1.txt
  89  110 1547 1.txt
[root@localhost day03]# wc -l 1.txt
89 1.txt
[root@localhost day03]# wc -w 1.txt
110 1.txt
[root@localhost day03]# wc -c 1.txt
1547 1.txt
```

### 5、压缩文件

+ 在linux中压缩格式`tar.gz`
+ `tar`
  + `z` 使用gzip压缩工具 必加
  + `x`  解压
  + `c` 压缩
  + `v` 显示详细信息
  + `f` 表示使用归档文件 必加

```shell
[root@localhost ~]# tar -zcvf day03.tar.gz day03
day03/
day03/3.txt
day03/a/
day03/b/
day03/4.txt
day03/2.txt
day03/.1.txt.swp
day03/1.txt
day03/6.txt
[root@localhost ~]# ls
anaconda-ks.cfg  day02  day03  day03.tar.gz

[root@localhost ~]# tar -zxvf day03.tar.gz
```

## 五、账号和权限管理

### 1、用户账号和组账号

#### 1.1、用户账号

在Linux操作系统中，根据系统管理的需要将用户分为不同的类型，主要包括**超级用户**、**普通用户**、**程序用户**，各角色拥有的权限和担任的角色各不相同。

+ 超级用户

  root用户是Linux操作系统中默认的超级用户账号，对操作系统拥有最高的权限，只有当进行系统维护、管理任务时我们才建议使用root账号登陆系统。日常任务处理建议使用普通用户

+ 普通用户

  通过root账号创建的普通账号。拥有的权限受到了一定的限制，一般用户只有在自己的**宿主目录**中拥有完整的权限

+ 程序用户

  这类用户一般不参与系统的维护，是在我们安装一些软件时自动创建的用户账号 该类账号往往只负责运行程序不负责该程序以外的内容

#### 1.2、组账号

基于某种特定联系（有些用户都要操作访问同一个服务）将多个用户集合在一起，即构成一个**用户组**，表示该组内所有用户的账号称为**组账号**，

**每一个用户至少属于一个组**，这个组被称为该用户的**基本组（私有组）**，该用户还可以存在于其它组中，这些组被称为**附加组（公有组）**

张三   技术组   基本组

​           测试组   附加组

我们在创建用户账号时可以指定该账号的基本组 如果不指定 创建用户账号的同时 会创建一个同名的组账号

user   user  基本组

u1      user  基本组

u2      u2     基本组

​           user 附加组

**对组账号设置的权限适用于组内的每一个用户账号**

#### 1.3、UID和GID

Linux操作系统中的每一个用户账号都有一个数字形式的身份标记，称为UID

root账号UID固定为0，程序用户的UID默认为1-499，普通用户500-60000

和UID一样每一个组账号都有一个GID

### 2、用户账号管理

#### 2.1、用户账号文件

Linux操作系统中账号相关的配置文件主要有两个，分别是passwd和shadow。

前者用于保存用户名称、宿主目录、登陆Shell等基本信息

后者用于保存用户的密码、账号等有效信息

每一行对应一个用户账号，不同的配置项之间以`:`隔开

+ passwd
  + 用户账号的名称
  + 经过加密的用户密码字符串或者使用密码占位符`x`
  + 用户账号的UID
  + 所属账号的GID
  + 用户全名，可填写与用户相关的说明信息
  + 宿主目录
  + 登陆Shell的信息 用户完成登陆后可以使用的Shell

```shell
[root@localhost ~]# head -5 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

+ shadow
  + 账号名
  + 密码的加密字符串
  + 上一次修改密码的天数
  + 密码最短有效天数
  + 密码最长有效天数
  + 提前多少天告诉用户密码将过期
  + ......

```shell
[root@localhost ~]# head -2 /etc/shadow
root:$6$uuL0jJsIfOjeNmcP$P8MoAURwg7AxXQJSmjsCfyv/FhzYWslfGV5xJyO1pIH.HK4RyOYxB3oAU2MaXnyBuJ395yBGsDdmZqQC2LKGn/::0:99999:7:::
bin:*:18353:0:99999:7:::
```

#### 2.2、用户账号的操作

+ 添加
  + `useradd [参数] 用户名`
  + -u 指定UID
  + -d 指定宿主目录 如果没有指定宿主目录 那么默认创建一个和用户名相同的宿主目录
  + -e 指定用户账号的失效时间 可以使用`yyyy-MM-dd`的日期格式指定
  + -g 指定用户的基本组 如果没有指定用户所属的组账号，则会自动创建一个同名的组账号
  + -G 指定用户的附加组
  + -M 不建立宿主目录
  + -s 指定用户的登陆shell
+ 设置密码
  + 在`root`用户下`passwd 用户名`设置指定用户的密码
  + 如果是普通用户可以直接使用`passwd`修改自己的密码
  + `-d`清空密码 可以使用用户名直接登陆
  + `-l`锁定用户账号 禁止登陆
  + `-u`解锁用户账号
  + `-S`查看用户账号的状态
+ 删除
  + `userdel 用户名`只删除账号不删除宿主目录
  + `-r`宿主目录一起删除
+ 修改
  + `usermod`
  + `-l`更改账号名称
  + `-L`锁定用户账号
  + `-U`解锁用户账号
  + 其余参数和`useradd`的参数一致

#### 2.3、用户账号的初始配置文件

添加一个新的用户账号后，系统会在该账号的宿主目录下生成一些初始配置文件

+ `.bash_history`
  + 记录当前账号的历史执行命令
+ `.bash_logout`
  + 文件中定义的命令会在用户退出登陆时执行
+ `.bash_profile`
  + 文件中定义的命令会在用户每次登陆时执行
+ `.bashrc`
  + 该文件中的命令会在每次加载`/bin/bash`程序时执行

### 3、组账号管理

#### 3.1、组账号文件

+ `group`
  + `fft:x:1000:f1,f2`
  + 组名
  + 密码占位符
  + GID
  + 当前组的附加用户
+ `gshadow`
  + 因为组账号一般不设置密码 所以该文件存储的数据有限

#### 3.2、组账号的操作

+ 添加
  + `groupadd 组名`
  + `-g`指定GID值
+ 删除
  + `groupdel`
  + 如果删除的组作为私有组被某个账号使用 那么改组无法删除（只能删除附加组）
+ 修改
  + 添加、删除组成员
  + `gpasswd -a/-d 用户账号名 组名`
+ 查询
  + `groups`
  + 展示当前登陆的账号所属的组

### 4、管理文件和目录的属性

#### 4.1、查看文件和目录的属性

+ `ls -l`
  + 展示当前目录中所有文件或者目录的详细信息
  + 如果指定某一个文件 则显示文件的详情
  + 如果指定某一个目录 则显示指定目录中所有文件或者目录的详情
  + `ls -ld 目录名`则显示目录本身的详情
  + 展示的详情以空格隔开
    + 第3个字段和第4个字段展示当前文件或者目录的**属主**和**属组**
    + 第1个字段展示的是该文件的访问权限，由4个部分组成`drwxr-xr-x.`
      + 第1个字符 表示文件类型d（目录），b（块设备文件），c（字符设备文件），-（普通文件），l（链接文件）
      + 第2-4个字符 表示该文件的属主用户对该文件的访问权限r（读），w（写），x（执行），-（没有）
      + 第5-7个字符 表示该文件的属组内各成员用户对该文件的访问权限
      + 第8-10个字符 表示其他用户对该文件的访问权限

#### 4.2、设置文件和目录的权限

+ `chmod [ugoa][+-=][rwx] 文件或目录`
  + `u` 文件属主的权限
  + `g`  文件属组的权限
  + `o`  其它用户的权限
  + `a`  以上三种类别的用户一起设置权限
  + `+` 添加权限
  + `-` 移除权限
  + `=` 设置对应的权限
  + `r` 读
  + `w`写
  + `x`执行

```shell
[f@localhost ~]$ ls -ld mytest.txt 
-rw-r--r--. 1 f fft 0 10月 15 14:18 mytest.txt
[f@localhost ~]$ chmod u-w mytest.txt 
[f@localhost ~]$ ls -ld mytest.txt 
-r--r--r--. 1 f fft 0 10月 15 14:18 mytest.txt
[f@localhost ~]$ echo 111 >> mytest.txt 
-bash: mytest.txt: 权限不够
[f@localhost ~]$ chmod u+w mytest.txt 
[f@localhost ~]$ ls -ld mytest.txt 
-rw-r--r--. 1 f fft 0 10月 15 14:18 mytest.txt
[f@localhost ~]$ echo 111 >> mytest.txt 
[f@localhost ~]$ cat mytest.txt 
111
```

#### 4.3、设置文件和目录的归属

+ 默认谁创建的文件和目录归属就是谁
+ `chown 属主:属组 文件或目录`
  + `chown fft:fft a`设置属主和属组
  + `chown fft a`设置属主
  + `chown :fft a`设置属组
  + 以上方式如果设置的是一个目录 那么只对目录本身生效
  + `chown -R`递归修改归属

## 六、软件安装和下载

+ 常见两种下载模式
  + `yum安装源下载`
  + `链接下载`

### 1、yun安装源下载

yum是CentOS7操作系统内置的下载工具 只需要指定需要安装的软件包名称 即可自动下载并安装

CentOS7目前已经停止了更新，自带的下载源已经关闭了，我们需要修改yum的下载源地址

+ 修改镜像源

```shell
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

+ 使用yum下载常用的软件包

```shell
yum -y install vim lrzsz wget
```

### 2、下载安装JDK

+ 下载JDK的压缩包
  + 将准备好的压缩包拖拽到虚拟机中的`/opt`中


+ 移动压缩包并且解压缩

```shell
cd /opt
tar -zxf openjdk-17_linux-x64_bin.tar.gz
```

+ 配置环境变量

```shell
vim /etc/profile

export JAVA_HOME=/opt/jdk
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

source /etc/profile
javac
```

### 3、下载安装Tomcat

+ 下载Tomcat

```shell
wget https://mirrors.huaweicloud.com/apache/tomcat/tomcat-10/v10.0.13/bin/apache-tomcat-10.0.13.tar.gz
```

+ 移动并且解压缩

```shell
[root@localhost opt]# tar -zxf apache-tomcat-10.0.13.tar.gz 
[root@localhost opt]# ls
apache-tomcat-10.0.13  apache-tomcat-10.0.13.tar.gz  jdk-17
[root@localhost opt]# rm -rf apache-tomcat-10.0.13.tar.gz 
[root@localhost opt]# mv apache-tomcat-10.0.13/ tomcat
[root@localhost opt]# ls
jdk-17  tomcat
```

+ 在tomcat中配置网站访问服务

```shell
[root@localhost opt]# cd tomcat/webapps/
[root@localhost webapps]# mkdir y23
[root@localhost webapps]# touch hello.html
[root@localhost webapps]# vim hello.html

<h1 style='color:skyblue'>大家好 我叫xxx</h1>

[root@localhost webapps]# mv hello.html y23
[root@localhost webapps]# systemctl stop firewalld
```

+ 启动tomcat服务

```shell
[root@localhost y23]# cd /opt/tomcat/bin/
[root@localhost bin]# ls
bootstrap.jar                 configtest.sh     startup.sh
catalina.bat                  daemon.sh         tomcat-juli.jar
catalina.sh                   digest.bat        tomcat-native.tar.gz
catalina-tasks.xml            digest.sh         tool-wrapper.bat
ciphers.bat                   setclasspath.bat  tool-wrapper.sh
ciphers.sh                    setclasspath.sh   version.bat
commons-daemon.jar            shutdown.bat      version.sh
commons-daemon-native.tar.gz  shutdown.sh
configtest.bat                startup.bat
[root@localhost bin]# ./startup.sh
```

![](./image/12.png)

