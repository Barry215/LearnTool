## Java实践

### java设计模式

#### 工厂模式

#### 单例模式



### 数据库



### JDBC



### FTP



### Linux

#### 简介

Linux是一种比Windows更加稳定，免费，性能高的操作系统。它被广泛用在服务器领域和移动端，比如安卓系统和嵌入式系统开发，所以我们学习网站开发，必须了解，并掌握Linux。

#### 特点

- 在linux中，一切设备，一切软硬件都被看作是文件。
- linux区分大小写
- \#(表示超级用户) 
- $(表示普通用户)
- 命令的参数可以一起使用，如`mkdir -vp`

#### 常用命令

##### 查看当前目录的绝对路径：`pwd`

##### 清屏：`clear`

##### 路径补全：`tab` 键

##### 测试网络是否连通：`ping`

```shell
ping www.baidu.com #向百度发送数据包，回收数据包
```

##### 远程访问服务器：`ssh`

```shell
 ssh root@172.11.1.67 #用root用户来登录远程服务器,然后会提示你输入密码
 logout #退出
```

##### 查看时间：`date`

```shell
#返回
2016年11月 3日 星期四 14时27分28秒 CST
```

##### 查看日期：`cal`

##### 查看有哪些用户登录了系统：`who`

##### 查看当前是哪个用户登录了系统：`whoami`

##### 查看历史命令：`history`

##### 查看命令帮助：`whatis`,`info`,`which`,`man`,`--help`

```shell
#使用方法
whatis command
info command
which command
man command
command -h
command -help
command --help
#在只记得部分命令关键字的场合，我们可通过man -k来搜索；
#需要知道某个命令的简要说明，可以使用whatis；而更详细的介绍，则可用info命令；
#查看命令在哪个位置，我们需要使用which；
#而对于命令的具体参数及使用方法，我们需要用到强大的man；
#会在终端列出所有可用的命令,可以使用任何命令的-h或-help选项来查看该命令的具体用法。
```

##### 查文件或目录的大小：`du`

```shell
du -h 文件名 
#查看文件夹大小 du -h T01
#查看文件大小 du -h tt.txt
```

##### 查看文件与目录的命令：`ls`

```shell
ls -l #列出长数据串，包含文件的属性与权限数据等，可以简写成:ll
ls -a #列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用）  
ls -d #仅列出目录本身，而不是列出目录的文件数据  
ls -h #将文件容量以较易读的方式（GB，kB等）列出来  
ls -R #连同子目录的内容一起列出（递归列出），等于该目录下的所有文件都会显示出来
```

##### 切换目录：`cd`

```shell
cd				   # 切换到初始目录下
cd /               # 切换到根目录下
cd (directory)     # 切换到某个子目录下
cd /root/Docements # 切换到目录/root/Docements  
cd -               # 切换到上一次的目录
cd ..              # 切换到上层目录
cd ../path         # 切换到上层目录中的path目录中，“..”表示上一层目录
```

##### 创建文件：`touch`

```shell
touch 文件名
#例如：
touch test.txt
```

##### 创建文件夹：`mkdir`

```shell
mkdir 文件夹 #创建文件夹
mkdir -p 目录 #此时若路径中的某些目录尚不存在,系统将自动建立好那些尚不存在的目录,即递归创建多个目录
mkdir -v 文件夹 #每次创建新目录都显示信息
```

##### 删除空目录：`rmdir`

```shell
#例如
rmdir d101 #删除空目录d101  
rmdir d102 d103 #同时删除两个空目录d102,d103  
rmdir -p d104/d105/ #删除d105目录后，若d104是空的，则连d104一起删除  
```

##### 搜寻指定的字符串：`grep`

```shell
grep "<string>" <file-name>
grep -i "<string>" <file-name>    #在搜寻时会忽略字符串的大小写。
grep -r "<string>" <file-name>    #则会在当前工作目录的文件中递归搜寻指定的字符串。
```

