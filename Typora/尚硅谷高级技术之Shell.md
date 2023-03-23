## 第 **1** 章 **Shell** 概 述

**1**） **Linux** 提 供 的 **Shell** 解 析 器 有

```shell
[atguigu@hadoop101 ~]$ cat /etc/shells /bin/sh

/bin/bash

/usr/bin/sh

/usr/bin/bash

/bin/tcsh

/bin/csh
```

**2**） **bash** 和 **sh** 的 关 系

```
[atguigu@hadoop101 bin]$ ll | grep bash

-rwxr-xr-x. 1 root root 941880 5 月 11 2016 bash lrwxrwxrwx. 1 root root 4 5 月 27 2017 sh -> bash
```

**3**） **Centos** 默 认 的 解 析 器 是 **bash**

```
[atguigu@hadoop101 bin]$ echo $SHELL

/bin/bash
```

## 第 **2** 章 **Shell** 脚 本 入 门

###  1. 脚 本 格 式

**脚 本 以 #!/bin/bash 开 头 （ 指 定 解 析 器 ）**

- 1） 需 求 ： 创 建 一 个 Shell 脚 本 ， 输 出 helloworld
- 2） 案 例 实 操 ：

```
[atguigu@hadoop101 shells]$ touch helloworld.sh 

[atguigu@hadoop101 shells]$ vim helloworld.sh

在helloworld.sh 中 输 入 如 下 内 容

 #!/bin/bash

echo "helloworld"
```



###  2. 脚 本 的 常 用 执 行 方 式

**第 一 种 ： 采 用 bash 或 sh+脚 本 的 相 对 路 径 或 绝 对 路 径 （ 不 用 赋 予 脚 本 +x 权 限 ） sh+脚 本 的 相 对 路 径**

```
[atguigu@hadoop101 shells]$ sh ./helloworld.sh 

Helloworld
```

sh+脚 本 的 绝 对 路 径

```
[atguigu@hadoop101 shells]$ sh /home/atguigu/shells/helloworld.sh 

helloworld
```

bash+脚 本 的 相 对 路 径

```
[atguigu@hadoop101 shells]$ bash ./helloworld.sh 

Helloworld
```

bash+脚 本 的 绝 对 路 径

```
[atguigu@hadoop101 shells]$ bash /home/atguigu/shells/helloworld.sh 

Helloworld
```

**第 二 种 ： 采 用 输 入 脚 本 的 绝 对 路 径 或 相 对 路 径 执 行 脚 本 （ 必 须 具 有 可 执 行 权 限 +x）**

- 首 先 要 赋 予 helloworld.sh 脚 本 的 +x 权 限

```
[atguigu@hadoop101 shells]$ chmod +x helloworld.sh
```



- 执 行 脚 本 相 对 路 径

```
[atguigu@hadoop101 shells]$ ./helloworld.sh 

Helloworld
```

- 绝 对 路 径


```
[atguigu@hadoop101 shells]$ /home/atguigu/shells/helloworld.sh 

Helloworld
```

**注 意 ： 第 一 种 执 行 方 法 ， 本 质 是 bash 解 析 器 帮 你 执 行 脚 本 ， 所 以 脚 本 本 身 不 需 要 执 行**

**权 限 。 第 二 种 执 行 方 法 ， 本 质 是 脚 本 需 要 自 己 执 行 ， 所 以 需 要 执 行 权 限 。**

【 了 解 】 第 三 种 ： 在 脚 本 的 路 径 前 加 上 “ .” 或 者 source

- 有 以 下 脚 本

```
[atguigu@hadoop101 shells]$ cat test.sh #!/bin/bash

A=5

echo $A
```



- 分 别 使 用 sh， bash， ./ 和 . 的 方 式 来 执 行 ， 结 果 如 下 ：

```
[atguigu@hadoop101 shells]$ bash test.sh
[atguigu@hadoop101 shells]$ echo $A

[atguigu@hadoop101 shells]$ sh test.sh 
[atguigu@hadoop101 shells]$ echo $A

[atguigu@hadoop101 shells]$ ./test.sh 
[atguigu@hadoop101 shells]$ echo $A

[atguigu@hadoop101 shells]$ . test.sh
[atguigu@hadoop101 shells]$ echo $A 

5
```

原 因 ：

前 两 种 方 式 都 是 在 当 前 shell 中 打 开 一 个 子 shell 来 执 行 脚 本 内 容 ，当 脚 本 内 容 结 束 ，则 子 shell 关 闭 ， 回 到 父 shell 中 。

第 三 种 ， 也 就 是 使 用 在 脚 本 路 径 前 加 “ .” 或 者 source 的 方 式 ，可 以 使 脚 本 内 容 在 当 前 shell 里 执 行 ，而 无 需 打 开 子 shell！这 也 是 为 什 么 我 们 每 次 要 修 改 完 /etc/profile 文 件 以 后 ，需 要 source 一 下 的 原 因 。

开 子 shell 与 不 开 子 shell 的 区 别 就 在 于 ， 环 境 变 量 的 继 承 关 系 ， 如 在 子 shell 中 设 置 的 当 前 变 量 ， 父 shell 是 不 可 见 的 。

## 第 **3** 章 变 量

### 1. 系统预定义变量

**1**） 常 用 系 统 变 量

$HOME、 $PWD、 $SHELL、 $USER 等 

**2**） 案 例 实 操

- 1） 查 看 系 统 变 量 的 值

```
[atguigu@hadoop101 shells]$ echo $HOME 

 /home/atguigu
```

- 2） 显 示 当 前 Shell 中 所 有 变 量 ： set

```
[atguigu@hadoop101 shells]$ set

BASH=/bin/bash

BASH_ALIASES=()

BASH_ARGC=()

BASH_ARGV=()
```

### 2. 自 定 义 变 量

