[root@song~]#    [root表用户@song表机器 ~表当前位置] #表管理员命令输入标志，$表普通用户输入标志

### **Linux目录结构**

- **/bin**：
  bin 是 Binaries (二进制文件) 的缩写, 这个目录存放着最经常使用的命令。

- **/boot：**
  这里存放的是启动 Linux 时使用的

  

  一些核心文件，包括一些连接文件以及镜像文件。

- **/dev ：**
  dev 是 Device(设备) 的缩写, 该目录下存放的是 Linux 的外部设备，在 Linux 中访问设备的方式和访问文件的方式是相同的。

- **/etc：**
  etc 是 Etcetera(等等) 的缩写,这个目录用来存放所有的系统管理所需要的配置文件和子目录。

- **/home**：
  用户的主目录，在 Linux 中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的，如上图中的 alice、bob 和 eve。

- **/lib**：
  lib 是 Library(库) 的缩写这个目录里存放着系统最基本的动态连接共享库，其作用类似于 Windows 里的 DLL 文件。几乎所有的应用程序都需要用到这些共享库。

- **/lost+found**：
  这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

- **/media**：
  linux 系统会自动识别一些设备，例如U盘、光驱等等，当识别后，Linux 会把识别的设备挂载到这个目录下。

- **/mnt**：
  系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在 /mnt/ 上，然后进入该目录就可以查看光驱里的内容了。

- **/opt**：
  opt 是 optional(可选) 的缩写，这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

- **/proc**：
  proc 是 Processes(进程) 的缩写，/proc 是一种伪文件系统（也即虚拟文件系统），存储的是当前内核运行状态的一系列特殊文件，这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
  这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

```
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```

- **/root**：
  该目录为系统管理员，也称作超级权限者的用户主目录。
- **/sbin**：
  s 就是 Super User 的意思，是 Superuser Binaries (超级用户的二进制文件) 的缩写，这里存放的是系统管理员使用的系统管理程序。
- **/selinux**：
   这个目录是 Redhat/CentOS 所特有的目录，Selinux 是一个安全机制，类似于 windows 的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。
- **/srv**：
   该目录存放一些服务启动之后需要提取的数据。
- **/sys**：

这是 Linux2.6 内核的一个很大的变化。该目录下安装了 2.6 内核中新出现的一个文件系统 sysfs 。

sysfs 文件系统集成了下面3种文件系统的信息：针对进程信息的 proc 文件系统、针对设备的 devfs 文件系统以及针对伪终端的 devpts 文件系统。

该文件系统是内核设备树的一个直观反映。

当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

- **/tmp**：
  tmp 是 temporary(临时) 的缩写这个目录是用来存放一些临时文件的。
- **/usr**：
   usr 是 unix shared resources(共享资源) 的缩写，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于 windows 下的 program files 目录。
- **/usr/bin：**
  系统用户使用的应用程序。
- **/usr/sbin：**
  超级用户使用的比较高级的管理程序和系统守护程序。
- **/usr/src：**
  内核源代码默认的放置目录。
- **/var**：
  var 是 variable(变量) 的缩写，这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。
- **/run**：
  是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。

在 Linux 系统中，有几个目录是比较重要的，平时需要注意不要误删除或者随意更改内部文件。

**/etc**： 上边也提到了，这个是系统中的配置文件，如果你更改了该目录下的某个文件可能会导致系统不能启动。

**/bin, /sbin, /usr/bin, /usr/sbin**: 这是系统预设的执行文件的放置目录，比如 **ls** 就是在 **/bin/ls** 目录下的。

值得提出的是 **/bin**、**/usr/bin** 是给系统用户使用的指令（除 root 外的通用用户），而/sbin, /usr/sbin 则是给 root 使用的指令。

**/var**： 这是一个非常重要的目录，系统上跑了很多程序，那么每个程序都会有相应的日志产生，而这些日志就被记录到这个目录下，具体在 /var/log 目录下，另外 mail 的预设放置也是在这里。

### **vim常用命令**

#### **一般模式（复制粘贴）**

vim + 文件名 进入

常用语法

| yy             | 复制光标当前行             |
| -------------- | -------------------------- |
| y 数字 y       | 复制一段（从第几行第几行） |
| p              | 箭头移动到目的行粘贴       |
| u              | 撤销上一部                 |
| dd             | 删除光标当行               |
| d 数字 d       | 删除光标后（含）多少行     |
| x              | 剪切一个字母               |
| yw             | 复制一个词                 |
| dw             | 删除一个词                 |
| shift+6 （^）  | 移动到行头                 |
| shift + 4（$） | 移动到行尾                 |
| 1+shift+g      | 移动到页头，数字           |
| shift+g        | 移动到页尾                 |
| 数字+shift+g   | 移动到目标行               |



#### **编辑模式（插入内容，正常文本编辑）**

直接在一般模式下输入下列指令进入

| i    | 当前光标前插入     |
| ---- | ------------------ |
| a    | 当前光标后插入     |
| o    | 当前光标行的下一行 |
| I    | 光标所在行的最前   |
| A    | 光标所在行的最后   |
| O    | 当前光标行的上一行 |

按Esc退出编辑模式，进入一般模式



#### **指令模式（搜索替换保存退出）**

 在一般模式下输入[:/?]三个按钮中任意一个便可进入

| :w                                         | 保存                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| :q                                         | 退出                                                         |
| :!                                         | 强制执行（:w!若文件属性为『只读』时，强制写入该档案。:q!若曾修改过档案，又不想储存，使用 ! 为强制离开不储存档案） |
| /要查找的词                                | 向光标之下查找，按n查找下一个，N向上查找                     |
| ?要查找的词                                | 在光标之上查找                                               |
| :noh                                       | 取消高亮显示                                                 |
| :set nu                                    | 显示行号                                                     |
| :set nonu                                  | 关闭行号                                                     |
| :n1,n2s/word1/word2/g                      | n1 与 n2 为数字。在第 n1 与 n2 行之间寻找 word1 这个字符串，并将该字符串取代为 word2 ！举例来说，在 100 到 200 行之间搜寻 vbird 并取代为 VBIRD 则：『:100,200s/vbird/VBIRD/g』。(常用) |
| :1,$s/word1/word2/g 或 :%s/word1/word2/g   | 从第一行到最后一行寻找 word1 字符串，并将该字符串取代为 word2 ！(常用) |
| :1,$s/word1/word2/gc 或 :%s/word1/word2/gc | 从第一行到最后一行寻找 word1 字符串，并将该字符串取代为 word2 ！且在取代前显示提示字符给用户确认 (confirm) 是否需要取代！(常用) |
| :wq!                                       | 强制保存退出                                                 |