##### 查找某目录下文件：`find`

```shell
# 与时间有关的参数：  
find -mtime n : n为数字，意思为在n天之前的“一天内”被更改过的文件；  
find -mtime +n : 列出在n天之前（不含n天本身）被更改过的文件名；  
find -mtime -n : 列出在n天之内（含n天本身）被更改过的文件名；  
find -newer file : 列出比file还要新的文件名  
# 例如：  
find /root -mtime 0 # 在root目录下查找今天之内有改动的文件  

# 与用户或用户组名有关的参数：  
find -user name : 列出文件所有者为name的文件  
find -group name : 列出文件所属用户组为name的文件  
find -uid n : 列出文件所有者为用户ID为n的文件  
find -gid n : 列出文件所属用户组为用户组ID为n的文件  
# 例如：  
find /home/ljianhui -user ljianhui # 在目录/home/ljianhui中找出所有者为ljianhui的文件

# 与文件权限及名称有关的参数：
find -name filename ：找出文件名为filename的文件
find -size [+-]SIZE ：找出比SIZE还要大（+）或小（-）的文件  
find -tpye TYPE ：查找文件的类型为TYPE的文件，TYPE的值主要有：一般文件（f)、设备文件（b、c）、  
         目录（d）、连接文件（l）、socket（s）、FIFO管道文件（p）；  
find -perm mode ：查找文件权限刚好等于mode的文件，mode用数字表示，如 0755；  
find -perm -mode ：查找文件权限必须要全部包括mode权限的文件，mode用数字表示  
find -perm +mode ：查找文件权限包含任一mode的权限的文件，mode用数字表示  
# 例如：  
find / -name passwd # 查找文件名为passwd的文件  
find . -perm 0755 # 查找当前目录中文件权限的0755的文件  
find . -size +12k # 查找当前目录中大于12KB的文件，注意c表示byte
```

##### 复制文件：`cp`

```shell
cp -a #将文件的特性一起复制，相当于 -pdr 的意思
cp -p #连同文件的属性一起复制，而非使用默认方式，与-a相似，常用于备份  
cp -i #若目标文件已经存在时，在覆盖时会先询问操作的进行  
cp -d #若来源文件为连结文件的属性(link file)，则复制连结文件属性而非档案本身； 
cp -r #递归持续复制，用于目录的复制行为  
cp -u #目标文件与源文件有差异时才会复制
# 例如：
cp 源文件路径/源文件名 目标路径
cp T01/test.txt T02/  
cp -a file1 file2 #连同文件的所有特性把文件file1复制成文件file2  
cp file1 file2 file3 dir #把文件file1、file2、file3复制到目录dir中
```

##### 远程复制文件(夹)：`scp`

```shell
#必须在本地使用中这条命令，不能在服务器上用
scp [-r](递归复制) root@IP地址或域名:服务器文件(夹) 本地路径
scp -r root@172.11.1.112:/root/install.log /root/
```

##### 移动文件,目录或重命名：`mv`

```shell
-f #force强制的意思，如果目标文件已经存在，不会询问而直接覆盖  
-i #若目标文件已经存在，就会询问是否覆盖  
-u #若目标文件已经存在，且比目标文件新，才会更新
# 例如：
mv file1 file2 file3 dir # 把文件file1、file2、file3移动到目录dir中  
mv file1 file2 # 把文件file1重命名为file2
```

> 注：该命令可以把一个文件或多个文件一次移动一个文件夹中，但是最后一个目标文件一定要是“目录”。

##### 删除文件或目录：`rm`

```shell
rm -f #就是force的意思，忽略不存在的文件，不会出现警告消息  
rm -i #互动模式，在删除前会询问用户是否操作  
rm -r #递归删除，最常用于目录删除，它是一个非常危险的参数
# 例如：
rm -i file # 删除文件file，在删除之前会询问是否进行该操作  
rm -fr dir # 强制删除目录dir中的所有文件
```