**1**） 基 本 语 法

- 1） 定 义 变 量 ： 变 量 名 =变 量 值 ， 注 意 ， **=号 前 后 不 能 有 空 格**
- 2） 撤 销 变 量 ： unset 变 量 名
- 3） 声 明 静 态 变 量 ： readonly 变 量 ， 注 意 ： 不 能 unset

**2**） 变 量 定 义 规 则

- 1） 变 量 名 称 可 以 由 字 母 、 数 字 和 下 划 线 组 成 ， 但 是 不 能 以 数 字 开 头 ,环 境 变 量 名 建 议 大 写。

- 2） 等 号 两 侧 不 能 有 空 格
- 3） 在 bash 中 ， **变 量 默 认 类 型 都 是 字 符 串 类 型 ， 无 法 直 接 进 行 数 值 运 算** 。
- 4） 变 量 的 值 如 果 有 空 格 ， 需 要 使 用 双 引 号 或 单 引 号 括 起 来 。

**3**） 案 例 实 操

- 1） 定 义 变 量 A

```
[atguigu@hadoop101 shells]$ A=5 

[atguigu@hadoop101 shells]$ echo $A 

5
```



- 2） 给 变 量 A 重 新 赋 值

```
[atguigu@hadoop101 shells]$ A=8 

[atguigu@hadoop101 shells]$ echo $A 

8
```



- 3） 撤 销 变 量 A

```
[atguigu@hadoop101 shells]$ unset A 

[atguigu@hadoop101 shells]$ echo $A
```



- 4） 声 明 静 态 的 变 量 B=2， 不 能 unset

```
atguigu@hadoop101 shells]$ readonly B=2 

[atguigu@hadoop101 shells]$ echo $B

2

[atguigu@hadoop101 shells]$ B=9

-bash: B: readonly variable
```



- 5） 在 bash 中 ， 变 量 默 认 类 型 都 是 字 符 串 类 型 ， 无 法 直 接 进 行 数 值 运 算

```
[atguigu@hadoop102 ~]$ C=1+2

[atguigu@hadoop102 ~]$ echo $C

1+2
```



- 6） 变 量 的 值 如 果 有 空 格 ， 需 要 使 用 双 引 号 或 单 引 号 括 起 来

```
[atguigu@hadoop102 ~]$ D=I love banzhang 

-bash: world: command not found

[atguigu@hadoop102 ~]$ D="I love banzhang" 

[atguigu@hadoop102 ~]$ echo $D

I love banzhang
```



- 7） 可 把 变 量 提 升 为 全 局 环 境 变 量 ， 可 供 其 他 Shell 程 序 使 用

```
export 变 量 名

[atguigu@hadoop101 shells]$ vim helloworld.sh
```

​        在 helloworld.sh 文 件 中 增 加 echo $B

```
#!/bin/bash
 
echo "helloworld" 
echo $B

[atguigu@hadoop101 shells]$ ./helloworld.sh Helloworld
```

​	发 现 并 没 有 打 印 输 出 变 量 B 的 值 。

```
[atguigu@hadoop101 shells]$ export B 

[atguigu@hadoop101 shells]$ ./helloworld.sh

 helloworld

2
```

### 3. 特 殊 变 量

#### **$n**（某个参数）

**1**） 基 本 语 法

$n （ 功 能 描 述 ： n 为 数 字 ， $0 代 表 该 脚 本 名 称 ， $1-$9 代 表 第 一 到 第 九 个 参 数 ， 十 以 上 的 参 数 ， 十 以 上 的 参 数 需 要 用 大 括 号 包 含 ， 如 ${10}）

**2**） 案 例 实 操

```
[atguigu@hadoop101 shells]$ touch parameter.sh 
[atguigu@hadoop101 shells]$ vim parameter.sh #!/bin/bash

echo '==========$n=========='

echo $0

echo $1

echo $2


[atguigu@hadoop101 shells]$ chmod 777 parameter.sh [atguigu@hadoop101 shells]$ ./parameter.sh cls xz ==========$n==========

./parameter.sh

cls

xz
```

#### **$#**（参数个数）

**1**） 基 本 语 法

$# （ 功 能 描 述 ： 获 取 所 有 输 入 参 数 个 数 ， 常 用 于 循 环 ,判 断 参 数 的 个 数 是 否 正 确 以 及 加 强 脚 本 的 健 壮 性 ） 。

**2**） 案 例 实 操

```
[atguigu@hadoop101 shells]$ vim parameter.sh #!/bin/bash

echo '==========$n=========='

echo $0

echo $1

echo $2

echo '==========$#=========='

echo $#

[atguigu@hadoop101 shells]$ chmod 777 parameter.sh [atguigu@hadoop101 shells]$ ./parameter.sh cls xz ==========$n==========

./parameter.sh

cls

xz

 ==========$#========== 

2
```



#### **$\***、 **$@ **  (所有参数)

**1**） 基 本 语 法

$\* （ 功 能 描 述 ： 这 个 变 量 代 表 命 令 行 中 所 有 的 参 数 ， $\*把 所 有 的 参 数 看 成 一 个 整 体 ）

$@ （ 功 能 描 述 ：这 个 变 量 也 代 表 命 令 行 中 所 有 的 参 数 ，不 过 $@把 每 个 参 数 区 分 对 待 ）

 **2**） 案 例 实 操

```
[atguigu@hadoop101 shells]$ vim parameter.sh #!/bin/bash

echo '==========$n=========='

echo $0

echo $1

echo $2

echo '==========$#=========='

echo $#

echo '==========$\*=========='

echo $\*

echo '==========$@=========='

echo $@

[atguigu@hadoop101 shells]$ ./parameter.sh a b c d e f g ==========$n==========

./parameter.sh

a

b

==========$#==========

7

==========$\*==========

a b c d e f g

==========$@==========

a b c d e f g
```