### **网络配置**

#### **显示所有网络接口的配置**

ifconfig

#### **测试主机之间的连通性**

ping 目标主机（如 IP或 www.baidu.com）

#### **修改IP地址**

- 查看IP配置文件

vim /etc/sysconfig/network-scripts/ifcfg-ens33     

- 修改

以下标红的项必须修改,有值的按照下面的值修改,没有该项的要增加。  

```
TYPE="Ethernet"
#网络类型(通常是 Ethemet)
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static"     # 修改
#IP 的配置方法[none|static|bootp|dhcp](引导
时不 使用协议|静态分配 IP|BOOTP 协议|DHCP 协议)
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="e83804c1-3257-4584-81bb-660665ac22f6"
#随机 id
DEVICE="ens33"
#接口名(设备,网卡)

#以下修改
ONBOOT="yes"
#系统启动的时候网络接口是否有效(yes/no)
#IP 地址
IPADDR=192.168.1.100
#网关
GATEWAY=192.168.1.2
#域名解析器
DNS1=192.168.1.2
```



- 重启网络  

service network restart

- 修改后可能遇到的问题

(1)物理机能 ping 通虚拟机,但是虚拟机 ping 不通物理机,一般都是因为物理机的 防火墙问题,把防火墙关       闭就行

(2)虚拟机能 Ping 通物理机,但是虚拟机 Ping 不通外网,一般都是因为 DNS 的设置有问题

(3)虚拟机 Ping www.baidu.com 显示域名未知等信息,一般查看 GATEWAY 和 DNS 设置是否正确

(4)如果以上全部设置完还是不行,需要关闭 NetworkManager 服务

  systemctl stop NetworkManager   关闭

  systemctl disable NetworkManager 禁用

(5)如果检查发现 systemctl status network 有问题 需要检查 ifcfg-ens3



#### **配置主机名**

- 查看当前服务器主机名称

hostname

- 修改主机名

​    vim /etc/hostname 重启完生效

- 修改hosts映射文件

1)  修改 linux 的主机映射文件(hosts 文件)

后续在 hadoop 阶段,虚拟机会比较多,配置时通常会采用主机名的方式配置,比较简单方便。 不用刻意记 ip 地址。

- 打开/etc/hosts

vim /etc/hosts

- 添加如下内容

192.168.2.100   hadoop100

192.168.2.101  hadoop101

192.168.2.102  hadoop102

- 重启设备,重启后,查看主机名,已经修改成功

2) 修改 windows 的主机映射文件(hosts 文件)

-  进入 C:\Windows\System32\drivers\etc 路径
- 打开 hosts 文件并添加如下内容

192.168.2.100   hadoop100

192.168.2.101  hadoop101

192.168.2.102  hadoop102

#### **远程登录**

使用工具xshell连接主机，使用xftp传输文件

或者使用  ssh 主机名 连接





### **系统管理(centOS 7)**

#### **设置后台服务的自启配置**

计算机中,一个正在执行的程序或命令,被叫做“进程”(process)。

启动之后一只存在、常驻内存的进程,一般被称作“服务”(service)。

1) 基本语法

systemctl start | stop | restart | status  服务名

2) 经验技巧

查看服务的方法:/usr/lib/systemd/system

```
[root@hadoop100 system]# pwd
/usr/lib/systemd/system
[root@hadoop100 init.d]# ls -al
-rw-r--r--. 1 root root 275 4 月27 2018 abrt-ccpp.service
```

3)案例实操

(1)查看防火墙服务的状态

[root@hadoop100 桌面]# systemctl status firewalld

(2)停止防火墙服务

[root@hadoop100 桌面]# systemctl stop firewalld

(3)启动防火墙服务

[root@hadoop100 桌面]# systemctl start firewalld

(4)重启防火墙服务

[root@hadoop100 桌面]# systemctl restart firewalld

(5）功能描述:查看服务开机启动状态

systemctl list-unit-files

(6）功能描述:关掉指定服务的自动启动

systemctl disable service_name 

 (7）功能描述:开启指定服务的自动启动

systemctl enable service_name

```
开启/关闭 iptables(防火墙)服务的自动启动
[root@hadoop100 桌面]# systemctl enable firewalld.service
[root@hadoop100 桌面]# systemctl disable firewalld.service
```

#### **系统运行级别**

1)Linux系统有七种运行级别：常用是3和5

0：系统停机状态（默认不能为0）

2：单用户，root权限，用户系统维护，禁止远程登录

3：多用户，命令行模式

4：系统未使用，保留

5：图形GUI模式

6：系统正常关闭并重启（默认不能为6）

**快捷方式：**

ctrl+art+F1          图形化页面

ctrl+art+F2-F7       6个不同的shell命令行页面



2)CentOS7 的运行级别简化为:

multi-user.target 等价于原运行级别 3(多用户有网,无图形界面)

graphical.target 等价于原运行级别 5(多用户有网,有图形界面)



3) 查看当前运行级别:

systemctl get-default



4)修改当前运行级别

systemctl set-default TARGET.target (这里 TARGET 取 multi-user 或者 graphical)



#### **系统关机重启命令**

1)基本语法

(1)sync (功能描述:将数据由内存同步到硬盘中)

(2)halt (功能描述:停机,关闭系统,但不断电)

(3)poweroff (功能描述:关机,断电)

(3)reboot (功能描述:就是重启,等同于 shutdown -r now)

(4)shutdown [选项] 时间

