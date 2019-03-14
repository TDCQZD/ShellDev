# Shell中的变量
## 变量的取用: echo
```
echo $PATH
```
## 变量的配置守则
1. 变量与变量内容以一个等号『=』来连结，如下所示： 
`『myname=VBird』`

2. 等号两边不能直接接空格符，如下所示为错误： 
`『myname = VBird』或『myname=VBird Tsai』`

3. 变量名称只能是英文字母与数字，但是开头字符不能是数字，如下为错误： 
`『2myname=VBird』`

4. 变量内容若有空格符可使用双引号『"』或单引号『'』将变量内容结合起来，但
- 双引号内的特殊字符如 $ 等，可以保有原本的特性，如下所示：
    `『var="lang is $LANG"』则『echo $var』可得『lang is en_US』`
- 单引号内的特殊字符则仅为一般字符 (纯文本)，如下所示：
    `『var='lang is $LANG'』则『echo $var』可得『lang is $LANG』`

5. 可用跳脱字符『 \ 』将特殊符号(如 `[Enter], $, \, 空格符, '`等)变成一般字符；

6. 在一串命令中，还需要藉由其他的命令提供的信息，可以使用反单引号『`命令`』或 『$(命令)』。特别注意，那个 ` 是键盘上方的数字键 1 左边那个按键，而不是单引号！ 例如想要取得核心版本的配置：
`『version=$(uname -r)』`再`『echo $version』`可得`『2.6.18-128.el5』`

7. 若该变量为扩增变量内容时，则可用 "$变量名称" 或 ${变量} 累加内容，如下所示：
`『PATH="$PATH":/home/bin』`

8. 若该变量需要在其他子程序运行，则需要以 export 来使变量变成环境变量：
`『export PATH』`

9. 通常大写字符为系统默认变量，自行配置变量可以使用小写字符，方便判断 (纯粹依照使用者兴趣与嗜好) ；

10. 取消变量的方法为使用 unset ：『unset 变量名称』例如取消 myname 的配置：
`『unset myname』`
## 系统变量
1. 常用系统变量
`$HOME、$PWD、$SHELL、$USER`等
```
$ echo $HOME # 查看系统变量的值
$ set # 显示当前Shell中所有变量
```

## 自定义变量
### 1．基本语法
- 定义变量：变量=值 
- 撤销变量：unset 变量
- 声明静态变量：readonly变量，注意：不能unset
### 2．变量定义规则
- 变量名称可以由字母、数字和下划线组成，但是不能以数字开头，环境变量名建议大写。
- 等号两侧不能有空格
- 在bash中，变量默认类型都是字符串类型，无法直接进行数值运算。
- 变量的值如果有空格，需要使用双引号或单引号括起来。

### 示例：
```
# 定义变量A

$ A=5
$ echo $A
5
```
```
# 给变量A重新赋值
$ A=8
$ echo $A
8
```
```
# 撤销变量A
$ unset A
$ echo $A
```
```
# 声明静态的变量B=2，不能unset
$ readonly B=2
$ echo $B
2
$ B=9
-bash: B: readonly variable
```
```
# 在bash中，变量默认类型都是字符串类型，无法直接进行数值运算
$ C=1+2
$ echo $C
1+2
```
```
# 变量的值如果有空格，需要使用双引号或单引号括起来
$ D=I love banzhang
-bash: world: command not found
$ D="I love banzhang"
$ echo $A
I love banzhang
```
```
# 可把变量提升为全局环境变量，可供其他Shell程序使用 `export 变量名`
$ vim helloworld.sh 

在helloworld.sh文件中增加echo $B
#!/bin/bash

echo "helloworld"
echo $B

$ ./helloworld.sh 
Helloworld
发现并没有打印输出变量B的值。
$ export B
$ ./helloworld.sh 
helloworld
2
```
## 特殊变量：
### `$n`
**基本语法**
- $n	（功能描述：n为数字，$0代表该脚本名称，$1-$9代表第一到第九个参数，十以上的参数，十以上的参数需要用大括号包含，如${10}）

**示例**

输出该脚本文件名称、输入参数1和输入参数2 的值
```
$ touch parameter.sh 
$ vim parameter.sh

#!/bin/bash
echo "$0  $1   $2"
```
```
$ chmod 777 parameter.sh

$ ./parameter.sh cls  xz
./parameter.sh  cls   xz
```
### `$#`

**基本语法**
- $#	（功能描述：获取所有输入参数个数，常用于循环）。

**案例**

获取输入参数的个数
```
$ vim parameter.sh

#!/bin/bash
echo "$0  $1   $2"
echo $#

$ chmod 777 parameter.sh

$ ./parameter.sh cls  xz
parameter.sh cls xz 
2
```
### `$*`、`$@`
**基本语法**
-	$*	（功能描述：这个变量代表命令行中所有的参数，$*把所有的参数看成一个整体）
- 	$@	（功能描述：这个变量也代表命令行中所有的参数，不过$@把每个参数区分对待）

**案例**

打印输入的所有参数
```
$ vim parameter.sh

#!/bin/bash
echo "$0  $1   $2"
echo $#
echo $*
echo $@

$ bash parameter.sh 1 2 3
parameter.sh  1   2
3
1 2 3
1 2 3
```
### `$？`
**基本语法**
- $？	（功能描述：最后一次执行的命令的返回状态。如果这个变量的值为0，证明上一个命令正确执行；如果这个变量的值为非0（具体是哪个数，由命令自己来决定），则证明上一个命令执行不正确了。）

**案例**

判断helloworld.sh脚本是否正确执行
```
$ ./helloworld.sh 
hello world
$ echo $?
0
```