#### **$?**（命令执行状态）

**1**） 基 本 语 法

$？ （ 功 能 描 述 ：最 后 一 次 执 行 的 命 令 的 返 回 状 态 。如 果 这 个 变 量 的 值 为 0，证 明 上 一 个 命 令 正 确 执 行 ；如 果 这 个 变 量 的 值 为 非 0（ 具 体 是 哪 个 数 ，由 命 令 自 己 来 决 定 ），则 证 明 上 一 个 命 令 执 行 不 正 确 了 。 ）

**2**） 案 例 实 操

判 断 helloworld.sh 脚 本 是 否 正 确 执 行

```
[atguigu@hadoop101 shells]$ ./helloworld.sh

 hello world

[atguigu@hadoop101 shells]$ echo $?

0
```

### 4. $ 的用法

#### 引用变量

##### $ 符号直接引用

引用变量时，使用 $ 符号直接来进行引用，以及包括循环变量；

```
[root@localhost ~]# x=1024
[root@localhost ~]# echo $x
1024
```

##### 双引号 " 将括起来

利用双引号 " 将括起来的字符串支持变量插值。

```
[root@localhost ~]# x=1024
[root@localhost ~]# echo "x = $x"
x = 1024
```

##### 使用 ${ } 作为单词边界。

```
[root@localhost ~]# x=1024
[root@localhost ~]# echo "x = ${x}xy"
x = 1024xy
```



##### 使用 ${#} 获取变量字符串长度。

```
[root@localhost etc]# s=helloworld
[root@localhost etc]# echo "s.length = ${#s}"
s.length = 10
```

#### 引用脚本或函数参数

基于引用脚本的方式，1 表示 Shell 脚本文件名，n 从 2 开始表示第 n 个参数，第 2 个参数是 $2；

即为特殊变量

#### $() 执行并获取命令输出

使用 $() 执行并获取命令输出赋值给变量，等于双引号的功能。

```
[root@localhost ~]# echo `date`
2016年 06月 05日 星期日 12:39:08 CST
[root@localhost ~]# echo $(date)
2016年 06月 05日 星期日 12:39:34 CST
```



#### $[]表达式求值

即为运算符

使用 [ ] 对 表 达 式 进 行 求 值 ， 与 命 令 e x p r 不 同 的 是 ： [ ] 对表达式进行求值，与命令 expr 不同的是：[]对表达式进行求值，与命令expr不同的是：[ ] 用于插值，则 expr 用于将值进行输出。

```
[root@localhost ~]# echo $[1024 + 2048]
3072
[root@localhost ~]# expr 1024 + 2048
3072
[root@localhost ~]# a=1024
[root@localhost ~]# b=2048
[root@localhost ~]# echo $[ a + b ]
3072
```



#### $$获取当前进程 ID

使用 $$ 来进行获取当前进程的 ID 号。

```
[root@localhost ~]# echo $$
55580
```



####  $!后台运行的最后一个进程 ID

使用 $! 来进行获取后台运行的最后一个进程 ID。

在命令结尾使用 & 可创建后台进程。

执行命令 kill $! 然后在输入 echo $! 将终止该 ping.sh 脚本。

```
[root@localhost ~]# tail -f /root/ping.sh &
[2] 55848
[root@localhost ~]# echo $!
55848
[root@localhost ~]# kill $!
[root@localhost ~]# echo $!
55848
[2]+ 已终止 tail -f /root/ping.sh
```



#### $- 获取 Shell 选项

使用 $- 来进行获取当前 Shell 的选项。

```
[root@localhost ~]# echo $-
himBH
```



## 第 **4** 章 运 算 符

**1**） 基 本 语 法

“$((运 算 式 ))” 或 “$[运 算 式 ]”

**2**） 案 例 实 操 ：

​		计 算 （ 2+3） \* 4 的 值

```
[atguigu@hadoop101 shells]# S=$[(2+3)*4] 

[atguigu@hadoop101 shells]# echo $S
```

## 第 **5** 章 条 件 判 断

###  基 本 语 法

- 1） test condition
- 2） [ condition ]（ **注 意 condition 前 后 要 有 空 格** ）

**注 意 ： 条 件 非 空 即 为 true， [ atguigu ]返 回 true， [ ] 返 回 false。 2） 常 用 判 断 条 件**

### 1. 两 个 整 数 之 间 比 较

-eq 等 于 （ equal）                      -ne 不 等 于 （ not equal）

-lt 小 于 （ less than）                 -le 小 于 等 于 （ less equal）

-gt 大 于 （ greater than）           -ge 大 于 等 于 （ greater equal）

注 ： 如 果 是 字 符 串 之 间 的 比 较 ， 用 等 号 “ =” 判 断 相 等 ； 用 “ !=” 判 断 不 等 。

### 2.  按 照 文 件 权 限 进 行 判 断

-r 有 读 的 权 限 （ read）

-w 有 写 的 权 限 （ write）

-x 有 执 行 的 权 限 （ execute）

### 3.  按 照 文 件 类 型 进 行 判 断

-e 文 件 存 在 （ existence）

-f 文 件 存 在 并 且 是 一 个 常 规 的 文 件 （ file）

 -d 文 件 存 在 并 且 是 一 个 目 录 （ directory）

### 4. 案 例 实 操

- 1） 23 是 否 大 于 等 于 22

- ```
  [atguigu@hadoop101 shells]$ [ 23 -ge 22 ] 
  
  [atguigu@hadoop101 shells]$ echo $?
  
  0
  
  ```

  2） helloworld.sh 是 否 具 有 写 权 限

```
[atguigu@hadoop101 shells]$ [ -w helloworld.sh ] 
[atguigu@hadoop101 shells]$ echo $?
0
```