| 选项 | 功能                 |
| ---- | -------------------- |
| -H   | 相当用于--halt，停机 |
| -r   | -r=reboot，重启      |
| -h   | 关机                 |

| 参数 | 功能                       |
| ---- | -------------------------- |
| now  | 立刻关机                   |
| 时间 | 等待多久关机（单位是分钟） |

2) 经验技巧

Linux 系统中为了提高磁盘的读写效率,对磁盘采取了 “预读迟写”操作方式。当用户

保存文件时,Linux 核心并不一定立即将保存数据写入物理磁盘中,而是将数据保存在缓

冲区中,等缓冲区满时再写入磁盘,这种方式可以极大的提高磁盘写入数据的效率。但是,

也带来了安全隐患,如果数据还未写入磁盘时,系统掉电或者其他严重问题出现,则将导

致数据丢失。使用 sync 指令可以立即将缓冲区的数据写入磁盘。

3)案例实操

(1)将数据由内存同步到硬盘中

[root@hadoop100 桌面]#sync

(2)重启

[root@hadoop100 桌面]# reboot

(3)停机(不断电)

[root@hadoop100 桌面]#halt

(4)计算机将在 1 分钟后关机,并且会显示在登录用户的当前屏幕中

[root@hadoop100 桌面]#shutdown -h 1 ‘This server will shutdown after 1 mins’

(5)立马关机(等同于 poweroff)

[root@hadoop100 桌面]# shutdown -h now

(6)系统立马重启(等同于 reboot)

[root@hadoop100 桌面]# shutdown -r now



### **Linux常用命令**

#### **常用快捷键**

| ctrl + c      | 停止进程                           |
| ------------- | ---------------------------------- |
| ctrl+l        | 清屏,等同于 clear;彻底清屏是:reset |
| 善于用 tab 键 | 提示(更重要的是可以防止敲错)       |
| 上下键        | 查找执行过的命令                   |



#### **帮助命令**

| 命令                 | 功能                                   | 示例                        |
| -------------------- | -------------------------------------- | --------------------------- |
| man [命令或配置文件] | 功能描述:获得帮助信息                  | man ls   (只能显示外部命令) |
| help 命令            | 功能描述:获得 shell 内置命令的帮助信息 | help cd                     |
| --help               | 可以显示外部命令                       | ls --help                   |
| type 命令            | 显示是否内嵌命令                       | type cd                     |



#### **文件目录**

| 命令                                                         | 选项                                                         | 功能                               | 经验技巧                                                     | 示例                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| pwd                                                          |                                                              | 显示当前工作目录的绝对路径         |                                                              | [root@hadoop101~]#                                           |
| ls[选项][目录或者文件]                                       | -a：全部文件（包含隐藏文件）-l：长数据串列出，包含文件的属性或者权限，等价ll | 列出目录内容                       |                                                              | [atguigu@hadoop101 ~]$ ls -al                                |
| cd[参数]                                                     | cd 绝对路径  ：切换路径cd 相对路径  ：切换路径cd ~或者 cd：回到自己家目录cd - ：回到上一次所在的目录cd ..：回到当前的上一级目录cd -P：跳转到实际的物理路径 | 切换路径                           |                                                              | [root@hadoop101 ~]# cd /root/                                |
| mkdir [选项] 要创建的目录                                    | -p：创建多层目录                                             | 创建一个新的目录                   |                                                              | 创建一个目录[root@hadoop101 ~]# mkdir xiyou/mingjie创建一个多级目录[root@hadoop101 ~]# mkdir -p xiyou/dssz/meihouwang |
| rmdir 要删除的目录                                           |                                                              | 删除一个空的目录                   |                                                              | [root@hadoop101 ~]# rmdir xiyou/dssz/meihouwang              |
| touch 文件名称                                               |                                                              | 创建空文件                         |                                                              | [root@hadoop101 ~]# touch xiyou/dssz/sunwukong.txt           |
| cp[选项]source dest                                          | -r ：递归复制整个文件夹                                      | 复制文件或者目录                   | 强制覆盖不提示：\cp                                          | (1)复制文件[root@hadoop101 ~]# cp xiyou/dssz/suwukong.txt xiyou/mingjie/(2)递归复制整个文件夹[root@hadoop101 ~]# cp -r xiyou/dssz/ ./ |
| rm[选项] deleteFile                                          | -r：递归删除目录中所有内容-f：强制执行删除操作,而不提示用于进行确认。-v ：显示指令的详细执行过程 | 删除文件或者目录                   |                                                              | (1)删除目录中的内容[root@hadoop101 ~]# rm xiyou/mingjie/sunwukong.txt(2)递归删除目录中所有内容[root@hadoop101 ~]# rm -rf dssz/ |
| mv oldNameFile newNameFilemv /temp/movefile /targetFolder    |                                                              | 移动文件与重命名                   |                                                              | (1)重命名[root@hadoop101 ~]# mv xiyou/dssz/suwukong.txt xiyou/dssz/houge.txt(2)移动文件[root@hadoop101 ~]# mv xiyou/dssz/houge.txt ./ |
| cat [选项] 要查看的文件                                      | -n：显示所有行号，包括空行                                   | 查看文件内容                       | 一般查看比较小的文件，一屏幕能显示全的                       | (1)查看文件内容并显示行号[atguigu@hadoop101 ~]$ cat -n houge.txt |
| more 要查看的文件                                            | 空白键 (space)：代表向下翻一页;Enter：代表向下翻『一行』q：代表立刻离开 more ,不再显示该文件内容。Ctrl+F：向下滚动一屏Ctrl+B：返回上一屏=：输出当前行的行号:f：输出文件名和当前行的行号 | 以全屏的..方式查看文件             |                                                              | [root@hadoop101 ~]# more smartd.conf                         |
| less 要查看的文件                                            | 空白键：向下翻动一页;[pagedown]：向下翻动一页[pageup]：向上翻动一页/字串：向下搜寻『字串』的功能;n:向下查找;N:向上查找;?字串：向上搜寻『字串』的功能;n:向上查找;N:向下查找;q：离开 less 这个程序 | 高效率查看文件（一般用于大型文件） | 用SecureCRT时[pagedown]和[pageup]可能会出现无法识别的问题。  | [root@hadoop101 ~]# less smartd.conf                         |
| echo[选项][输出内容]                                         | -e: 支持反斜线控制的字符转换控制字符：\\ ：输出\本身；\n ：换行符；\t：制表符,也就是 Tab 键 | 输出内容到控制台                   |                                                              | [atguigu@hadoop101 ~]$ echo “hello\tworld”hello\tworld       |
| head [选项]文件                                              | -n<行数>：指定显示头部内容的行数                             | 显示文件头部内容（默认前10行）     |                                                              | 查看文件的头2行[root@hadoop101 ~]# head -n 2 smartd.conf     |
| tail[选项] 文件                                              | -n<行数>：指定显示头部内容的行数-f：显示文件最新追加的内容,监视文件变化 | 显示文件尾部内容（默认前10行）     |                                                              | (1)查看文件尾 1 行内容[root@hadoop101 ~]# tail -n 1 smartd.conf(2)实时追踪该档的所有更新[root@hadoop101 ~]# tail -f houge.txt |
| (1)ls -l **>** 文件(功能描述:列表的内容写入文件 a.txt 中(覆盖写))(2)ls -al **>>** 文件 (功能描述:列表的内容追加到文件 aa.txt 的末尾)(3)cat 文件 1 **>** 文件 2 (功能描述:将文件 1 的内容覆盖到文件 2)(4)echo “内容” **>>** 文件 |                                                              | > 输出重定向和 >> 追加             |                                                              | (1)将 ls 查看信息写入到文件中[root@hadoop101 ~]# ls -l>houge.txt(2)将 ls 查看信息追加到文件中[root@hadoop101 ~]# ls -l>>houge.txt(3)采用 echo 将 hello 单词追加到文件中[root@hadoop101 ~]# echo hello>>houge.txt |
| ln -s [原文件或目录] [软链接名]                              |                                                              | 给原文件创建一个软链接             | 删除软链接: rm -rf 软链接名,而不是 rm -rf 软链接名/如果使用 rm -rf 软链接名/ 删除,会把软链接对应的真实目录下内容删掉查询:通过 ll 就可以查看,列表属性第 1 位是 l,尾部会有位置指向 | (1)创建软连接[root@hadoop101 ~]# mv houge.txt xiyou/dssz/[root@hadoop101 ~]# ln -s xiyou/dssz/houge.txt ./houzi[root@hadoop101 ~]# lllrwxrwxrwx. 1 rootroot20 6 月 17 12:56 houzi ->xiyou/dssz/houge.txt(2)删除软连接(注意不要写最后的/)[root@hadoop101 ~]# rm -rf houzi(3)进入软连接实际物理路径[root@hadoop101 ~]# ln -s xiyou/dssz/ |
| history                                                      |                                                              | 查看已经执行过历史命令             |                                                              | (1)查看已经执行过的历史命令[root@hadoop101 test1]# history   |



