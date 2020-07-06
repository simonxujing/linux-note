# 一、实操命令

​	文本编辑器。

## 1、三种常见模式：

1. 正常模式

   在正常模式中，可以使用快捷键

2. 插入模式/编辑模式
   按i进入编辑模式

3. 命令模式
   提供读取、存盘、离开、替换等命令



## 2、Vi/Vim命令

1. `:wq `write quit 保存并退出
2. `:q` 未修改内容退出
3. `:q!`  已修改，不保存强制退出

## 3、开关机、重启、注销命令

1. shutdown：
   `shutdown -h now` 立即关机
   `shutdown -h 1` 一分钟后关机
   `shutdown -r now` 立即重启
2. `halt` 关机
3. `reboot` 重启
4. `sync` 把内存数据同步到磁盘，防止数据丢失，建议关机前执行一次
5. `logout` 注销

## 4、用户管理

1. `useradd username`  添加用户
   `useradd -d dirname username`  指定目录添加用户
   
2. `passwd 用户名`  修改用户密码

3. `userdel 用户名`  删除用户，不删除/home/用户名 目录
   `userdel -r 用户名 `  删除用户，且删除/home/用户 目录
   
4. `id 用户名`  查询用户
   uid=1000(isalpha) gid=1000(isalpha) groups=1000(isalpha),10(wheel)

5. `su username`  切换用户
   `exit`  退出当前用户的登录状态

6. `groupadd groupName`  增加组名

7. `groupdel groupName`  delete group

8. `useradd -g groupName userName`  add user to specified group

9. `usermod -g groupName userName`  modify user's group

10. **/etc/passwd**   file that store user configuration information
    userName: password: groupId: homeDir: ShellDir

11. **/etc/group**  store group infomation

    groupName: password: groupId: user list in this group

12. **/etc/shadow**  store user information and password (Encrypted)
    userName: password: lastModifiedTime: ...

## 5、实用指令

1. Specify run level （指定运行级别）
   0: halt 关机
   1: single-user mode 单用户 
   2: mutli-user mode 多用户状态没有网络服务
   3: mutli-user mode with networking 多用户有网络服务
   4: undefined 未定义（保留）
   5: X11 图形界面
   6: reboot 重启
   **/etc/inittab**  **/lib/systemd/system (ubuntu)**  file is the configuration file used by System V initialzation system in Linux.
   `init [012356]`   run level command
   **How to find root's pwd** :  `init 1` to select single-user mode (cuz in single-user mode, root can login without pwd )

2. centos 8 enter single-user mode

   1. press 'enter' to selected item

   2. Press ‘**e**’ to enter in the edit mode and then go to the end of line which starts with ‘**linux**‘ word, type the keyword “**rd.break**”

   3. press **Ctrl-x** to boot system in single user mode

   4. Remount the /sysroot in read-write (rw) mode

      ```
      switch_root:/# mount -o remount,rw /sysroot
      switch_root:/# chroot /sysroot
      sh-4.4#
      ```

   5. change pwd

      ```
      sh-4.4# echo “P@ssW0rD@123#” | passwd --stdin root 
      sh-4.4# touch /.autorelabel
      sh-4.4# reboot -f
      ```

3. `man [command]`  show the manual of command 

4. `help [command]`  show description of command


## 6、目录指令

1. `pwd`  print the current working directory
2. `ls `  print list of current working directory
3. `cd ~`  put you in username's home directory (cd meas **ch**ange **dir**ectory)
   `cd ..`  move you up one directory
4. `mkdir [dirName]`  create a new directory named dirName (make directory)
   `mkdir -p [dirA/dirB/dirC]`  create folder dirA and its subfolder
5. `rmdir [dirName]`  only can remove empty directory
6. `touch [fileName]`  create a new file named filename
7. `cp [option] [source] [destination]`  copy file or folder to specified destination
   `cp -r [source] [dest]`  copy all the files in the folder to specified destination (-r : recursive 递归)
   `\cp -r [source] [desc]`  copy and overwrite the original file 强制覆盖复制
8. `rm -r [name]`  recursive remove file or folder 
   `rm -f [name]` force remove file or folder, no prompt
   `rm -rf [name]`  recursive and force remove file or folder
9. `mv oldNameFile newNameFile`  rename the file
   `mv /temp/movefile /targetFolder`  move file to the targetFolder

## 7、文件内容相关指令

1. `cat [fileName]`  display text file on screen readonly.(cat : concatenate 连接)
   `cat -n [fileName]`  -n: display line number
   `cat -n [fileNam] | more`  page display  text file 

2. `more [fileName]`  more是一个基于vi编辑器的文本过滤器，它以全屏方式按页显示文本文件的内容。
   **shortcut keys** 
   - space  下翻一页
   - Enter  下翻一行
   - q  离开
   - ctrl+F  滚动一屏 forward
   - ctrl+B  返回上一屏 back
   - =  输出当前行的行号
   - :f  输出文件名和当前行的行号

3. `less [fileName]`  与more相似，但更强大。根据显示需要加载内容，对显示大型文件具有较高的效率。
   **shortcut keys**
   - space 下一页
   - [pagedown] 下一页
   - [pageup] 上一页
   - /string 向下搜索“string”，n:向下查找，N：向上查找
   - ?string 向上搜索
   - q 离开