- 3） /home/atguigu/cls.txt 目 录 中 的 文 件 是 否 存 在

```
[atguigu@hadoop101 shells]$ [ -e /home/atguigu/cls.txt ] 
[atguigu@hadoop101 shells]$ echo $?

1
```



- 4） 多 条 件 判 断 （ && 表 示 前 一 条 命 令 执 行 成 功 时 ， 才 执 行 后 一 条 命 令 ， || 表 示 上 一

条 命 令 执 行 失 败 后 ， 才 执 行 下 一 条 命 令 ）

```
[atguigu@hadoop101 ~]$ [ atguigu ] && echo OK || echo notOK

 OK

[atguigu@hadoop101 shells]$ [ ] && echo OK || echo notOK 

notOK
```

## 第 **6** 章 流 程 控 制 （ 重 点 ）

### 1. if判 断

**1**） 基 本 语 法

- 1） 单 分 支

```
if [ 条 件 判 断 式 ];then
程 序
fi

或 者

if [ 条 件 判 断 式 ] 
then
	程 序
fi
```

- 2） 多 分 支

```
if [ 条 件 判 断 式 ] 
then
	程 序
elif [ 条 件 判 断 式 ] 
then
	程 序 
else
	程 序 
fi
```

注 意 事 项 ：

- **[ 条 件 判 断 式 ]， 中 括 号 和 条 件 判 断 式 之 间 必 须 有 空 格**
- **if 后 要 有 空 格**

**2**） 案 例 实 操

输 入 一 个 数 字 ，如 果 是 1，则 输 出 banzhang zhen shuai，如 果 是 2，则 输 出 cls zhen mei， 如 果 是 其 它 ， 什 么 也 不 输 出 。

```
[atguigu@hadoop101 shells]$ touch if.sh 

[atguigu@hadoop101 shells]$ vim if.sh

#!/bin/bash

if [ $1 -eq 1 ]
then
	echo "banzhang zhen shuai" 
elif [ $1 -eq 2 ]
then
​	echo "cls zhen mei"
fi

[atguigu@hadoop101 shells]$ chmod 777 if.sh

[atguigu@hadoop101 shells]$ ./if.sh 1 

banzhang zhen shuai
```



### 2. case语 句

**1**） 基 本 语 法

```
case $变 量 名 in
"值1"）
	如 果 变 量 的 值 等 于 值1， 则 执 行 程 序1
;; 
"值2"）
	如 果 变 量 的 值 等 于 值2， 则 执 行 程 序2
;;
	…省 略 其 他 分 支…
 *）
	如 果 变 量 的 值 都 不 是 以 上 的 值 ， 则 执 行 此 程 序
;; 
esac
```

**注 意 事 项** ：

- 1） case 行 尾 必 须 为 单 词 “ in” ， 每 一 个 模 式 匹 配 必 须 以 右 括 号 “ ） ” 结 束 。
- 2） 双 分 号 “ **;;**” 表 示 命 令 序 列 结 束 ， 相 当 于 java 中 的 break。
- 3） 最 后 的 “ \*） ” 表 示 默 认 模 式 ， 相 当 于 java 中 的 default。

**2**） 案 例 实 操

输 入 一 个 数 字 ，如 果 是 1，则 输 出 banzhang，如 果 是 2，则 输 出 cls，如 果 是 其 它 ，输 出 renyao。

```
[atguigu@hadoop101 shells]$ touch case.sh 

[atguigu@hadoop101 shells]$ vim case.sh

!/bin/bash

case $1 in
"1")
	echo "banzhang"
;;
"2")
	echo "cls"
;;
*)
	echo "renyao"
;; 
esac
[atguigu@hadoop101 shells]$ chmod 777 case.sh
[atguigu@hadoop101 shells]$ ./case.sh 1
1
```

### 3. for循 环

**1**） 基 本 语 法 **1**

```
for (( 初 始 值;循 环 控 制 条 件;变 量 变 化 )) 
do	
	程 序
done
```

**2**） 案 例 实 操

从 1 加 到 100

```
[atguigu@hadoop101 shells]$ touch for1.sh 

[atguigu@hadoop101 shells]$ vim for1.sh

#!/bin/bash

sum=0 
for((i=0;i<=100;i++)) 
do
	sum=$[$sum+$i] 
done
echo $sum
[atguigu@hadoop101 shells]$ chmod 777 for1.sh
[atguigu@hadoop101 shells]$ ./for1.sh
5050
```

**3**） 基 本 语 法 **2**

```
for 变 量 in 值1 值2 值3… 
do
	程 序
done
```

**4**） 案 例 实 操

- 1） 打 印 所 有 输 入 参 数

```
[atguigu@hadoop101 shells]$ touch for2.sh 

[atguigu@hadoop101 shells]$ vim for2.sh

#!/bin/bash  
#打 印 数 字

for i in cls mly wls
do
	echo "ban zhang love $i"
done
[atguigu@hadoop101 shells]$ chmod 777 for2.sh 
[atguigu@hadoop101 shells]$ ./for2.sh
ban zhang love cls
ban zhang love mly
ban zhang love wls
```



#### 比 较 $\*和 $@区 别

$\*和 $@都 表 示 传 递 给 函 数 或 脚 本 的 所 有 参 数 ， 不 被 双 引 号 “”包 含 时 ， 都 以 $1 $2 …$n 的 形 式 输 出 所 有 参 数 。

```
[atguigu@hadoop101 shells]$ touch for3.sh 

[atguigu@hadoop101 shells]$ vim for3.sh

#!/bin/bash

echo '=============$\*=============' 

for i in $*
do
	echo "ban zhang love $i"
done
echo '=============$@============='
for j in $@
do
	echo "ban zhang love $j"
done
[atguigu@hadoop101 shells]$ chmod 777 for3.sh 
[atguigu@hadoop101 shells]$ ./for3.sh cls mly wls 
=============$\*=============
banzhang love cls
banzhang love mly
banzhang love wls
=============$@=============
banzhang love cls
banzhang love mly
banzhang love wls
```

