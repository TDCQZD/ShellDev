# read读取控制台输入
## 基本语法
```
	read(选项)(参数)
```
选项：
* -p：指定读取值时的提示符；
*  -t：指定读取值时等待的时间（秒）。
参数
	变量：指定读取值的变量名
## 案例实操
提示7秒内，读取控制台输入的名称
```
$ touch read.sh
$ vim read.sh
```
```
#!/bin/bash

read -t 7 -p "Enter your name in 7 seconds " NAME
echo $NAME
```
```
$ ./read.sh 
Enter your name in 7 seconds xiaoze
xiaoze
```