4. `>` `>>` command
   `ls > fileName.txt`  overwrite to fileName.txt
   `ls >> fileName.txt`   append to fileName.txt
   `cat fileA > fileB`  overwrite A to B
   `echo "hello" > fileName.txt`  append "hello" to fileName.txt

5. `echo`  output content to the console

   `echo $PATH`  print PATH 环境变量

   `head -n 5 [file]`   show top 5 lines of this file.

   `tail -f [file]`  实时追踪文档的所有更新

6. `ln` 软连接或符号链接，类似于windows里的快捷方式，主要存放了链接其他文件的路径
   `ln -s [orginalFileName or orginalDirectory] [destinationLink]`  
   `rm -rf [destinationLink]`  删除软链接时，不要带/（destinationLink/）

7. `history`  show executed command history
   `history 10`  show last 10 executed command 
   `!1(after history)` execute command that number is 1

8. `date`  display current datetime
   `date "+%Y-%m-%d %H:%M:%S"`
   `date -s [datetime string]`  set system time. eg `date -s "2020-10-10 10:10:10"`

9. `cal`  print calendar
   `cal 2020` print calendar of 2020

10. `find [range] [option]`

    option: 

    - `-name [fileName]`  find file that the name is 'fileName'  eg.`find / -name *.txt`  支持通配符
    - `-user [userName]`  根据文件拥有者查找
    - `-size [size]`  eg. `find /home -size +20M` 大于20兆的文件。  eg.`find /home -20M` 小于20兆的文件

11. `locate [fileName]`  可以快速定位文件路径。locate指令利用实现建立的系统中所有文件名称以及路径的locate数据库实现快速定位到给定文件。第一次运行前需使用`sudo updatedb`  指令创建locate数据库。

12. `grep` 过滤查找。 `|`  管道符，表示将前一个命令的处理结果传递给后面的命令处理。
    `grep -n -i ` -n: 显示行号；-i：忽略大小写

## 8、压缩、解压缩指令

1. `gzip [fileName]`  压缩，源文件不保留
2. `gunzip [fileName]`  解压缩
3. `zip [option] [fileName] [dirtoryName]` 压缩文件夹到当前目录 eg.`zip -r mypackage.zip /home`
4. `unzip [fileName] -d [dirtoryName]` 解压缩
5. `tar`  打包指令
   option:
   - `-c` 产生tar打包文件
   - `-v` 显示详细信息
   - `-f` 指定解压缩后的文件名
   - `-z` 打包同时压缩
   - `-x`  解包.tar文件

# 二、组、权限管理

## 1、组管理

1. `ls -ahl`  查看文件所有者
2. `chown [userName] [fileName]` 修改文件所有者
3. `chgrp [groupName] [fileName]` 修改文件所在组
4. `usermod -g [groupName] [userName] `  修改用户所在组

## 2、权限管理

1. `chmod`  修改文件或者目录的权限
   - `u` user 所有者
   - `g` group 所在组
   - `o` other 其他人
   - `a` all 所有人
   - `chmod u=rwx,g=rw,o=r [file]`  给文件设置权限
   - `chmod u-x`  去除所有者执行权限
   - `chmod a+r`  添加所有用户读权限
   - `r=4 w=2 x=1`  可使用 `chmod 751 [file]`  相当于`chmod u=rwx,g=rx,o=x [file]`
2. `chown`  修改拥有者
   - `chown newOwner [file]` 
   - `chown newOwner:newGroup [file]`  修改文件的所有者和所有组
   - `chown -R [user] [dir]`  将dir目录下的所有文件递归修改拥有者

# 三、任务调度

## 1、crond 任务调度

1. `crontab -e`  编辑crondtab定时任务
   eg1. `crontab -e`  then insert ```*/1 * * * * ls -l /etc >> /tmp/to.txt```

   | object  | meaning            | range               |
   | ------- | ------------------ | ------------------- |
   | 第一个* | 一小时中的第几分钟 | 0~59                |
   | 第二个* | 第几个小时         | 0~23                |
   | 第三个* | 第几天（日）       | 1~31                |
   | 第四个* | 月份               | 1~12                |
   | 第五个* | 一周中的周几       | 0~7（0、7都为周日） |

   eg2. 每隔一分钟，将当前日期追加到/tmp/mydate 中

   - `touch myTask1.sh`
   - `vim myTask1.sh`   insert ```date >> /tmp/mydate```
   - `chmod 744 myTask1.sh`
   - `crontab -e` insert ``` */1 * * * * /tmp/myTask1.sh ```

2. `cronatb -l`  查询crontab任务

3. `crontab -r`  删除当前用户所有的crontab任务，终止任务调度

4. `service crond restart`  重启任务调度

# 四、磁盘分区与挂载

## 1、基础知识

1. MBR分区
   - 最多支持4个主分区
   - 扩展分区占一个主分区
   - 系统只能装在主分区
   - 最大支持2TB，但有较好的兼容性
   
2. GPT分区
   - 支持无限个主分区（但操作系统中有限制，如window最多128个主分区）
   - 最大支持18EB的大容器（1EB=1024PB，1PB=1024TB）
   - window7 64位以后支持GTP
   
3. Linux硬盘分为IDE硬盘和SCSI硬盘，目前基本上为SCSI硬盘

   `lsblk` `lsblk -f`  list block 查看分区、挂载情况
   `sda`  分区号， `sr0` 光驱， `MOUNTPOING` 挂载点

4.  P43

5. 