当 它 们 被 双 引 号 “”包 含 时 ， $\*会 将 所 有 的 参 数 作 为 一 个 整 体 ， 以 “$1 $2 …$n”的 形 式 输 出 所 有 参 数 ； $@会 将 各 个 参 数 分 开 ， 以 “$1” “$2”…“$n”的 形 式 输 出 所 有 参 数 。

```
[atguigu@hadoop101 shells]$ vim for4.sh

#!/bin/bash
echo '=============$\*============='
for i in "$*"
#$\*中 的 所 有 参 数 看 成 是 一 个 整 体 ， 所 以 这 个for 循 环 只 会 循 环 一 次 do
	echo "ban zhang love $i"
done
echo '=============$@============='
for j in "$@"
#$@中 的 每 个 参 数 都 看 成 是 独 立 的 ， 所 以“$@”中 有 几 个 参 数 ， 就 会 循 环 几 次 do
	echo "ban zhang love $j"
done
[atguigu@hadoop101 shells]$ chmod 777 for4.sh 
[atguigu@hadoop101 shells]$ ./for4.sh cls mly wls
=============$\*=============
banzhang love cls mly wls 
=============$@=============
banzhang love cls
banzhang love mly
banzhang love wls
```



### 4. **while** 循 环

**1**） 基 本 语 法

```
while [ 条 件 判 断 式 ] 
do
	程 序
done
```

```
while read line

do

       …

done < file

read通过输入重定向，把file的第一行所有的内容赋值给变量line，循环体内的命令一般包含对变量line的处理；然后循环处理file的第二行、第三行。。。一直到file的最后一行。

还记得while根据其后的命令退出状态来判断是否执行循环体吗？

是的，read命令也有退出状态，当它从文件file中读到内容时，退出状态为0，循环继续进行；

当read从文件中读完最后一行后，下次便没有内容可读了，此时read的退出状态为非0，所以循环才会退出。
```

**2**） 案 例 实 操

从 1 加 到 100

```
[atguigu@hadoop101 shells]$ touch while.sh

[atguigu@hadoop101 shells]$ vim while.sh

#!/bin/bash
sum=0
i=1
while [ $i -le 100 ] 
do
	sum=$[$sum+$i] 
	i=$[$i+1]
done 
echo $sum
[atguigu@hadoop101 shells]$ chmod 777 while.sh 
[atguigu@hadoop101 shells]$ ./while.sh
5050
```

## 第 **7** 章 **read** 读 取 控 制 台 输 入

**1**） 基 本 语 法

- ```
  read (选 项 ) (参 数 )
  
  - 选 项 ：
  
    ​	-p： 指 定 读 取 值 时 的 提 示 符 ；
  
    ​	-t： 指 定 读 取 值 时 等 待 的 时 间 （ 秒 ） 如 果 -t 不 加 表 示 一 直 等 待
  
  - 参 数
  
    变 量 ： 指 定 读 取 值 的 变 量 名
  ```

  

**2**） 案 例 实 操

提 示 7 秒 内 ， 读 取 控 制 台 输 入 的 名 称

```
[atguigu@hadoop101 shells]$ touch read.sh 

[atguigu@hadoop101 shells]$ vim read.sh

#!/bin/bash

read -t 7 -p "Enter your name in 7 seconds :" NN 

echo $NN

[atguigu@hadoop101 shells]$ ./read.sh 

Enter your name in 7 seconds : atguigu 

atguigu
```

## 第 **8** 章 函 数

### 1. 系 统 函 数

#### **basename**(截取文件名称)

**1**） 基 本 语 法

basename [string / pathname] [suffix] （ 功 能 描 述 ： basename 命 令 会 删 掉 所 有 的 前 缀 包 括 最 后 一 个 （ ‘/’） 字 符 ， 然 后 将 字 符 串 显 示 出 来 。

basename 可 以 理 解 为 取 路 径 里 的 文 件 名 称

选 项 ：

suffix 为 后 缀 ，如 果 suffix 被 指 定 了 ，basename 会 将 pathname 或 string 中 的 suffix 去 掉 。

 **2**） 案 例 实 操

截 取 该 /home/atguigu/banzhang.txt 路 径 的 文 件 名 称 。

```
[atguigu@hadoop101 shells]$ basename /home/atguigu/banzhang.txt banzhang.txt

[atguigu@hadoop101 shells]$ basename /home/atguigu/banzhang.txt .txt 

banzhang
```



#### **dirname**（截取文件绝对路径）

**1**） 基 本 语 法

dirname 文 件 绝 对 路 径 （ 功 能 描 述 ：从 给 定 的 包 含 绝 对 路 径 的 文 件 名 中 去 除 文 件 名非 目 录 的 部 分 ） ， 然 后 返 回 剩 下 的 路 径 （ 目 录 的 部 分 ） ）,截取最后一个斜杠前面部分

dirname 可 以 理 解 为 取 文 件 路 径 的 绝 对 路 径 名 称

**2**） 案 例 实 操

获 取 banzhang.txt 文 件 的 路 径 。

```
[atguigu@hadoop101 ~]$ dirname /home/atguigu/banzhang.txt 

/home/atguigu
```

### 2. 自 定 义 函 数

**1**） 基 本 语 法

```
[ function ] funname[()] {

	Action;

	[return int;]

}


```

**2**） 经 验 技 巧

- 1）必 须 在 调 用 函 数 地 方 之 前 ，**先 声 明 函 数** ，shell 脚 本 是 逐 行 运 行 。不 会 像 其 它 语 言 一

