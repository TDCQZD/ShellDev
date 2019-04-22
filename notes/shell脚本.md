# shell 脚本
## 脚本格式
脚本以`#!/bin/bash`开头（指定解析器）
### 示例：
第一个Shell脚本：helloworld
1. 需求：创建一个Shell脚本，输出helloworld
2. 案例实操：
```
$ touch helloworld.sh
$ vi helloworld.sh
```
在helloworld.sh中输入如下内容
```
#!/bin/bash
echo "helloworld"
```
### 脚本的常用执行方式

**第一种：bash或sh**

采用bash或sh+脚本的相对路径或绝对路径（不用赋予脚本+x权限）
```
$ sh helloworld.sh  # sh+脚本的相对路径
$ sh /home/datas/helloworld.sh  # sh+相对路径执行脚本

$ bash helloworld.sh  # bash+脚本的相对路径
$ bash /home/datas/helloworld.sh  # bash+相对路径执行脚本
```
### `./`	
第二种：采用输入脚本的绝对路径或相对路径执行脚本（必须具有可执行权限+x）
1. 首先要赋予helloworld.sh 脚本的+x权限
```
$ chmod 777 helloworld.sh
```
2. 执行脚本
```
$ ./helloworld.sh 
$ /home/datas/helloworld.sh 
```
注意：第一种执行方法，本质是bash解析器帮你执行脚本，所以脚本本身不需要执行权限。第二种执行方法，本质是脚本需要自己执行，所以需要执行权限。
