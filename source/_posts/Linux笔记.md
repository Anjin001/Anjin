---
title: Linux期末
date: 2025-6-9 14:00
mathjex: true
---
# Linux笔记

获取系统版本的命令：？

- Term(终端) 快速启动快捷键  Ctrl+Alt+T

- 关闭终端 Ctrl+D

- 命令补齐 Tab

- 终端清屏 Ctrl+L

  ß4.光标移动所在行首：Ctrl+A

  ß5.光标移动所在行尾：Ctrl+E

  ß6.命令行的删除：Ctrl+U

  ß7.快捷键6的反面：Ctrl+Y

  ß8.不同应用之间的切换：Alt+Tab

软件源存在：source.list

source shell脚本名

## Vim常用命令

ß移动光标：gg第一行，G最后一行，XG第X行；

ß删除一行：dd     删除单词：dw

ß复制一行：yy

ß粘贴一行：p



## Linux的重要概念

 自由、 开放、 免费  多任务和多用户  遵守POSIX标准  类Unix操作系统  

Linux就是在**Minix**的基础上开发和设计的。

Redhat——商业化最成功

Debian——纯志愿者，最纯正自由软件

Ubuntu——基于Debian为开发蓝本

红旗Linux



## Linux的优点

**⚫  （1）基于Unix设计，性能出色**
**⚫  （2）遵循GPL许可，自由软件**
**⚫  （3）符合POSIX标准，兼容性好**
⚫  （4）可移植性好
⚫  （5）网络功能强大
⚫  （6）设备独立性
**⚫  （7）安全性强**
⚫  （8）良好的用户界面



内核版本号由三个部分的数字组成，即**“主版本号+次版本号+修订序列号”**  



pwd:打印当前目录路径

date:查看日期    `+%M`分钟   `+%H`小时 `+%S`秒 `+%Y`年 `+%m`月份 `+%d`日 `+%A`星期 

gedit 文本编译器

sudo apt-get install xx:安装

​						remove xx:卸载软件 但不卸载配置文件

​						purge xx:卸载软件+配置文件

- `sudo apt-get update` 更新软件包索引信息。
- `sudo apt-get upgrade` 根据最新的索引信息升级已安装的软件包

显示命令提示符，普通用户默认的提示符是**“$”**，root用户默认的提示符是**“#”**。



## ls 列出当前目录下的所有内容

- ls -a: 显示目录中包括隐藏文件的全部文件

- ls -l: 显示文件详细信息

- drwxr-xr-x”的含义——这一部分共有10个字符组成。

  第一个字符4种情况：“-”普通文件，“d”目录，“l”链接文件，“b”设备文件。

  后面的9个字符每3个字符为一组，分别代表文件所有者、文件所有者所在用户组、其它用户对文件拥有的权限。

  读（r）、写（w）、执行（x）  

## cd 转换目录

- .  当前目录
- .. 上一级目录
- /   根目录
- ~   当前用户目录

## pwd 显示当前工作目录的绝对路径  

## mkdir 创建新目录

## rmdir 删除空目录  

- 只能删空目录
- rmdir -p 递归删除各级空目录

## touch 创建新文件

## cat 显示某文件的内容

- cat -n 对文件中所有的行进行编号并显示行号
- cat > 文件名    创建文件

## 重定向符与管道符  

| 符号  | 格式            | 含义               |
| ----- | --------------- | ------------------ |
| <     | 命令 < 文件     | 标准输入重定向     |
| **>** | **命令 > 文件** | **标准输出重定向** |
| **>>** | **命令 >> 文件** | **标准输出追加重定向** |
| **\|** | **命令 \| 命令** | **管道** |
## CP 文件拷贝

- cp [选项] <源文件> <目标>  
- cp命令格式中的目标可以是目标路径  

## rm 删除指定文件

- -r, -R, --recursive 递归删除目录及其内容
- -f, --force 强制删除。忽略不存在的文件，不提示确认

## mv 剪切复制

- mv  文件名 路径名

## chmod 修改文件权限和属性

- chmod [mode] 文件名  

- ”u“文件主  ”g“文件组所在组群用户  ”o”其他用户   “a”所有用户
- “+”——代表增加权限   “-”——代表删除权限
  “=”——代表赋予给定的权限，并取消其它权限（如果有的话）
  1. a-rwx   为所有用户取消读、写、执行的权限
  2. ug+r   为所有者和组群用户增加读权限
  3. g=rx   只允许组群用户读、执行。并删除其写的权限
- 权限缩写 “4”代表读 “2”代表写 “1”代表执行

