# Shell 


Shell 是一个命令行解释器，它接收应用程序/用户的命令，然后调用操作系统内核。

shell 介于Linux 内核和 外部引用程序之间。

shell 还是一个功能强大的编程语言，易编写、易调试、灵活性强。(python 性能更好)

## Shell解析器
1. Linux提供的Shell解析器有：6
```
[root@Aws ~]$ cat /etc/shells 
/bin/sh
/bin/bash
/sbin/nologin
/bin/dash
/bin/tcsh
/bin/csh
```

2. bash和sh的关系:sh 调用bash
```
[atguigu@hadoop101 bin]$ ll | grep bash
-rwxr-xr-x. 1 root root 941880 5月  11 2016 bash
lrwxrwxrwx. 1 root root      4 5月  27 2017 sh -> bash
```
3. Centos/Unbutn默认的解析器是bash
```
[atguigu@hadoop102 bin]$ echo $SHELL
/bin/bash
root@Aws:~# echo $SHELL
/bin/bash
root@Aws:~# 

```

## shell 脚本
```

#!/bin/bash
echo "Hello world ！"

```
```
root@Aws:~/shell# sh helloword.sh 
Hello world ！
root@Aws:~/shell# bash helloword.sh 
Hello world ！
root@Aws:~/shell# ./helloword.sh
-bash: ./helloword.sh: Permission denied
root@Aws:~/shell# chmod 777 helloword.sh 
root@Aws:~/shell# ./helloword.sh
Hello world ！
root@Aws:~/shell# 

```