#### **文件权限**

Linux系统是一种典型的多用户系统,不同的用户处于不同的地位,拥有不同的权限。为了保护系统的安全性,Linux系统对不同的用户访问同一文件(包括目录文件)的权限做了不同的规定。在Linux中我们可以使用ll或者ls -l命令来显示一个文件的属性以及文件所属的用户和组。

**1)从左到右的 10 个字符表示 （使用ll命令）**

 -rw-rw-r-- 1 xcadmin xcadmin 4518658 4月  1 10:36 '尚硅谷高级技术之Linux(CentOS7.9).pdf'

(1)0 首位表示类型

在Linux中第一个字符代表这个文件是目录、文件或链接文件等等

\- 代表文件

d 代表目录

l 链接文档(link file);

(2)第1-3位确定属主(该文件的所有者)拥有该文件的权限。---User

(3)第4-6位确定属组(所有者的同组用户)拥有该文件的权限,---Group

(4)第7-9位确定其他用户拥有该文件的权限 ---Other

第10位连接数，如果查看到是文件:链接数指的是硬链接个数。如果查看的是文件夹:链接数指的是子文件夹个数

11位是文件属主，12位是文件属组，13位是文件大小，14位是建立或最近修改时间，15位文件名字

**2)rwx 作用文件和目录的不同解释**

(1)作用到文件:

[ r ]代表可读(read): 可以读取,查看

[ w ]代表可写(write): 可以修改,但是不代表可以删除该文件,删除一个文件的前提条件是对该文件所在的目录有写权限,才能删除该文件.

[ x ]代表可执行(execute):可以被系统执行

(2)作用到目录:

[ r ]代表可读(read): 可以读取,ls查看目录内容

[ w ]代表可写(write): 可以修改,目录内创建+删除+重命名目录

[ x ]代表可执行(execute):可以进入该目录

| 命令                                | 功能                             | 经验技巧                                            | 示例                                                         |
| ----------------------------------- | -------------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| chmod [{ugoa}{+-=}{rwx}] 文件或目录 | 第一种方式**变更权限**           | u:所有者 g:所有组 o:其他人 a:所有人(u、g、o 的总和) | 1)修改文件使其所属主用户具有执行权限[root@hadoop101 ~]# cp xiyou/dssz/houge.txt ./[root@hadoop101 ~]# chmod u+x houge.txt(2)修改文件使其所属组用户具有执行权限[root@hadoop101 ~]# chmod g+x houge.txt(3)修改文件所属主用户执行权限,并使其他用户具有执行权限[root@hadoop101 ~]# chmod u-x,o+x houge.txt |
| chmod [mode=421 ] [文件或目录]      | 第二种方式**变更权限**           | r=4 w=2 x=1rwx=4+2+1=7                              | (4)采用数字的方式,设置文件所有者、所属组、其他用户都具有可读可写可执行权限。[root@hadoop101 ~]# chmod 777 houge.txt(5)修改整个文件夹里面的所有文件的所有者、所属组、其他用户都具有可读可写可执行权限。[root@hadoop101 ~]# chmod -R 777 xiyou/ |
| chown [-R] [最终用户] [文件或目录]  | **改变**文件或者目录的**所有者** | -R是递归操作                                        | (1)修改文件所有者[root@hadoop101 ~]# chown atguigu houge.txt[root@hadoop101 ~]# ls -al-rwxrwxrwx. 1 atguigu root 551 5 月 23 13:02 houge.txt(2)递归改变文件所有者和所有组[root@hadoop101 xiyou]# lldrwxrwxrwx. 2 root root 4096 9 月3 21:20 xiyou[root@hadoop101 xiyou]# chown -R atguigu:atguigu xiyou/[root@hadoop101 xiyou]# lldrwxrwxrwx. 2 atguigu atguigu 4096 9 月3 21:20 xiyou |
| chgrp [最终用户组] [文件或目录]     | **改变**文件或者目录的**所属组** |                                                     | [root@hadoop101 ~]# chgrp root houge.txt[root@hadoop101 ~]# ls -al-rwxrwxrwx. 1 atguigu root 551 5 月 23 13:02 houge.txt |