样 先 编 译 。

- 2） 函 数 返 回 值 ， 只 能 通 过 $?系 统 变 量 获 得 ， 可 以 显 示 加 ： return 返 回 ， 如 果 不 加 ， 将

以 最 后 一 条 命 令 运 行 结 果 ， 作 为 返 回 值 。 return 后 跟 数 值 n(0-255)

**3**） 案 例 实 操

计 算 两 个 输 入 参 数 的 和 。

```
[atguigu@hadoop101 shells]$ touch fun.sh 
[atguigu@hadoop101 shells]$ vim fun.sh

#!/bin/bash
function sum() {
	s=0
	s=$[$1+$2] 
	echo "$s"

}

read -p "Please input the number1: " n1; 
read -p "Please input the number2: " n2; 
sum $n1 $n2;

[atguigu@hadoop101 shells]$ chmod 777 fun.sh [atguigu@hadoop101 shells]$ ./fun.sh

Please input the number1: 2

Please input the number2: 5

7
```

## 第 **9** 章 正 则 表 达 式 入 门

正 则 表 达 式 使 用 单 个 字 符 串 来 描 述 、匹 配 一 系 列 符 合 某 个 语 法 规 则 的 字 符 串 。在 很 多 文 本 编 辑 器 里 ，正 则 表 达 式 通 常 被 用 来 检 索 、替 换 那 些 符 合 某 个 模 式 的 文 本 。在 Linux 中 ，grep， sed， awk 等 文 本 处 理 工 具 都 支 持 通 过 正 则 表 达 式 进 行 模 式 匹 配 。

### 1. 常 规 匹 配

一 串 不 包 含 特 殊 字 符 的 正 则 表 达 式 匹 配 它 自 己 ， 例 如 ：

```
[atguigu@hadoop101 shells]$ cat /etc/passwd | grep atguigu
```

就 会 匹 配 所 有 包 含 atguigu 的 行 。

### 2. 常 用 特 殊 字 符

#### **1**） 特 殊 字 符 ： **^**

^ 匹 配 一 行 的 开 头 ， 例 如 ：

[atguigu@hadoop101 shells]$ cat /etc/passwd | grep ^a

会 匹 配 出 所 有 以 a 开 头 的 行

#### **2**） 特 殊 字 符 ： **$**

$ 匹 配 一 行 的 结 束 ， 例 如

[atguigu@hadoop101 shells]$ cat /etc/passwd | grep t$

会 匹 配 出 所 有 以 t 结 尾 的 行 思 考 ： **^$** 匹 配 什 么 ？

#### **3**） 特 殊 字 符 ： **.**

. 匹 配 一 个 任 意 的 字 符 ， 例 如

[atguigu@hadoop101 shells]$ cat /etc/passwd | grep r..t

会 匹 配 包 含 rabt,rbbt,rxdt,root 等 的 所 有 行

#### **4**） 特 殊 字 符 ： **\***

\* 不 单 独 使 用 ， 他 和 上 一 个 字 符 连 用 ， 表 示 匹 配 上 一 个 字 符 0 次 或 多 次 ， 例 如

[atguigu@hadoop101 shells]$ cat /etc/passwd | grep ro\*t

会 匹 配 rt, rot, root, rooot, roooot 等 所 有 行 思 考 ： **.\*** 匹 配 什 么 ？

#### **5**） 字 符 区 间 （ 中 括 号 ） ： **[ ]**

[ ] 表 示 匹 配 某 个 范 围 内 的 一 个 字 符 ， 例 如 [6,8]------匹 配 6 或 者 8

[0-9]------匹 配 一 个 0-9 的 数 字 [0-9]\*------匹 配 任 意 长 度 的 数 字 字 符 串 [a-z]------匹 配 一 个 a-z 之 间 的 字 符

[a-z]\* ------匹 配 任 意 长 度 的 字 母 字 符 串 [a-c, e-f]-匹 配 a-c 或 者 e-f 之 间 的 任 意 字 符

[atguigu@hadoop101 shells]$ cat /etc/passwd | grep r[a,b,c]\*t

会 匹 配 rt,rat, rbt, rabt, rbact,rabccbaaacbt 等 等 所 有 行

#### **6**） 特 殊 字 符 ： \

\ 表 示 转 义 ，并 不 会 单 独 使 用 。由 于 所 有 特 殊 字 符 都 有 其 特 定 匹 配 模 式 ，当 我 们 想 匹 配 某 一 特 殊 字 符 本 身 时（ 例 如 ，我 想 找 出 所 有 包 含 '$' 的 行 ），就 会 碰 到 困 难 。此 时 我 们 就 要 将 转 义 字 符 和 特 殊 字 符 连 用 ， 来 表 示 特 殊 字 符 本 身 ， 例 如

[atguigu@hadoop101 shells]$ cat /etc/passwd | grep ‘a\$b’

就 会 匹 配 所 有 包 含 a$b 的 行 。 注 意 需 要 使 用 单 引 号 将 表 达 式 引 起 来 。

## 第 **10** 章 文 本 处 理 工 具

### **cut**（剪切列）

cut 的 工 作 就 是 “剪 ”， 具 体 的 说 就 是 在 文 件 中 负 责 剪 切 数 据 用 的 。 cut 命 令 从 文 件 的 每 一 行 剪 切 字 节 、 字 符 和 字 段 并 将 这 些 字 节 、 字 符 和 字 段 输 出 。

**1**） 基 本 用 法

```
cut [选 项 参 数 ] filename

说 明 ： 默 认 分 隔 符 是 制 表 符
```

**2**） 选 项 参 数 说 明