##### 获取进程运行情况：`ps`

```shell
ps -A #所有的进程均显示出来  
ps -a #不与terminal有关的所有进程  
ps -u #有效用户的相关进程  
ps -x #一般与a参数一起使用，可列出较完整的信息  
ps -l #较长，较详细地将PID的信息列出
ps -ef #查看系统正在运行的进程
# 实例
ps aux  # 列出目前所有的正在内存当中的程序
ps ax   # 查看不与terminal有关的所有进程  
ps -lA  # 查看系统所有的进程数据  
ps axjf # 查看连同一部分进程树状态
```

##### 显示CPU占用量较大的进程：`top`

```shell
top    #top命令会默认按照CPU的占用情况，显示占用量较大的进程
top -u <username>    #查看某个用户的CPU使用排名情况。
```

##### 判断文件的基本数据：`file`

```shell
file filename
#例如：
file ger.txt
输出 ger.txt:ASCII text
```

> 因为在Linux下文件的类型并不是以后缀为分的，所以这个命令对我们来说就很有用了

##### 对文件进行打包：`tar`

```shell
tar -c ：新建打包文件  
tar -t ：查看打包文件的内容含有哪些文件名  
tar -x ：解打包或解压缩的功能，可以搭配-C（大写）指定解压的目录，注意-c,-t,-x不能同时出现在同一条命令中  
tar -j ：通过bzip2的支持进行压缩/解压缩  
tar -z ：通过gzip的支持进行压缩/解压缩  
tar -v ：在压缩/解压缩过程中，将正在处理的文件名显示出来  
tar -f filename ：filename为要处理的文件  
tar -C dir ：指定压缩/解压缩的目录dir
# 主要记住
压缩：tar -jcv -f filename.tar.bz2 要被处理的文件或目录名称  
查询：tar -jtv -f filename.tar.bz2  
解压：tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录
# 打包并压缩
tar 参数 目标文件路径和包名 被打包的文件名称
tar -czvf t101.tar.gz T101 #将目录和文件打到当前目录下的t101.tar.gz压缩包中
tar -czvf /opt/t101.tar.gz T101 #将目录和文件打到/opt/t101.tgz压缩包中
tar -tzvf ./t101.tar.gz #查看t101.tar.gz压缩包中的内容
```

> 注：
>
> - 默认情况并不会压缩，如果指定了相应的参数，它还会调用相应的压缩程序（如gzip和bzip等）进行压缩和解压
> - 文件名并不定要以后缀tar.bz2结尾，这里主要是为了说明使用的压缩程序为bzip2

##### 查看文件的内容：`more`,`less`,`cat`,`head`,`tail`

```shell
more 文件名        #按回车一行，空格一页。不能向上下翻行。  
less 文件名        #按回车一行，空格一页。可以通过上下键上下翻行。按q就退出。  
cat 文件名         #查看文件的所有内容  
cat -n 文件名      #查看文件的所有内容，并显示行数   
head -n 文件名     #查看文件的前n行，n表示你要看的行数。  
tail -n 文件名     #查看文件的后n行  
```

> 1. cat命令可以一次显示整个文件，如果文件比较大，使用不是很方便；
> 2. more命令可以让屏幕在显示满一屏幕时暂停，此时可按空格健继续显示下一个画面，或按Q键停止显示。
> 3. less命令也可以分页显示文件，和more命令的区别就在于它支持上下键卷动屏幕，当结束浏览时，只要在less命令的提示符“: ”下按Q键即可。

##### 改变文件所属用户组：`chgrp`

```shell
chgrp 组名 文件名
chgrp g1015 echo.sh
chgrp -R 组名 文件名
-R #进行递归的持续对所有文件和子目录更改  
# 例如：  
chgrp -R users ./dir # 递归地把dir目录下中的所有文件和子目录下所有文件的用户组修改为users
```

