# 一、vi、vim

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
10. `cat [fileName]`  display text file on screen readonly.(cat : concatenate 连接)
    `cat -n [fileName]`  -n: display line number
    `cat -n [fileNam] | more`  page display  text file 
11. `more [fileName]`  more是一个基于vi编辑器的文本过滤器，它以全屏方式按页显示文本文件的内容。
    **shortcut keys** 
    - space  下翻一页
    - Enter  下翻一行
    - q  离开
    - ctrl+F  滚动一屏 forward
    - ctrl+B  返回上一屏 back
    - =  输出当前行的行号
    - :f  输出文件名和当前行的行号
12. `less [fileName]`  与more相似，但更强大。根据显示需要加载内容，对显示大型文件具有较高的效率。
    **shortcut keys**
    - space 下一页
    - [pagedown] 下一页
    - [pageup] 上一页
    - /string 向下搜索“string”，n:向下查找，N：向上查找
    - ?string 向上搜索
    - q 离开
13. 