#### **搜索查找**



| 命令                      | 选项                                                         | 功能                    | 经验技巧                                                     | 示例                                                         |
| ------------------------- | ------------------------------------------------------------ | ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| find [搜索范围] [选项]    | -name<查询方式>:按照指定的文件名查找模式查找文件-user<用户名>:查找属于指定用户名所有文件-size<文件大小>:按照指定的文件大小查找文件,单位为:b —— 块(512 字节)c —— 字节w —— 字(2 字节)k —— 千字节M —— 兆字节G —— 吉字节 | find 查找文件或者目录   |                                                              | (1)按文件名:根据名称查找/目录下的filename.txt文件。[root@hadoop101 ~]# find xiyou/ -name "*.txt"(2)按拥有者:查找/opt目录下,用户名称为-user的文件[root@hadoop101 ~]# find xiyou/ -user atguigu(3)按文件大小:在/home目录下查找大于200m的文件(+n 大于 -n小于 n等于)[root@hadoop101 ~]find /home -size +204800 |
| locate 搜索文件           |                                                              | locate 快速定位文件路径 | 由于 locate 指令基于数据库进行查询,所以第一次运行前,必须使用 updatedb 指令创建 locate 数据库。 | (1)查询文件夹[root@hadoop101 ~]# updatedb[root@hadoop101 ~]#locate tmp |
| grep 选项 查找内容 源文件 | -n:显示匹配行及行号                                          | 过滤查找以及管道符“\|”  | 管道符,“\|”,表示将前一个命令的处理结果输出传递给后面的命令处理 | (1)查找某文件在第几行[root@hadoop101 ~]# ls \| grep -n test  |



#### **压缩和解压**



| 命令                                     | 选项                                                         | 功能                               | 经验技巧                                                     | 示例                                                         |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| gzip 文件                                |                                                              | 压缩文件,只能将文件压缩为*.gz 文件 | (1)只能压缩文件不能压缩目录(2)不保留原来的文件(3)同时多个文件会产生多个压缩包 | (1)gzip压缩[root@hadoop101 ~]# lstest.java[root@hadoop101 ~]# gzip houge.txt[root@hadoop101 ~]# lshouge.txt.gz |
| gunzip 文件.gz                           |                                                              | 解压缩文件命令                     | (2)gunzip解压缩文件[root@hadoop101 ~]# gunzip houge.txt.gz[root@hadoop101 ~]# lshouge.txt |                                                              |
| zip [选项] XXX.zip 将要压缩的内容        | -r:压缩目录                                                  | 压缩文件和目录的命令               | zip 压缩命令在windows/linux都通用,可以压缩目录且保留源文件。 | (1)压缩 houge.txt 和bailongma.txt,压缩后的名称为mypackage.zip[root@hadoop101 opt]# touch bailongma.txt[root@hadoop101 ~]# zip mypackage.zip houge.txt bailongma.txtadding: houge.txt (stored 0%)adding: bailongma.txt (stored 0%)[root@hadoop101 opt]# lshouge.txtbailongma.txtmypackage.zip |
| unzip XXX.zip [选项]                     | -d<目录>：指定解压后文件的存放目录                           | 解压缩文件                         | 解压mypackage.zip到指定目录-d[root@hadoop101 ~]# unzip mypackage.zip -d /opt[root@hadoop101 ~]# ls /opt/ |                                                              |
| tar [选项] XXX.tar.gz 将要打包进去的内容 | -c：产生.tar 打包文件-v：显示详细信息-f：指定压缩后的文件名-z：打包同时压缩-x：解包.tar 文件-C：解压到指定目录 | 打包目录,压缩后的文件格式.tar.gz   |                                                              | (1)压缩多个文件[root@hadoop101 opt]# tar -zcvf houma.tar.gz houge.txt bailongma.txthouge.txtbailongma.txt[root@hadoop101 opt]# lshouma.tar.gz houge.txt bailongma.txt(2)压缩目录[root@hadoop101 ~]# tar -zcvf xiyou.tar.gz xiyou/xiyou/xiyou/mingjie/xiyou/dssz/xiyou/dssz/houge.txt(3)解压到当前目录[root@hadoop101 ~]# tar -zxvf houma.tar.gz(4)解压到指定目录[root@hadoop101 ~]# tar -zxvf |
|                                          |                                                              |                                    |                                                              |                                                              |

#### **进程管理**

1)**ps aux 显示信息说明**

USER:该进程是由哪个用户产生的

PID:进程的 ID 号

%CPU:该进程占用 CPU 资源的百分比,占用越高,进程越耗费资源;

%MEM:该进程占用物理内存的百分比,占用越高,进程越耗费资源;

VSZ:该进程占用虚拟内存的大小,单位 KB;

RSS:该进程占用实际物理内存的大小,单位 KB;

TTY:该进程是在哪个终端中运行的。对于 CentOS 来说,tty1 是图形化终端,tty2-tty6 是本地的字符界面终端。pts/0-255 代表虚拟终端。