|选 项 参 数|功 能|
| - | - |
|-f|列 号 ， 提 取 第 几 列    -f  3- 表示提取第三列后面所有内容|
|-d|分 隔 符 ， 按 照 指 定 分 隔 符 分 割 列 ， 默 认 是 制 表 符 “ \t”|
|-c|按 字 符 进 行 切 割 后 加 加 n 表 示 取 第 几 列 比 如 -c 1|
**3**） 案 例 实 操

- 1） 数 据 准 备

```
[atguigu@hadoop101 shells]$ touch cut.txt 
[atguigu@hadoop101 shells]$ vim cut.txt dong shen

guan zhen

wo wo

lai lai

le le
```



- 2） 切 割 cut.txt 第 一 列

```
[atguigu@hadoop101 shells]$ cut -d " " -f 1 cut.txt dong

guan

wo

lai

le
```



- 3） 切 割 cut.txt 第 二 、 三 列

```
[atguigu@hadoop101 shells]$ cut -d " " -f 2,3 cut.txt shen

zhen

wo

lai

le
```



- 4） 在 cut.txt 文 件 中 切 割 出 guan

```
[atguigu@hadoop101 shells]$ cat cut.txt |grep guan | cut -d " " -f 1 

guan
```



- 5） 选 取 系 统 PATH 变 量 值 ， 第 2 个 “ ： ” 开 始 后 的 所 有 路 径 ：

```
[atguigu@hadoop101 shells]$ echo $PATH /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/atguigu/.local/bin:/ home/atguigu/bin

[atguigu@hadoop101 shells]$ echo $PATH | cut -d ":" -f 3- /usr/local/sbin:/usr/sbin:/home/atguigu/.local/bin:/home/atguigu/bin
```

- 6） 切 割 ifconfig 后 打 印 的 IP 地 址

```
[atguigu@hadoop101 shells]$ ifconfig ens33 | grep netmask | cut -d " " -f 10 

192.168.111.101
```

### **awk**(行分析)

一 个 强 大 的 文 本 分 析 工 具 ，把 文 件 逐 行 的 读 入 ，以 空 格 为 默 认 分 隔 符 将 每 行 切 片 ，切 开 的 部 分 再 进 行 分 析 处 理 。

**1**） 基 本 用 法

```
awk [选 项 参 数 ] ‘ /pattern1/{action1} /pattern2/{action2}...’ filename

pattern： 表 示 awk 在 数 据 中 查 找 的 内 容 ， 就 是 匹 配 模 式

action： 在 找 到 匹 配 内 容 时 所 执 行 的 一 系 列 命 令
```

**2**） 选 项 参 数 说 明



|选 项 参 数|功 能|
| - | - |
|-F|指 定 输 入 文 件 分 隔 符|
|-v|赋 值 一 个 用 户 定 义 变 量|
**3**） 案 例 实 操

- 1） 数 据 准 备

```
[atguigu@hadoop101 shells]$ sudo cp /etc/passwd ./ passwd 
数 据 的 含 义

用 户 名:密 码(加 密 过 后 的):用 户id:组id:注 释:用 户 家 目 录:shell 解 析 器
```



- 2） 搜 索 passwd 文 件 以 root 关 键 字 开 头 的 所 有 行 ， 并 输 出 该 行 的 第 7 列 。

```
[atguigu@hadoop101 shells]$ awk -F : '/^root/{print $7}' passwd 

/bin/bash
```

- 3） 搜 索 passwd 文 件 以 root 关 键 字 开 头 的 所 有 行 ， 并 输 出 该 行 的 第 1 列 和 第 7 列 ，

中 间 以 “ ， ” 号 分 割 。

```
[atguigu@hadoop101 shells]$ awk -F : '/^root/{print $1","$7}' passwd 

root,/bin/bash
```

注 意 ： 只 有 匹 配 了 pattern 的 行 才 会 执 行 action。

- 4）只 显 示 /etc/passwd 的 第 一 列 和 第 七 列 ，以 逗 号 分 割 ，且 在 所 有 行 前 面 添 加 列 名 user，

shell 在 最 后 一 行 添 加 "dahaige， /bin/zuishuai"。

```
[atguigu@hadoop101shells]$awk-F:'BEGIN{print"user,shell"}{print$1","$7} END{print "dahaige,/bin/zuishuai"}' passwd

user, shell

root,/bin/bash

bin,/sbin/nologin

atguigu,/bin/bash

dahaige,/bin/zuishuai
```

注 意 ： BEGIN 在 所 有 数 据 读 取 行 之 前 执 行 ； END 在 所 有 数 据 执 行 之 后 执 行 。

- 5） 将 passwd 文 件 中 的 用 户 id 增 加 数 值 1 并 输 出

```
[atguigu@hadoop101 shells]$ awk -v i=1 -F : '{print $3+i}' passwd 1

2

3![](Aspose.Words.af3035cd-dc58-4896-bf1b-6e9e71607f95.010.png)

4


```

**4**） **awk** 的 内 置 变 量



|变 量|说 明|
| - | - |
|FILENAME|文 件 名|
|NR|已 读 的 记 录 数 （ 行 号 ）|
|NF|浏 览 记 录 的 域 的 个 数 （ 切 割 后 ， 列 的 个 数 ）|
**5**） 案 例 实 操

- 1） 统 计 passwd 文 件 名 ， 每 行 的 行 号 ， 每 行 的 列 数

```
[atguigu@hadoop101 shells]$ awk -F : '{print "filename:" FILENAME ",linenum:" NR ",col:"NF}' passwd

filename:passwd,linenum:1,col:7

filename:passwd,linenum:2,col:7

filename:passwd,linenum:3,col:7
```

- 2） 查 询 ifconfig 命 令 输 出 结 果 中 的 空 行 所 在 的 行 号

```
[atguigu@hadoop101 shells]$ ifconfig | awk '/^$/{print NR}' 9

18

26
```



- 3） 切 割 IP

