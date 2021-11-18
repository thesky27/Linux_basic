# 第二章linux基本工具

### 一、重定向

##### 1.输入重定向

- cat test.py——输入来源是键盘，终端执行cat命令，并查看test文件内容
- cat <文件名 ——执行者是文件，改变命令来源，让他来源于一个文件、
- wc -l 文件名 ——查看文件行数

##### 2.输出重定向

- 命令把内容输出到文件中，重定向就是把输出的内容写到文件中
- echo 内容——将内容输出到终端
- 命令 内容 >文件——会覆盖到原有内容
- 命令 内容 >>文件——追加内容——echo 内容 >>文件

### 二、终端信息传输

##### 1.查看信息

- tty ——查看终端信息
- who am i——只看自己的信息
- w——查看所有的终端信息
- echo hello >> /dev/pts/0——在另一个终端上输出hello

##### 2.文件别名

- alias cdt cdt="cd test/"——把复杂的命令定义一个别名
- alias cdt或者type cdt——查看原本的命令
- 但这只是临时的，unalias cdt——取消别名
- 若想变成永久的则——修改家目录下的隐藏文件.bash——修好需要下次才能使用——source .bashrc立即生效
- ls -alF等于ll,la等于ls -a

##### 3.文件打包

- tar  -cvf test.tar test py_case——将test py_case打包到一起test.tar
- tar  -cxf test.tar test.tar——解压test.tar
- tar  -czvf test.tar.gz test py_case——将test py_case打包到一起test.tar,并压缩软件
- tar -xvf test.tar.gz -C 解压到的目录
- tar  -cgvf test.tar.bz2 test py_case——将test py_case打包到一起test.tar,并压缩软件
- find -name "*.sh" >> a.list——找到当前目录下的所有脚本文件
- tar -T a.list -czvf a.tar.gz——将a.list文件里面的内容打包到a.tar.gz里面去

##### 4.链接——创建快捷方式

- ln 要链接的文件地址 连接名——硬链接

- ln ./test/a.py a.hard——将test文件夹下的a.py文件创建一个快捷方式a.hard——硬链接
- 不会受删除原文件的影响，大小不会发生改变相当于复制，会进行内容同步
- ln -s 要链接的文件地址 连接名——软链接
- ln -s  ./test/a.py a.hard——创立一个软连接，内容也会同步，但受源文件的影响——相当于Windows中的桌面快捷方式

##### 5.进程管理

- 进程就是正在进行中的程序——一个程序有多个进程
- 查看进程：ps 命令——u:按用户启动时间来展示，a：显示所有用户的所有进程，x：显示无终端控制的进程
- ps -aux | grep python——查看与python有关的进程
- 结束进程：kill -9 端口——强制结束进程
- ps——动态的监听进程——q退出
- CTRL+c或者CTRL+z——暂停进程

##### 6.shell

- 解释器——将人的语言翻译成电脑能识别的语言
- 编程语言——脚本语言，模式：交互模式——打开终端就是了

脚本的编写

```python
#shell脚本的第一行最好是以#！开头——是脚本开始的标记，告诉系统执行某个解释器，后面的路径只是具体路径
#第二行是注释
#第三行简单的输出命令
#$ 数字 0代表文件名 1代表第一个参数
#！/bin/bash
#this is test
echo "Hello Shell"
echo $0#打印文件名
echo $1#接收参数
echo $2#接受参数

```



```python
#test
bash test.sh yige one
#结果是
Hello Shell
test.sh
yige

```