STAT:进程状态。常见的状态有:R:运行状态、S:睡眠状态、T:暂停状态、Z:僵尸状态、s:包含子进程、l:多线程、+:前台显示

START:该进程的启动时间

TIME:该进程占用 CPU 的运算时间,注意不是系统时间

COMMAND:产生此进程的命令名



(2)**ps -ef 显示信息说明**

UID:用户 ID

PID:进程 ID

PPID:父进程 ID

C:CPU 用于计算执行优先级的因子。数值越大,表明进程是 CPU 密集型运算,执行优先级会降低;数值越小,表明进程是 I/O 密集型运算,执行优先级会提高

STIME:进程启动的时间

TTY:完整的终端名称

TIME:CPU 时间

CMD:启动进程所用的命令和参数



(3)**top查询结果字段解释(自行百度)**

第一行信息为任务队列信息

第二行为进程信息

第三行为 CPU 信息

第四行为物理内存信息

第五行为交换分区(swap)信息

| 命令                        | 选项                                                         | 功能                                                         | 经验技巧                                                     | 示例                                                         |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ps aux \| grep xxx          | a：列出带有终端的所有用户的进程x：列出当前用户的所有进程,包括没有终端的进程u：面向用户友好的显示风格-e：列出所有进程-u：列出某个用户关联的所有进程-f：显示完整格式的进程列表 | 查看系统中所有进程                                           | 如果想查看进程的 CPU 占用率和内存占用率,可以使用 aux;如果想查看进程的父进程 ID 可以使用 ef; | [root@hadoop101 datas]# ps aux                               |
| ps -ef \| grep xxx          | 可以查看子父进程之间的关系                                   | [root@hadoop101 datas]# ps -ef                               |                                                              |                                                              |
| kill [选项] 进程号          | -9:表示强迫进程立即停止                                      | 通过进程号杀死进程                                           |                                                              | (1)杀死浏览器进程[root@hadoop101 桌面]# kill -9 5102         |
| killall 进程名称            |                                                              | 通过进程名称杀死进程,也支持通配符,这在系统因负载过大而变得很慢时很有用 |                                                              | (2)通过进程名称杀死进程[root@hadoop101 桌面]# killall firefox |
| pstree [选项]               | -p:显示进程的 PID-u:显示进程的所属用户                       | 查看进程树                                                   |                                                              | (1)显示进程 pid[root@hadoop101 datas]# pstree -p(2)显示进程所属用户[root@hadoop101 datas]# pstree -u |
| top [选项]                  | -d 秒数：指定 top 命令每隔几秒更新。默认是 3 秒在 top 命令的交互模式当中可以执行的命令-i：使 top 不显示任何闲置或者僵死进程。-p：通过指定监控进程 ID 来仅仅监控某个进程的状态。 | 实时监控系统进程状态                                         | 操作P:以 CPU 使用率排序,默认就是此项M:以内存的使用率排序N:以 PID 排序q:退出 top | [root@hadoop101 atguigu]# top -d 1[root@hadoop101 atguigu]# top -i[root@hadoop101 atguigu]# top -p 2575 |
| netstat -anp \| grep 进程号 | -a： 显示所有正在监听(listen)和未监听的套接字(socket)-n ：拒绝显示别名,能显示数字的全部转化成数字-l ：仅列出在监听的服务状态-p： 表示显示哪个进程在调用 | 查看该进程网络信息                                           |                                                              | (1)通过进程号查看sshd进程的网络信息[root@hadoop101 hadoop-2.7.2]# netstat -anp \| grep sshd |
| netstat –nlp \| grep 端口号 | 查看网络端口号占用情况                                       |                                                              | (2)查看某端口号是否被占用[root@hadoop101 桌面]# netstat -nltp \| grep 22 |                                                              |

#### **crontab 系统定时任务**

重新启动 crond 服务

[root@hadoop101 ~]# systemctl restart crond



| 命令           | 选项                                                         | 功能         | 经验技巧 | 示例                                                         |
| -------------- | ------------------------------------------------------------ | ------------ | -------- | ------------------------------------------------------------ |
| crontab [选项] | -e ：编辑 crontab 定时任务-l ：查询 crontab 任务-r ：删除当前用户所有的 crontab 任务 | 定时任务设置 |          | (1)每隔 1 分钟,向/root/bailongma.txt 文件中添加一个 11 的数字*/1 * * * * /bin/echo ”11” >> /root/bailongma.txt |



进入 crontab 编辑界面。会打开 vim 编辑你的工作。

[root@hadoop101 ~]# crontab -e

\* * * * * 执行的任务

项目   含义  范围

第一个“*” 一小时当中的第几分钟 0-59

第二个“*” 一天当中的第几小时 0-23

第三个“*” 一个月当中的第几天 1-31

第四个“*” 一年当中的第几月 1-12

第五个“*” 一周当中的星期几 0-7 ( 0 和 7 都 代 表 星 期日)

特殊符号 含义

\* 代表任何时间。比如第一个“*”就代表一小时中每分钟都执行一次的意思。

,代表不连续的时间。比如“0 8,12,16 * * * 命令”,就代表在每天的 8 点 0 分,12 点 0 分,16 点 0 分都执行一次命令

-代表连续的时间范围。比如“0 5 * * 1-6 命令”,代表在周一到周六的凌晨 5 点 0 分执行命令

*/n代表每隔多久执行一次。比如“*/10 * * * * 命令”,代表每隔 10 分钟就执行一遍命令

特定时间执行命令

时间 含义

45 22 * * * 命令 每天 22 点 45 分执行命令

0 17 * * 1 命令 每周 1 的 17 点 0 分执行命令

0 5 1,15 * * 命令 每月 1 号和 15 号的凌晨 5 点 0 分执行命令

40 4 * * 1-5 命令 每周一到周五的凌晨 4 点 40 分执行命令

*/10 4 * * * 命令 每天的凌晨 4 点,每隔 10 分钟执行一次命令

0 0 1,15 * 1 命令 每月 1 号和 15 号,每周 1 的 0 点 0 分都会执行命令。注意:星期几和几号最好不要同时出现,因为他们定义的都是天。非常容易让管理员混乱。