## grep 查找某个特定字符串

- grep  [选项（-i 不区分大小写）  (-E 使用正则表达式)]  关键字 文件名

## head tail 查看文件开头或结尾

- head  [数字选项( -n 指定行数)]  文件名

- 默认10行

## wc 统计文件行数、单词数、字符数

- -l 显示行数   -w   显示单词数   -m 显示字符数  

## find 查找文件

-   find  文件名（或目录名）
- 无参数 则查找并显示在当前目录下所有子目录与文件

## which 查找某命令绝对路径

- 按**PATH变量**所规定的路径进行查找相应的命令，显示该命令的绝对路径。 

## whereis   能查询出命令和Ubuntu资料库里记载的文件

- 与which不同的是， whereis不但能找到可执行的命令，而且将所有包含文件名字符串的文件全部查找出来，而且
  速度很快。  

## locate 将所有与被查询的文件名相同（部分匹配就行）的文件查找出来

## 压缩

- bzip2--.bz2    **gzip--.gz**      **gzip -d解压.gz**    **unzip解压.zip**   zcat查看.gz   bzcar查看.bz2  

## tar 打包解包

-c 打包  -t 查看  -x抽取

- tar [-选项] [备份包的文件名] [要打包（或要解包）的文件或目录]  
- 只是对文件进行打包，并不进行压缩  
- `tar –cf filename.tar file1 file2 file3`  打包成.tar新文件 文件名filename.tar
- `tar –tf filename.tar.gz file1 file2 file3`  查看filename.tar打包文件里的内容  
- `tar –xf filename.tar ` 抽取filename.tar打包文件里的内容，filename.tar文件保持不变，不会消失。 
- `tar –zcf filename.tar.gz file1 file2 file3  ` 把file1、 file2、 file3打包成后缀为.tar的新文件，文件名为filename.tar  
- `tar –zxf filename.tar.gz  ` 抽取filename.tar打包文件里的内容，filename.tar文件保持不变，不会消失  

## mount 挂载  umount卸载

## df 硬盘分区信息   du当前目录下所有文件及目录的信息  

- -h 以Gb或Mb等显示文件大小   -s 只列出各文件大小总和
  1. fsck 硬盘检查


1. shutdown 安全关机
2. halt 强制关机
3. reboot 重启
4. init 切换运行级别  0关机   6重启  [0,6]
5. cal 日历
6. more less 分屏显 示
7. sudo useradd -m 用户名    加一个新用户
8. chown 用户名 文件      改变文件所属用户

 

## linux目录结构

- **符号链接**（软连接）----指向另一个文件   `ln –s  目标（原文件或目录） 链接文件`

- **硬链接**----拷贝源文件   `ln  目标（原文件） 链接文件`

- **绝对路径**：从根目录到达目标目录 第一个**"/"表示根目录**，其余''/"用于分割的作用

- 目录树的起始点为**根目录**



## 网络

- 域名必须对应一个ip地址，ip地址不一定只对应一个域名

- DHCP——局域网网络协议，自动分配ip地址

- `ifconfig` ——查看配置网卡ip，掩码等，不包括DNS

  例如：`sudo ifconfig eth0 192.168.0.1  `

- `ping` [选项] 主机名或IP地址  

  -c5  5次后自动停止

- `ssh` 安全协议

  安装  `sudo apt-get install openssh-server`

  是否安装 `dpkg -l | grep ssh`

  启动 `sudo service ssh start` 

  是否启动 `ps -e | grep ssh`

  登录 `ssh username@ip`

- `netstat`检测连接情况     `bye`退出ftp服务器     `route`对路由表操作     `traceroute` 路由跟踪     `telnet 与 logout `远程登录与取消   `rlogin` 远程登录    `finger`登录账号信息

- `wget` 简易文件下载   `curl`有库支持 协议包括(SMTP、POP3)

- **FFmpeg** 是一个强大的开源多媒体框架，可用于录制、转换和流式传输数字音频和视频以及各种格式。

## 网络服务器

### SimpleHTTPServe

1. 进入待分享的目录

2. 执行命令

   python3: `python3 -m http.server 端口号`

   python2: `python -m SimpleHttpServer 端口号`

   不填默认8000

3. 浏览器 `http://IP:端口号/`

**SMB**协议 主要目的是为了和Windows进行 **文件和打印共享**

- Samba是SMB一种实现

Apache——最广泛Web服务器

## Shell编程

本章了介绍Shell的基础知识，包括Shell
中的通配符、正则表达式、特殊字符等；
以及常用字符串处理工具，包括grep，
sed和awk。 Shell中的变量设置，包括定
义变量、给变量赋值以及读取变量的值，
也介绍了命令别名和命令历史的用法。  

