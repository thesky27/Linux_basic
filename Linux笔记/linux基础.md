[TOC]

# 第一章Linux基础

### 一、基本命令

##### 1.ls命令

- 清屏——CTRL+l或者clear
- who——显示登录信息（用户、终端、开机时间）
- pwd——查看自己当前的位置
- ls——查看当前位置的所有文件以及文件夹。
- ls -a查看所有的文件包含隐藏的文件（.开头的就是隐藏文件）
- ls -l——以列表的形式展示文件（一般不包含隐藏文件）
- ls --help——查看帮助文档

##### 2.cd命令

- cd /——进入根目录
- cd 空格或者~——回到家目录
- tab键——自动补全
- cd py_case/——进入下一级目录
- cd ../——回到上一级目录，最后一个/可以省略
- cd -——回到之前所在的目录

##### 3.文件操作

- mkdir test——创建test文件夹
- rmdir test——删除test文件夹
- **touch test.py——创建文件**
- rm -rf test——删除test文件夹
- rm可以带参数，r表示递归删除，f表示强制删除
- cat test.py——查看该文件
- cp test.py a.py——将test复制到a文件里面
- mv test.py 路径——将将test移动到某个文件里

### 二、用户解读

![image-20210707182129985](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210707182129985.png)

- 用户名@计算机名：当前路径+身份
- $:普通用户，#:超级用户

##### 1.用户权限

- sudo 临时提权

![image-20210707182708491](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210707182708491.png)

### 三、linux的基本操作

##### 1.软件介绍

- 软件安装：下载系统相关的软件与插件使用apt命令
- python相关包：pip下载相关的库
- sudo apt remove 插件名
- sudo pip uninstall 插件名
- pip install 插件名 -i [https://pypi.douban.com/simple](https://pypi.douban.com/simple)
- 远程连接工具：MobaXterm.exe——绿色版本不需要安装解压即可，或者xshell
- 通过MobaXterm.exe可以进行文件的上传与下载

##### 2.用户操作

- useradd -m (自动建立用户的登录命令) 用户名——必须是超级用户创建的
- 切换用户 ——su 超级用户名，切换用户要设置密码
- useradd -m yige——设置账号              passwd yige ——设置密码
- 出现乱码则——vim /etc/passwd——将sh改为bash
- 退出编辑模式——esc+：q，保存退出——esc+：wq,强制退出——esc+：q!
- 进行编辑模式——i,
- 删除用户——userdel 用户名——但是信息还保留着，不能再次创建相同的用户名
- userdel -r 用户名——全部删除
- 切换组——sudo newgrp 组名

##### 3.组

- groupadd  组名 ——创建组，groupdel 组名——删除组名
- groups——查看组

###### 3.1权限控制

- chmod u +w ——增加写的权限只能通过超级用户来管理

##### 4.文件权限控制

![image-20210709152511206](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210709152511206.png)

- 第一列——第一个字符d和-	d代表的是目录，-代表的是文件
- 第二列——剩余的全部表示文件的权限9个字符——三个字符为一组
  - 第一组：所有者的权限，第二组：所属组的权限，第三组其他人的权限
  - u-所有者 g-所属组 o -其他人

- 第三列——硬链接个数——文件夹引用计数
- 第四列——所有者
- 第五列——所属组
- 第六列——文件大小
- 第七列——修改时间
- 第八列——文件名

**r:读4——w:写2——x：目录表示是否有进入的权限或可执行权限1——-没有权限**

###### 4.1权限设置

- chmod 要操作的对象（+，-）权限 要操作的文件
- chgrp 组名 文件名 ——修改文件所属的用户组
- chown——将文件或者目录更改新的属主与属组——sudo chown -R yige:yige test.py

##### 5.vim的使用——一开始是命令模式

- gg移动到首行
- yy复制当前行——nyy:复制n行
- p粘贴
- u撤销
- CTRL+r取消撤销
- i：编辑模式
- esc:退出到命令模式——在按：进行到末行模式

##### 6.寄存器

- 相当于粘贴板Vim提供了36个粘贴板——a-z0-9
- 复制三行放到a的粘贴板——3“ayy
- 3"p粘贴
- ：reg——查看寄存器
- set nu:显示行号

##### 7.find命令格式

find [-path] -options

- find -name 'a*'——默认当前目录
- find  /home/bd/ -name "*.py"

##### 8.管道符—— |xargs

- find -name '*.py' |xargs rm 
- 将|前的输出结果作为参数执行后面的程序

##### 9.grep命令

- grep -c "print" 文件名——展示符合条件的条数
- grep -nw "print" 文件名——展示编号及内容
- grep -no "print" 文件名——只输出匹配到的部分