#### **时间日期**

date [OPTION]... [+FORMAT]

[OPTION].:

-d<时间字符串>：显示指定的“时间字符串”表示的时间,而非当前时间

-s<日期时间>：设置系统日期时间

[+FORMAT]:<+日期时间格式>:指定显示时使用的日期时间格式

| 命令                      | 选项                         | 功能                  | 经验技巧                                 | 示例                                              |
| ------------------------- | ---------------------------- | --------------------- | ---------------------------------------- | ------------------------------------------------- |
| date                      |                              | 显示当前时间          |                                          | [root@hadoop101 ~]# date                          |
| date [+选项]              | %Y:年%m:月 %d:日             | 显示当前时间年月日    |                                          | [root@hadoop101 ~]# date +%Y%m%d                  |
| date "+%Y-%m-%d %H:%M:%S" |                              | 显示年月日时分秒      |                                          | [root@hadoop101 ~]# date "+%Y-%m-%d %H:%M:%S"     |
| date -d '1 days ago'      |                              | 显示非当前时间        | 显示前一天时间                           | [root@hadoop101 ~]# date -d '1 days ago'          |
| date -d '-1 days ago'     |                              | 显示明天时间          | [root@hadoop101 ~]#date -d '-1 days ago' |                                                   |
| date -s 字符串时间        |                              | 设置系统时间          |                                          | [root@hadoop101 ~]# date -s "2017-06-19 20:52:18" |
| cal [选项]                | 具体某一年：显示这一年的日历 | 不加选项,显示本月日历 |                                          | 查看 2017 年的日历[root@hadoop101 ~]# cal 2017    |

#### **用户管理**



| 命令                     | 选项                                                        | 功能                             | 经验技巧                                                  | 示例                                                         |
| ------------------------ | ----------------------------------------------------------- | -------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| useradd [g 组名] 用户名  | 添加新用户到某个组                                          | 添加新用户                       |                                                           | (1)添加一个用户[root@hadoop101 ~]# useradd tangseng[root@hadoop101 ~]#ll /home/ |
| passwd 用户名            |                                                             | 设置用户密码                     |                                                           | (1)设置用户的密码[root@hadoop101 ~]# passwd tangseng         |
| id 用户名                |                                                             | 查看用户是否存在                 |                                                           | [root@hadoop101 ~]#id tangseng                               |
| cat /etc/passwd          |                                                             | 查看创建了哪些用户               |                                                           | [root@hadoop101 ~]# cat/etc/passwd                           |
| su [-] 用户名称          | -：切换到用户并获得该用户的环境变量及执行权限               | 切换用户                         | 没有加-，切换用户,只能获得用户的执行权限,不能获得环境变量 | [root@hadoop101 ~]#su tangseng[root@hadoop101 ~]#echo $PATH  |
| userdel [-r ] 用户名     | -r:删除用户的同时,删除与用户相关的所有文件。                | 删除用户                         | 没有-r,删除用户但保存用户主目录                           | [root@hadoop101 ~]#userdel tangseng[root@hadoop101 ~]#ll /home/ |
| whoami                   |                                                             | 显示自身用户名称                 |                                                           |                                                              |
| who am i                 |                                                             | 显示登录用户的用户名以及登陆时间 |                                                           |                                                              |
| usermod -g 用户组 用户名 | -g：修改用户的初始登录组,给定的组必须存在。默认组 id 是 1。 | 修改用户                         |                                                           | (1)将用户加入到用户组[root@hadoop101 opt]# usermod -g root zhubajie |
| sudo                     |                                                             | 设置普通用户具有 root 权限       |                                                           | 用普通用户在/opt 目录下创建一个文件夹[atguigu@hadoop101 opt]$ sudo mkdir module |

1)添加 atguigu 用户,并对其设置密码。

[root@hadoop101 ~]#useradd atguigu

[root@hadoop101 ~]#passwd atguigu

2)修改配置文件

[root@hadoop101 ~]#vi /etc/sudoers

修改 /etc/sudoers 文件,找到下面一行(91 行),在 root 下面添加一行,如下所示:

```
## Allow root to run any commands anywhere
root         ALL=(ALL)     ALL
atguigu    ALL=(ALL)    ALL
```



或者配置成采用 sudo 命令时,不需要输入密码

```
## Allow root to run any commands anywhere
root        ALL=(ALL)        ALL
atguigu    ALL=(ALL)        NOPASSWD:ALL
```

修改完毕,现在可以用 atguigu 帐号登录,然后用命令 sudo ,即可获得 root 权限进行

操作。

#### **用户组管理**

每个用户都有一个用户组,系统可以对一个用户组中的所有用户进行集中管理。不同

Linux 系统对用户组的规定有所不同,

如Linux下的用户属于与它同名的用户组,这个用户组在创建用户时同时创建。

用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对

/etc/group文件的更新。

| 命令                      | 选项                           | 功能             | 经验技巧 | 示例                                                         |
| ------------------------- | ------------------------------ | ---------------- | -------- | ------------------------------------------------------------ |
| groupadd 组名             |                                | 新增组           |          | 添加一个xitianqujing组[root@hadoop101 opt]#groupadd xitianqujing |
| groupdel 组名             |                                | 删除组           |          | (1)删除xitianqujing组[root@hadoop101 opt]# groupdel xitianqujing |
| groupmod -n 新组名 老组名 | -n<新组名>：指定工作组的新组名 | 修改组           |          | 1)修改atguigu组名称为atguigu1[root@hadoop101 ~]#groupadd xitianqujing |
| cat /etc/group            |                                | 查看创建了哪些组 |          | [root@hadoop101 atguigu]# cat/etc/group                      |

#### **磁盘查看和分区**