- Ubuntu默认的Shell是bash

- 初始化配置文件 `~/.bashrc`

- shell脚本一般以.sh结尾

- **每次执行都要加chmod 755 file or chmod a+x file**

- `#! /bin/bash`

- 执行脚本 `./脚本名`  or `bash 脚本名` or `source 脚本名`

- 输入 `read -p "input" name`

  

  ## 判断

- `test file` 检测文件类型属性比较  `-d` 是否为目录 `-e` 是否存在 `-f` 是否为文件 `-w（r,x）`是否文件可写（可读，可执行）  `-s`文件名长度大于0 

- `-eq`：等于 
- `-ne`：不等于
- `-lt`：小于
-   `-le`：小于或等于    
- `-gt`：大于 
- `-ge`：大于或等于
- `=` 相等 
-   `-n` 非空
-   `!=` 不相等
- `-e`：文件存在
- `-f`：普通文件存在且是一个普通文件
- `-d`：目录存在
- `-r`：文件可读
- `-w`：文件可写
- `-x`：文件可执行
- `-n`：字符串非空
- `=`:两字符串是否相等
- `-a -o !`



```bash
for i in *.jpeg;
do
    ...
done

if [];
then
	...
else
	...
fi

If..else..if结构
格式：
if [条件1]; then
   命令列表1
elif [条件2]; then
   命令列表2
else
   命令列表3
fi

#!/bin/bash
read –p “input your score:” score
if [ $score –lt 60 ] ; then
   echo “not pass”
elif [ $score –ge 60 –a $scrore –le 70 ] ; then
    echo “pass –D”
elif [ $score –ge 71 –a $scrore –le 80 ] ; then
    echo “pass –C”
elif [ $score –ge 81 –a $scrore –le 90 ] ; then
    echo “pass –B”
elif [ $score –ge 91 –a $scrore –le 100 ] ; then
    echo “pass –A”
fi


利用while循环求和；
#！/bin/bash
sum=0
i=0
while(($i<=100))
do
     sum=$(($sum+$i))
     i=$(($i+1))
done
echo “the result is $sum”

利用for循环求和；
#！/bin/bash
sum=0
for((i=1; i<=100; i++))
do
     sum=$(($sum+$i))
done
echo “the result is $sum”

Case语句结构：
case 变量值 in 
   模式1)
   命令列表1；
    模式2）
    命令列表2；
…
Esac

hour = `date +%H`
case $hour in 
   08|09|10|11|12) echo “good morning”;
   13|14|15|16|17）echo “good afternoon”;
    18|19|20|21) echo “good evening”;
     *) echo “hello”;
esac


```



## 字符串处理

### 通配符

用在文件名那

- `*` 匹配任何字符串，包括空串

- `？` 匹配单个字符

- `[]`匹配其中某个字符,如`[ab]`意为匹配a或b

  注意：除了“-”和之“!”外，其他特殊字符在[]中都是普通字符，包括*和？