##### 改变文件的所有者：`chown`

```shell
#更改单个文件的属主：
#chown 用户名 文件名
chown wsg echo.sh

#更改文件夹的属主：
#语法：chown -R 用户名 文件名
chown -R u101 Desktop/ #单独更改文件夹的拥有者(-R表示文件夹的所有子内容全部更改,*表示所有本目录文件)

#同时更改文件的拥有者和所属组
#语法：chown 用户名:组名 文件名
chown u101:g1015 install.log.syslog #同时更改文件的拥有者和所属组

#同时更改文件夹和文件夹下的所有内容的拥有者和所属组
#语法：chown -R 用户名:组名 文件名
chown -R u101:g1015 test01 #同时更改文件的拥有者和所属组
```

##### 改变文件的权限：`chmod`

```shell
chmod 权限 文件名
如：chmod 755 filename
ls -l命令
获取：drwxr-xr-x  2 root root 4.0K 11-06 18:30 Desktop
解释：
r: read       可读
w: write      可写
x：execute    可执行
d表示是个普通文件夹
-表示普通文件
r用数字4表示，w用数字2表示，x用数字1表示。
第一个rwx，表示该文件所属的用户对其所拥有的操作权限
第二个rwx，表示与该文件所属用户在同组内的用户对其所拥有的操作权限
第三个rwx，表示不与该文件所属用户在同组内的用户对其所拥有的操作权限
第一个root:表示该文件夹属于哪个用户
第二个root:表示该文件夹属于哪个组

chmod -R xyz 文件或目录  
-R #进行递归的持续更改，即连同子目录下的所有文件都会更改
# 例如：  
chmod -R 755 file # 把file的文件权限改变为-rxwr-xr-x
# 同时，chmod还可以使用u（user）、g（group）、o（other）、a（all）和+（加入）、-（删除）、=（设置）跟rwx搭配来对文件的权限进行更改。
chmod g+w file # 向file的文件权限中加入用户组可写权限
```

##### 文本编辑：`vim`,`vi`

```shell
#Vim是从 vi 发展出来的一个文本编辑器
vim
#在命令行中输入vim,进入vim编辑器
vim filename
#用vim打开一个文件
i
#按一下i键,下端显示 --INSERT--
#插入命令,在vim中可能任意字符都有作用
Esc按键
#退出i(插入)命令进行其它命令使用
:w
#在编辑的过程中保存文件,相当于word中的ctrl+s
:w 文件名
#另存为
:wq
#保存文件并退出
:q!
#强制退出,不保存
u 
#撤消上一步操作
dd
#删除行
```

#### 更多命令