| 命令                                       | 选项                                                         | 功能                                                         | 经验技巧                         | 示例                                                         |
| ------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------- | ------------------------------------------------------------ |
| du 目录/文件                               | -h：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示-a：不仅查看子目录大小,还要包括文件-c：显示所有的文件和子目录大小后,显示总和-s：只显示总和--max-depth=n：指定统计子目录的深度为第 n 层 | 显示目录下每个**子目录的磁盘使用情况**                       |                                  | (1)查看当前用户主目录占用的磁盘空间大小[root@hadoop101 ~]# du -sh |
| df 选项                                    | -h：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示   | 列出文件系统的**整体磁盘使用量**,检查文件系统的磁盘空间占用情况 |                                  | df -h                                                        |
| lsblk                                      | -f:查看详细的设备挂载情况,显示文件系统信息                   |                                                              |                                  |                                                              |
| mount [-t vfstype] [-o options] device dir |                                                              | 挂载设备                                                     | 自行百度                         |                                                              |
| umount 设备文件名或挂载点                  |                                                              | 卸载设备                                                     |                                  |                                                              |
| fdisk -l                                   | -l：显示所有硬盘的分区列表                                   | 查看磁盘分区详情                                             | 该命令必须在 root 用户下才能使用 |                                                              |
| fdisk 硬盘设备名                           |                                                              | 对新增硬盘进行分区操作                                       |                                  |                                                              |

**fdisk 分区**

1)Linux 分区

Device:分区序列

Boot:引导

Start:从X磁柱开始

End:到Y磁柱结束

Blocks:容量

Id:分区类型ID

System:分区类型

(2)分区操作按键说明

m:显示命令列表

p:显示当前磁盘分区

n:新增分区

w:写入分区信息并退出

q:不保存分区信息直接退出





### **软件包管理**

**rpm 只能安装已经下载到本地机器上的rpm 包. yum能在线下载并安装rpm包,能更新系统,且还能自动处理包与包之间的依赖问题,这个是rpm 工具所不具备的。**

#### **RPM(本地)**

RPM(RedHat Package Manager),RedHat软件包管理工具,类似windows里面的setup.exe是Linux这系列操作系统里面的打包安装工具,它虽然是RedHat的标志,但理念是通用的。

RPM包的名称格式

Apache-1.3.23-11.i386.rpm

\- “apache” 软件名称

\- “1.3.23-11”软件的版本号,主版本和此版本

\- “i386”是软件所运行的硬件平台,Intel 32位处理器的统称

\- “rpm”文件扩展名,代表RPM包



| 命令                        | 选项                                                         | 功能                            | 经验技巧                                                     | 示例                                                         |
| --------------------------- | ------------------------------------------------------------ | ------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| rpm -qa                     |                                                              | **查询**所安装的所有 rpm 软件包 | 由于软件包比较多,一般都会采取过滤。rpm -qa \| grep rpm软件包 | (1)查询firefox软件安装情况[root@hadoop101 Packages]# rpm -qa \|grep firefox |
| rpm -e [--nodeps] RPM软件包 | -e:卸载软件包--nodeps:卸载软件时,不检查依赖。这样的话,那些使用该软件包的软件在此之后可能就不能正常工作了。 | **卸载**命令(rpm -e)            |                                                              | (1)卸载firefox软件[root@hadoop101 Packages]# rpm -e firefox  |
| rpm -ivh RPM 包全名         | -i :install,安装-v :--verbose,显示详细信息-h: --hash,进度条--nodeps: 安装前不检查依赖 | **安装**命令(rpm -ivh)          |                                                              | (1)安装firefox软件[root@hadoop101 Packages]# pwd/run/media/root/CentOS 7 x86_64/Packages[root@hadoop101 Packages]# rpm -ivh firefox-45.0.1-1.el6.centos.x86_64.rpm |

#### **YUM（在线）**

YUM(全称为 Yellow dog Updater, Modified)是一个在 Fedora 和 RedHat 以及 CentOS中的 Shell 前端软件包管理器。基于 RPM 包管理,能够从指定的服务器自动下载 RPM 包并且安装,可以自动处理依赖性关系,并且一次安装所有依赖的软件包,无须繁琐地一次次下载、安装



1)基本语法

**yum [选项] [参数]**

2)**选项**说明

-y :对所有提问都回答“yes”

3)**参数**说明

参数   功能

install 安装 rpm 软件包

update 更新 rpm 软件包

check-update 检查是否有可用的更新 rpm 软件包

remove 删除指定的 rpm 软件包

list 显示软件包信息

clean 清理 yum 过期的缓存

deplist 显示 yum 软件包的所有依赖关系

4)案例**实操**

(1)采用 yum 方式安装 firefox

[root@hadoop101 ~]#yum -y install firefox



##### **修改网络 YUM 源**

默认的系统 YUM 源,需要连接国外 apache 网站,网速比较慢,可以修改关联的网络YUM 源为国内镜像的网站,比如网易 163,aliyun 等

1)安装 wget, wget 用来从指定的 URL 下载文件

[root@hadoop101 ~] yum install wget

2)在/etc/yum.repos.d/目录下,备份默认的 repos 文件,

[root@hadoop101 yum.repos.d] pwd

/etc/yum.repos.d

[root@hadoop101 yum.repos.d] cp CentOS-Base.repo CentOS-Base.repo.backup

3)下载网易 163 或者是 aliyun 的 repos 文件,任选其一,如图 8-2

[root@hadoop101 yum.repos.d] wget

http://mirrors.aliyun.com/repo/Centos-7.repo //阿里云

[root@hadoop101 yum.repos.d] wget

http://mirrors.163.com/.help/CentOS7-Base-163.repo //网易 163

4)使用下载好的 repos 文件替换默认的 repos 文件

例如:用 CentOS7-Base-163.repo 替换 CentOS-Base.repo

[root@hadoop101 yum.repos.d]# mv CentOS7-Base-163.repo CentOS-Base.repo

5)清理旧缓存数据,缓存新数据

[root@hadoop101 yum.repos.d]#yum clean all

[root@hadoop101 yum.repos.d]#yum makecache

yum makecache 就是把服务器的包信息下载到本地电脑缓存起来

6)测试

[root@hadoop101 yum.repos.d]# yum list | grep firefox

[root@hadoop101 ~]#yum -y install firefox