```
[atguigu@hadoop101 shells]$ ifconfig ens33 | awk '/netmask/ {print $2}' 

192.168.6.101
```

## 补充

### typeset(declare)

typeset [-afFgrxilnrtux] [-p] [name[=value] …]，typeset命令是为了与Korn shell兼容而提供的，与内建命令declare相同。

declare [-aAfFgilnrtux] [-p] [name[=value] …]，声明变量并设置属性。如果没有任何参数，则显示所有参数及其对应的值。-p选项，显示每个name变量对应的属性和值。当-p与name一起使用时会忽略除-f和-F之外的其他选项。当只有-p选项没有指定name时，将显示具有附加选项指定的属性的所有变量的属性和值。如果也没有其他附加选项，则显示所有变量的属性和值。

可选的附加选项如下：

-a：表示每个name都是一个索引数组变量。

-A：表示每个name都是一个关联数组变量。

-f：表示每个name都是一个函数名，此选项会打印函数定义。

-F：表示每个name都是一个函数名，此选项不会打印函数定义，只打印函数名和属性。如果使用内建命令shopt启用extdebug，还会显示定义每个name的源文件名和行号。

-g：强制在全局范围内创建或修改变量，即使是在shell函数中执行declare。

-i：变量将被当做整数。当为变量赋值时执行算术运算。

-l：当为变量赋值时，**所有大写字符都转换为小写**。

-n：为name设置namref属性，使其成为对另一个变量的名称引用，另一个变量由name的值value定义。name的所有引用、赋值和属性修改都是对name的值value引用的变量执行的，除非使用或更改-n属性本身。不能将nameref属性应用于数组变量。

-r：使每个name变量为只读的。这些变量后续不能进行修改或取消。

-t：为name设置trace属性，跟踪函数从调用shell继承DEBUG和RETURN类型的trap。trace属性对变量没有特殊意义。

-u：当为变量赋值时，**所有小写字符都转换为大写**。

-x：将每个name导出到后续的命令或子进程，相当于对name执行了export

source 

## 第 **11** 章 综 合 应 用 案 例

### 1. 归档文件

实 际 生 产 应 用 中 ， 往 往 需 要 对 重 要 数 据 进 行 归 档 备 份 。

需 求 ： 实 现 一 个 每 天 对 指 定 目 录 归 档 备 份 的 脚 本 ， 输 入 一 个 目 录 名 称 （ 末 尾 不 带 /） ， 将 目 录 下 所 有 文 件 按 天 归 档 保 存 ，并 将 归 档 日 期 附 加 在 归 档 文 件 名 上 ，放 在 /root/archive 下 。

这 里 用 到 了 归 档 命 令 ： tar

后 面 可 以 加 上 -c 选 项 表 示 归 档 ， 加 上 -z 选 项 表 示 同 时 进 行 压 缩 ， 得 到 的 文 件 后 缀 名 为 .tar.gz。

脚 本 实 现 如 下 ：

```
#!/bin/bash
# 首 先 判 断 输 入 参 数 个 数 是 否 为1
if [ $# -ne 1 ]
then
	echo "参 数 个 数 错 误 ！ 应 该 输 入 一 个 参 数 ， 作 为 归 档 目 录 名" 
	exit
fi

# 从 参 数 中 获 取 目 录 名 称 
if [ -d $1 ]
then
	echo
	else
	echo
	echo "目 录 不 存 在 ！" 
	echo
	exit
fi

DIR_NAME=$(basename $1) 
DIR_PATH=$(cd $(dirname $1); pwd)    # 进入目录执行pwd获取绝对路径


# 获 取 当 前 日 期 
DATE=$(date +%y%m%d)
# 定 义 生 成 的 归 档 文 件 名 称
FILE=archive_${DIR_NAME}_$DATE.tar.gz DEST=/root/archive/$FILE

#开 始 归 档 目 录 文 件
echo "开 始 归 档..."
echo
tar -czf $DEST $DIR\_PATH/$DIR_NAME
if [ $? -eq 0 ]
then
	echo
	echo "归 档 成 功 ！"
	echo "归 档 文 件 为 ：$DEST" 
	echo
else
	echo "归 档 出 现 问 题 ！" 
	echo
fi 
exit
```



### 2. 发 送 消 息

我 们 可 以 利 用 Linux 自 带 的 mesg 和 write 工 具 ， 向 其 它 用 户 发 送 消 息 。

需 求 ：实 现 一 个 向 某 个 用 户 快 速 发 送 消 息 的 脚 本 ，输 入 用 户 名 作 为 第 一 个 参 数 ，后 面 直 接 跟 要 发 送 的 消 息 。脚 本 需 要 检 测 用 户 是 否 登 录 在 系 统 中 、是 否 打 开 消 息 功 能 ，以 及 当 前 发 送 消 息 是 否 为 空 。

脚 本 实 现 如 下 ：

```
#!/bin/bash

login_user=$(who | grep -i -m 1 $1 | awk '{print $1}')

if [ -z $login_user ]
then
	echo "$1 不 在 线 ！" echo "脚 本 退 出.." 
	exit
fi

is_allowed=$(who -T | grep -i -m 1 $1 | awk '{print $2}')

if [ $is_allowed != "+" ] 
then
	echo "$1 没 有 开 启 消 息 功 能" 
	echo "脚 本 退 出.."
exit
fi

if [ -z $2 ]
then
	echo "没 有 消 息 发 出" echo "脚 本 退 出.." 
	exit
fi

whole_msg=$(echo $\* | cut -d " " -f 2- )
user_terminal=$(who | grep -i -m 1 $1 | awk '{print $2}') 
echo $whole_msg | write $login_user $user_terminal
if [ $? != 0 ] then
	echo "发 送 失 败 ！"
else
	echo "发 送 成 功 ！" 
fi
exit

```