[29个你必须知道的Linux命令](http://www.jianshu.com/p/462c9e20ffb5)



### Git

#### 简介

Git是目前世界上最先进的分布式版本控制系统，以其优秀的控制能力独傲全球

#### 集中式版本控制系统-SVN,CVS

版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就纳闷了。

#### 分布式版本控制系统-Git

分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

#### Git学习笔记

[Gi基本操作](http://www.jianshu.com/p/1d5e97222cad)

[工作区、暂存区和版本库的关系](http://www.jianshu.com/p/4416c3c61dba)

[撤销或回退版本](http://www.jianshu.com/p/f0d6a5a4325f)

[连接远程仓库](http://www.jianshu.com/p/8468d43074f3)

[协同工作](http://www.jianshu.com/p/e7ddad179c9d)

[搭建git服务器](http://www.jianshu.com/p/ee8c379ef888)

#### Git命令

![git](www.maijinta.cn/user/files/git.png)

- workspace: 本地的工作目录。（记作A）
- index：缓存区域，临时保存本地改动。（记作B）
- local repository: 本地仓库，只想最后一次提交HEAD。（记作C）
- remote repository：远程仓库。（记作D）

```shell
#初始化
git init //创建
git clone /path/to/repository //检出
git config --global user.email "you@example.com" //配置email
git config --global user.name "Name" //配置用户名

#操作
git add <file> // 文件添加，A → B
git add . // 所有文件添加，A → B

git commit -m "代码提交信息" //文件提交，B → C
git commit --amend //与上次commit合并, *B → C

git push origin master //推送至master分支, C → D
git pull //更新本地仓库至最新改动， D → A
git fetch //抓取远程仓库更新， D → C

git log //查看提交记录
git status //查看修改状态
git diff//查看详细修改内容
git show//显示某次提交的内容

#撤销操作
git reset <file>//某个文件索引会回滚到最后一次提交， C → B
git reset//索引会回滚到最后一次提交， C → B
git reset --hard // 索引会回滚到最后一次提交， C → B → A

git checkout // 从index复制到workspace， B → A
git checkout -- files // 文件从index复制到workspace， B → A
git checkout HEAD -- files // 文件从local repository复制到workspace， C → A

#分支相关
git checkout -b branch_name //创建名叫“branch_name”的分支，并切换过去
git checkout master //切换回主分支
git branch -d branch_name // 删除名叫“branch_name”的分支
git push origin branch_name //推送分支到远端仓库
git merge branch_name // 合并分支branch_name到当前分支(如master)
git rebase //衍合，线性化的自动， D → A

#冲突处理
git diff //对比workspace与index
git diff HEAD //对于workspace与最后一次commit
git diff <source_branch> <target_branch> //对比差异
git add <filename> //修改完冲突，需要add以标记合并成功

#其他
gitk //开灯图形化git
git config color.ui true //彩色的 git 输出
git config format.pretty oneline //显示历史记录时，每个提交的信息只显示一行
git add -i //交互式添加文件到暂存区
```

#### Git使用规范提醒

- 使用Git过程中，必须通过创建分支进行开发，坚决禁止在主干分支上直接开发。review的同事有责任检查其他同事是否遵循分支规范。
- 在Git中，默认是不会提交空目录的，如果想提交某个空目录到版本库中，需要在该目录下新建一个 .gitignore 的空白文件，就可以提交了
- 把外部文件纳入到自己的 Git 分支来的时候一定要记得是先比对，确认所有修改都是自己修改的，然后再纳入。不然，容易出现代码回溯
- 多人协作时，不要各自在自己的 Git 分支开发，然后发文件合并。正确的方法应该是开一个远程分支，然后一起在远程分支里协作。不然，容易出现代码回溯（即别人的代码被覆盖的情况）
- 每个人提交代码是一定要 git diff 看提交的东西是不是都是自己修改的。如果有不是自己修改的内容，很可能就是代码回溯
- review 代码的时候如果看到有被删除掉的代码，一定要确实是否是写代码的同事自己删除的。如果不是，很可能就是代码回溯

#### Git使用规范

Git 使用规范流程 - [http://www.ruanyifeng.com/blog/2015/08/git-use-process.html](http://www.ruanyifeng.com/blog/2015/08/git-use-process.html)
团队中的 Git 实践 - [https://ourai.ws/posts/working-with-git-in-team/](https://ourai.ws/posts/working-with-git-in-team/)
构家网 git 团队协作使用规范 v2 - [http://wenku.baidu.com/view/e1430d1b7f1922791788e81e](http://wenku.baidu.com/view/e1430d1b7f1922791788e81e)

#### 扩展阅读

Git Book - [https://git-scm.com/book/zh/](https://git-scm.com/book/zh/)
git简明指南 - [http://rogerdudler.github.io/git-guide/index.zh.html](http://rogerdudler.github.io/git-guide/index.zh.html)
常用 Git 命令清单 - [http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
猴子都能懂的GIT入门 - [http://backlogtool.com/git-guide/cn/](http://backlogtool.com/git-guide/cn/)
Git教程 - [http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### 