- `!` 排除字符，如`[!ef]`表示不为e或f的字符

  ß 列出”/etc”目录下所有扩展名为conf的配置文件：

  Þ ls /etc/*.conf 

  Þ 如果要包含文件”.conf”，则采用 ls –l /etc/{*.,.}conf

  ß 列出”/etc”目录下由3个字母作为文件名的配置文件：

  Þ ls /etc/???.conf

  ß 列出”/etc”目录下所有以a,b,c字母开头的配置文件：

  Þ ls /etc/[a-c]\*.conf 或者 ls /etc/[!d-z]\*.conf

  ß **如果要同时删除a.txt和.txt文件，则 rm –f ./{*., .}txt**

### 正则表达式

- **通配符的组合**构成正则表达式

- `^` 不为当前单词

- ß如何表示英文字母？

  Þ 正则表达式：[a-zA-Z]

  ß案例4：匹配生日格式“June 26, 1951”，对应的正则表达式：[A-Za-z]+\s+[0-9]{1,2},\s+[0-9]{4}
  
  

```c++
### sed命令

- 专门处理文字流的工具，强项在于结合正则表达式后的文本替换功能
- `sed ‘s/pattern/replace_string/’ filename`
- `sed ‘s/this/This/’ a.txt`  替换a.txt中的每个this成This
- `sed ‘/^$/d’ a.txt`  删除空行

### awk高级文本处理

- `awk ‘BEGIN{commands} pattern{commands} END{ commands}’ file`

- 1. 执行BEGIN{ commands }中的语句；

  2. 从文件或者stdin中读取一行，然后执行pattern{ commands }。重复这个过程，直到文件全部被读取完毕。

  3. 当读至输入流末尾时，执行END{ command }语句块

- 对值进行累加。

  `seq 5 | awk ‘BEGIN{ sum=0; print “Sum:” }{sum+=$1} END{ print sum}’`

- 如果要使用awk统计a.txt文件的行数。

  `awk ‘BEGIN{i=0} {i++} END{ print i}’ b.txt`

echo what is windows? This is linux. What you like? | sed 's/ [^.]*linux[^.]*\.//'a.txt
```

  

  

### 命令控制符

- `;` 顺序执行 如 `cal;date`
- `&&` 逻辑与 前面返回true才执行 
- `||`逻辑或 前面返回false才执行
- `&` 把该命令放后台执行 `vim&`
- `""`字符串  除$、 \、单引号和双引号仍作为特殊字符  
- `''`全视为普通字符串
- ”``“ 命令行

### 元字符

- `#` 注释符
- `$` 变量引用符
- ` (Space)` 分隔符
- `\` 转义字符
- 赋值 `var = $abc`  ，若如`var = \$abc`  则`var = "$abc"`





## crontab

```c++
* * * * * command_to_be_executed
- - - - -
| | | | |
| | | | +----- 星期几 (0 - 7) (Sunday is both 0 and 7)
| | | +------- 月份 (1 - 12)
| | +--------- 日期 (1 - 31)
| +----------- 小时 (0 - 23)
+------------- 分钟 (0 - 59)
    
15 * * * * /path/to/cleanup.sh    		//每小时的第 15 分钟运行清理脚本
0 0 1 * * /path/to/generate_report.sh //每个月的第 1 天午夜运行报告生成脚本    
0 8 * * 1 /path/to/send_reminder.sh  //每周一上午 8 点发送提醒邮件    
*/10 * * * * /path/to/script.sh 	//隔 10 分钟运行一次脚本
```



## 进程

```c
$0   //当前Shell程序的名称
$#   //传送给Shell程序的位置参数的数量
$?    //前一个命令或函数的返回值    0是正常返回 非0不是
```

```c++
ps			//报告进程信息
top			//实时报告
pstree  	//进程家族树
```

- 进程是操作系统**资源分配**和**独立运行**的**基本单元**
- 每个进程都有唯一进程标识符（PID）
- 进程是可执行程序的一次执行过程
- 进程控制块PCB是进程存在的唯一标志。

- 进程的基本状态:  就绪状态   执行状态    阻塞状态

`exec`:运行一个程序，即程序调用；

只有调用失败了，它们才会返回一个-1，从原程序的调用点接着往下执行  

`fork`:建立一个进程，即创建子进程；   

一个进程调用fork来复制自己。创建子进程后，父、子进程执行同一个程序，子进程继承父进程的资源  

返回值：子进程是0    父进程是子进程pid   错误是-1

`wait`:等待子进程结束；

暂停调用它的进程直到子进程结束    取得子进程结束时传给exit的值        ` pid = wait(NULL)`获得 `pid`或者 `-1`

`exit`:结束进程。  



## 线程

- 线程是操作系统能够进行运算调度的**最小单位**

- 多个线程**可共享资源**

- 线程和进程的最大区别在于**线程完全共享相同的地址空间，运行在同一地址上**。

  ```c++
  #include  <pthread.h>
  main()
  {
  	pthread_t t1, t2;		/* two threads */
  	void	*print_msg(void *);
  	pthread_create(&t1, NULL, print_msg, (void *)"hello");
  	pthread_create(&t2, NULL, print_msg, (void *)"world\n");
  	pthread_join(t1, NULL);
  	pthread_join(t2, NULL);
  }
  
  ```

  


## makefile

```c++
//makefile
cal:  cal.o add.o
     gcc –o cal  cal.o  add.o
cal.o: cal.c
     gcc –c  cal.c
add.o: add.c
     gcc –c  add.c
//make命令可以自动推导文件以及文件依赖关系后面的命令，make会自动识别并自己推导命令。只要make查到某个 .o 文件，它就好自动把相关的 .c 加到依赖文件中。
```



stat:文件状态

fputs(str,stdout);  





ßinitscr(): 初始化curses库；

ßendwin(): 关闭curses库;

ßmove(r, s): 移动光标到屏幕(r,s)位置；

ßaddstr(s): 当前位置绘制字符串s;

ßrefresh(): 更新屏幕；

ßclear(): 清屏；

