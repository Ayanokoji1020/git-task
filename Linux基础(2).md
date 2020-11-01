# 红岩网校运维安全部 Linux基础



## Part 0. Linux三问

假期的时候很多小伙伴都对linux不太了解，也不明白我们布置的作业有什么意义，那么我们第一节课就从linux的三个问题开始吧。

### 1. 什么是 Linux

Linux，全称GNU/Linux，是一套免费使用和自由传播的[类UNIX](https://baike.baidu.com/item/类UNIX/9032872)操作系统，其内核由[林纳斯·本纳第克特·托瓦兹](https://baike.baidu.com/item/林纳斯·本纳第克特·托瓦兹/1034429)于1991年第一次释出，它主要受到Minix和Unix思想的启发，是一个基于[POSIX](https://baike.baidu.com/item/POSIX)和Unix的多用户、[多任务](https://baike.baidu.com/item/多任务/1011764)、支持[多线程](https://baike.baidu.com/item/多线程/1190404)和多[CPU](https://baike.baidu.com/item/CPU)的操作系统。它能运行主要的Unix工具软件、应用程序和网络协议。它支持[32位](https://baike.baidu.com/item/32位/5812218)和[64位](https://baike.baidu.com/item/64位)硬件。Linux继承了Unix以网络为核心的设计思想，是一个性能稳定的多用户网络操作系统。Linux有上百种不同的发行版，如基于社区开发的[debian](https://baike.baidu.com/item/debian/748667)、[archlinux](https://baike.baidu.com/item/archlinux/10857530)，和基于商业开发的[Red Hat Enterprise Linux](https://baike.baidu.com/item/Red Hat Enterprise Linux/10770503)、[SUSE](https://baike.baidu.com/item/SUSE/60409)、[oracle linux](https://baike.baidu.com/item/oracle linux/6876458)等。

### 2. 为什么要用 Linux

windows与linux的设计理念有根本性的区别：

​    **windows：**用户不知道自己想要什么，也不明白自己在做什么，更不打算为自己的行为负责。

​    因此windows将所有操作都隐藏起来，只给用户提供封装好的功能，用户只能在操作系统限制的范围内操作，如果是普通用户，会觉得很windows很舒服，因为不需要思考。只需要按照指示去操作。但对于开发人员而言，这种设计理念是无法接受的，一旦要做出一些超越封装好的功能之外的事情，就会出现各种难以意料的情况，而且很多情况下，这些问题是无解的。或者只能用极其蹩脚扭曲的方式去勉强处理，然后瑟瑟发抖地期待着程序能正常运行。

​    **linux：**用户知道自己想要什么，也明白自己在做什么，并且会为自己的行为负责。

​    linux将所有操作权都交给了用户，它相信用户是理性的聪明的，忠实地执行用户的指令，向用户暴露所有的细节。用户在拥有自主权的同时也拥有了破坏力，因此普通用户根本无法驾驭，可能一个指令就把操作系统弄崩溃了。对于开发者而言，linux的开放与自由给了我们无限的可能性，我们能看到程序是如何运行的，运行报错也会有友好的提示。根据报错指引往往能将问题解决。

### 3. 有了 Linux，你能做些什么

- 极小的资源占用与噪音污染（雾）
- 搭建个人博客/网盘/笔记本等各项服务
- 运维gitlab/jenkins等开发平台
- 编译自己的软路由提升上网体验
- 舒适地开发软件应用
- 用vps向全世界提供你自己的服务
- ......



## Part 1. 基础知识


> 重要警告：本部已与百度达成战略合作协议，遇到理解不了的问题的可以随时向百度请教



### 图形界面与命令行

- GUI：https://baike.baidu.com/item/GUI
- CLI：https://baike.baidu.com/item/CLI

![banner-of-cli](https://s2.ax1x.com/2019/10/10/uo22IU.jpg)



### 软件中心

Linux发行版与Windows最大的不同之处就在于它有自己的软件中心，安装应用往往可以一行代码解决，而Windows往往要经历 `打开浏览器 -> 进入软件官网 -> 下载安装包 -> 安装` 这几个步骤，极其的繁琐。



#### 包管理工具

你可以理解成软件中心，不同发行版所用的软件中心不同，就像各大品牌手机自身的应用商店一样。

对于以下常见的软件中心大家一定不要弄混，比如你在CentOS用apt装东西的样子就像在ios上装apk一样（雾

- DEB系：apt install xxx
- RPM系：yum install xxx
- Arch系：pacman -S xxx

以下教程我们使用DEB系的Ubuntu作为参考



#### 源(镜像源)

有同学装过系统以后在群里抱怨下载慢的问题，我们给的解决方式通常是 “换源”，那么什么是 “源”，“换源”又是什么意思？源在那好好的，我们为什么要换？下面我们来一一解答。

##### 1. 什么是镜像

> 镜像是冗余的一种类型，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本即为镜像。

##### 2. 什么是源站

> 顾名思义，源站就是“源头的站点“，也就是表示资源最初来自哪里。

##### 3. 什么是镜像源

> 综合上述，镜像源是把源站的资源在另一个地方进行一次拷贝，并定期同步，以方便特定人群进行高速下载

##### 4. 为什么要换源

> Linux 发行版的官方一般都在国外，你要是没有科学手段，那个下载速度很感人，相反，如果我们换成国内同步的镜像源，安装软件的速度会快很多。



**常用的源:**

[一键直达](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=%E9%95%9C%E5%83%8F%E6%BA%90&oq=linux%25E9%2595%259C%25E5%2583%258F%25E6%25BA%2590&rsv_pq=8163bd4a0010c5b4&rsv_t=7d8aJIFAc2BOmsNXoNF34HAFsx3ezg6N5zmNTxSpb3pOk6q%2BEndEKwIJVzs&rqlang=cn&rsv_enter=1&rsv_dl=tb&inputT=1718&rsv_sug3=31&rsv_sug1=26&rsv_sug7=100&rsv_sug2=0&rsv_sug4=3383)

### 如何换源

下面介绍一个命令

```bash
sed [-nefr] [动作]
选项与参数：
-n ：使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN 的数据一般都会被列出到终端上。但如果加上 -n 参数后，则只有经过sed 特殊处理的那一行(或者动作)才会被列出来。
-e ：直接在命令列模式上进行 sed 的动作编辑；
-f ：直接将 sed 的动作写在一个文件内， -f filename 则可以运行 filename 内的 sed 动作；
-r ：sed 的动作支持的是延伸型正规表示法的语法。(默认是基础正规表示法语法)
-i ：直接修改读取的文件内容，而不是输出到终端。

动作说明： [n1[,n2]]function
n1, n2 ：不见得会存在，一般代表『选择进行动作的行数』，举例来说，如果我的动作是需要在 10 到 20 行之间进行的，则『 10,20[动作行为] 』

function：
a ：新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)～
c ：取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！
d ：删除，因为是删除啊，所以 d 后面通常不接任何咚咚；
i ：插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)；
p ：列印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行～
s ：取代，可以直接进行取代的工作哩！通常这个 s 的动作可以搭配正规表示法！例如 1,20s/old/new/g 就是啦！
```

那么接下来就简单了（以ubuntu举例）

```bash
# 校内
sed -i 's/archive.ubuntu.com/mirrors.cqupt.edu.cn/g' /etc/apt/sources.list
# 校外
sed -i 's/archive.ubuntu.com/mirrors.redrock.team/g' /etc/apt/sources.list
```



### 怎么用?

```
apt update  更新源
apt list --upgradeable：(显示可升级的软件包) --installed：(显示已安装的软件包)
apt upgrade 升级软件包
apt install <软件包名>  安装指定软件
apt remove <软件包名>用来卸载指定软件。
apt autoremove用来自动清理不再使用的依赖和库文件。
apt show <软件包名> 显示软件包具体信息。
```

大家去看一下这篇文章------[apt命令详解](https://www.jianshu.com/p/e6f436f785ed)

至于换源,也给一个参考链接,记得输入你的操作系统名+换源(例如: ubuntu 换源)------[换源](https://www.baidu.com/)



## Part 1. 正片开始

### 预备工作

相信过了一个假期，大家都有自己的linux系统了，没有的也没关系，可以在下面的链接白嫖或者自己用虚拟机装一个



> 白嫖ECS：
>
> https://developer.aliyun.com/adc/student
>
> 阿里云实验室：
> https://edu.aliyun.com/roadmap/linux?spm=5176.11399608.aliyun-edu-index-014.2.216a4679CyE6Ek



### Linux常用知识点

#### Linux目录结构

**以下内容来自[运维](https://mp.weixin.qq.com/s?__biz=MzI4MDEwNzAzNg==&mid=2649445943&idx=2&sn=d0fcaa1cfcc5e767a11e72f5a4d1ce5a&chksm=f3a27744c4d5fe52afbfeed2fcf3aab688093f588024d8dc0afea1c6fef41f655413f59f1d1e&mpshare=1&scene=23&srcid=1009wsjSP7ok35o4DFUv4qyI&sharer_sharetime=1570625853080&sharer_shareid=bfbc6455430a72987624b0597100e6c1#rd
)**

你登上系统后,先输入一个 cd / ,再输入一个ls命令康康是不是像下面这样?

![QQ截图20191009224407](https://s2.ax1x.com/2019/10/10/uoICes.png)

这些就是Linux目录结构.下面我提取了一部分的文件目录,记得千万别删除他们┗|｀O′|┛ 嗷~~

![640](https://mmbiz.qpic.cn/mmbiz_jpg/tuSaKc6SfPrCdhhPgOiaoBcFPce4tpjykKa6Mib0INI8WR69mJnFnqycibJJyudibgmAPfx8eDgL3p9Phe3tgFmVzA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- bin (binaries)存放二进制可执行文件
- sbin (super user binaries)存放二进制可执行文件，只有root才能访问
- etc (etcetera)存放系统配置文件
- usr (unix shared resources)用于存放共享的系统资源
- home 存放用户文件的根目录
- root 超级用户目录
- dev (devices)用于存放设备文件
- lib (library)存放跟文件系统中的程序运行所需要的共享库及内核模块
- mnt (mount)系统管理员安装临时文件系统的安装点
- boot 存放用于系统引导时使用的各种文件
- tmp (temporary)用于存放各种临时文件
- var (variable)用于存放运行时需要改变数据的文件

**上面这些目录结构,大家要记一下.**这个没啥好讲的.

但是等我讲了下面的几个东西之后,就可以玩玩了

#### Linux常用命令选讲

**命令格式**：命令 -选项 参数 （选项和参数可以为空）

```
如：ls -la /usr
```

##### **操作文件及目录**

| 命令  | 参数  | 示例                     | 说明                                                         |
| ----- | ----- | ------------------------ | ------------------------------------------------------------ |
| cd    |       | cd /home                 | 切换目录                                                     |
| pwd   |       | pwd                      | 显示当前工作目录                                             |
| touch |       | touch 1.txt              | 创建空文件                                                   |
| mkdir |       | mkdir testdir            | 创建一个新目录                                               |
|       | -p    | mkidr -p dir1/dir2/dir3/ | 创建多级目录，父目录不存在情况下先生成父目录                 |
| cp    |       | cp 1.txt                 | 复制文件或目录                                               |
|       | -r    | cp -r dir1/              | 递归处理，将指定目录下的文件与子目录一并拷贝                 |
| mv    |       | mv dir1 dir2             | 移动文件或目录、文件或目录改名                               |
| rm    |       | rm 1.txt                 | 删除文件                                                     |
|       | -r-f  | rm -rf dir1              | r同时删除该目录下的所有文件,f强制删除文件或目录              |
| rmdir |       | rmdir dir1               | 删除空目录                                                   |
| cat   |       | cat 1.txt                | 显示文本文件内容                                             |
| find  | -name | find / -name 1.txt       | 在文件系统中的指定目录下查找指定的文件                       |
| grep  |       | grep aaa 1.txt           | 在指定文件中查找包含指定内容的行，例：在1.txt中查找包含aaa的所有行 |

##### **系统常用命令**

| **命令** | **参数** | **示例**       | **说明**                           |
| -------- | -------- | -------------- | ---------------------------------- |
| ifconfig |          | ifconfig       | 网卡网络配置，常用于查看当前IP地址 |
| ping     |          | ping baidu.com | 测试网络的连通性                   |
| shutdown | -r       | shutdown -r    | 先关机，再重启                     |
|          | -h       | shutdown -h    | 关机后不重启                       |
| reboot   |          | reboot         | 重新启动 相当于shutdown -r         |

```什么是进程?
什么是进程?
简单的说,进程就是一个运行的程序.与程序不同的是,程序只是存储在各种存储设备中.程序没有占用除存储外的计算机任何资源.但是,进程,他就占用了计算机的其他资源(如CPU,主存等)
```

| **命令** | **参数** | **示例**    | **说明**                                        |
| -------- | -------- | ----------- | ----------------------------------------------- |
| top      |          | top         | 显示当前系统中耗费资源最多的进程                |
| ps       |          |             | 较少单独使用，配参数根据需求，ps -ef 或者ps-aux |
|          | -e /-A   | ps -e       | 显示所有进程，环境变量                          |
|          | -a       | ps -a       | 显示所有用户的所有进程（包括其它用户）          |
|          | -u       | ps -au      | 按用户名和启动时间的顺序来显示进程              |
|          | -x       | ps -aux     | 显示无控制终端的进程                            |
| kill     | -9       | kill -9 pid | 强制杀死一个进程                                |

**Htop**

Htop是一款运行于Linux系统监控与进程管理软件，用于取代Unix下传统的top。与top只提供最消耗资源的进程列表不同，htop提供所有进程的列表，并且使用彩色标识出处理器、swap和内存状态。

![213917wm845ijmjj04rmpi](https://s2.ax1x.com/2019/10/10/uoIEWT.png)

##### **压缩解压缩**

| **命令** | **参数** | **示例**                                         | **说明**                                                     |
| :------- | :------- | ------------------------------------------------ | ------------------------------------------------------------ |
| gzip     |          | gzip 1.txt                                       | 压缩后面的文件或者文件夹                                     |
|          | -d       | gzip -d 1.txt.gz                                 | 解压后面的压缩文件                                           |
| tar      | -c       | tar -cvf 1.tar 1.txt                             | 建立一个压缩文件的参数指令，例，将1.txt压缩为1.tar，也可指定多个文件或文件夹 |
|          | -x       | tar -xvf 1.tar 1.txt                             | 解开一个压缩文件的参数指令                                   |
|          | -z       | tar -zcvf 1.tar.gz 1.txttar -zxvf 1.tar.gz 1.txt | 是否需要用 gzip ，使用gzip压缩或解压                         |
|          | -v       |                                                  | 压缩的过程中显示文件                                         |
|          | -f       |                                                  | 使用档名，在 f 之后要立即接档名                              |

##### **linux系统常用快捷键及符号命令**

| 命令     | 参数 | 实例 | 说明                      |
| -------- | ---- | ---- | ------------------------- |
| ctrl + c |      |      | 停止进程                  |
| tab      |      |      | 自动补全                  |
| ctrl+d   |      |      | 退出终端/推出root用户登录 |
| *        |      |      | 通配符，指所有            |
| clear    |      |      | 清屏                      |

##### **root管理员权限**

一般情况下,为了系统安全,Linux并不会让我们以超级管理员(root)的身份登陆系统,因为我们很可能面临误操作导致不可挽回的损失,以及保证系统的安全.通常情况下,linux会要求我们以普通用户登录,当我们需要以root权限去进行某些操作的时候,我们可以用sudo命令,去执行某些操作.sudo会要求我们输入当前登录用户的密码.

在`/etc/sudoers`中设置了可执行sudo指令的用户。若其未经授权的用户企图使用sudo，则会发出警告的邮件给管理员。用户使用sudo时，必须先输入密码，之后有5分钟的有效期限，超过期限则必须重新输入密码。

```
sudo(选项)(参数)
-b：在后台执行指令；
-h：显示帮助；
-H：将HOME环境变量设为新身份的HOME环境变量；
-k：结束密码的有效期限，也就是下次再执行sudo时便需要输入密码；。
-l：列出目前用户可执行与无法执行的指令；
-p：改变询问密码的提示符号；
-s<shell>：执行指定的shell；
-u<用户>：以指定的用户作为新的身份。若不加上此参数，则预设以root作为新的身份；
-v：延长密码有效期限5分钟；
-V ：显示版本信息。
```

当然,除了sudo,还有su 也可以获得root权限,但是,我建议你使用sudo.后面有关于sudo和su区别的拓展阅读.

#### Vim编辑器

我们在操作系统上避免不了的就是对文件的编辑,虽然我们在GUI下肯定会有很多好用的编辑器,但是,如果有一天你没有GUI了怎么办?所以,我们需要掌握一个在Linux上很强大的编辑器,他就是,Vim.

vi / vim是Linux上最常用的文本编辑器而且功能非常强大。只有命令，没有菜单，下图表示vi命令的各种模式的切换图。

![646](https://mmbiz.qpic.cn/mmbiz_jpg/tuSaKc6SfPrCdhhPgOiaoBcFPce4tpjykeSGAqQ6vwicJcNf9AtHRpxAb8efawNibqgx2zmkCReVbLYSCuyvXIM6w/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

##### **常用命令**

| i         | 在光标前插入                     |
| --------- | -------------------------------- |
| :wq       | 保存并退出                       |
| :set nu   | 显示行号                         |
| :set nonu | 取消行号                         |
| gg        | 跳到首行                         |
| :n        | 跳到第n行                        |
| u         | undo，取消上一步操作             |
| dd        | 删除光标所在行。ndd删除n行       |
| dG        | 删除光标所在行到末尾行的所以内容 |
| :5,7d     | 删除指定范围的行                 |



### 命令查询工具

#### man

![QQ截图20191009233138](https://s2.ax1x.com/2019/10/10/uoInOJ.png)

男人的确很强悍，给出了这么多提示，但没有我真正想要的。。。还是不知道怎么用。

相信你在技术文章里经常会看到 TL;DR 即Too Long; Didn’t Read. 太长不看， man curl 的内容就是太长了，我不看。

#### tldr

```
npm install -g tldr 安装命令,如果没有npm,请先apt安装npm哦~
tldr tldr 查看tldr的使用方法

```

小试牛刀下

```
$ tldr -p linux tar

  tar

  Archiving utility.
  Often combined with a compression method, such as gzip or bzip.
  More information: .

  - Create an archive from files:
    tar -cf target.tar file1 file2 file3

  - Create a gzipped archive:
    tar -czf target.tar.gz file1 file2 file3

  - Extract an archive in a target directory:
    tar -xf source.tar -C directory

  - Extract a gzipped archive in the current directory:
    tar -xzf source.tar.gz

  - Extract a bzipped archive in the current directory:
    tar -xjf source.tar.bz2

  - Create a compressed archive, using archive suffix to determine the compression program:
    tar -caf target.tar.xz file1 file2 file3

  - List the contents of a tar file:
    tar -tvf source.tar

  - Extract files matching a pattern:
    tar -xf source.tar --wildcards "*.html"
```

嗯，很简洁，直接给出了tar需要的参数.

除了自带的命令，安装的命令也可以

除了node 还有其他版本 https://github.com/tldr-pages/tldr

比如Python，直接pip install tldr安装。

如果你不想安装tldr,也可以直接使用网页在线查看https://tldr.sh/

![647](https://mmbiz.qpic.cn/mmbiz_png/sZeVtjGD4lEEqICFepViayic06hI8cJ6Ff3sia0jQib4gJTC5RN1ibAtCEbv4fADeOpNgfA41icadmTUf5Q9xicklseTQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

有了tldr,妈妈再也不用担心我记不住命令行参数了，还有没有比 tldr更强悍的男人呢，有!

#### cheat

比如cheat https://github.com/cheat/cheat ，直接使用`pip install cheat`安装。

看看 cheat 怎么用吧

```
cheat cheat 产看cheat的使用方法
注意，使用cheat之前需要安装python环境，然后安装pip
```

### 有几句话

上面提到的所有命令,是最常用的命令,可以说掌握了这些东西就基本上可以正常的开始用Linux了.其实这些命令没啥好讲的，但是，最重要的一点，**你千万不能死记硬背**，而应该**用到一个查一个**，逐渐熟练之后自然而然地记住这些用法。



## 尾声

### 总结

第一次上课，很多东西不知道如何去讲比较合适，也不知道你们每个人预习到了哪些地方，也就只能基与我自己的理解和上一届的课件跟你们讲讲linux基础的一些知识。因为linux不管怎么讲，我都没办法再这短短的时间内给你们讲明白，包括我自己，也不能说有多么的了解，只能说是折腾过了，大概入门了。---hhh,我比较菜,这是实话.我希望你们预习我的课件的时候,看到这段时,之前的内容,你们都认真的过了一下.那些命令,也去看了的~

说点儿其他的吧。希望在座的每位朋友，都认真的坚持一些事儿，不关乎你们是否愿意留在红岩网校，不关乎你想去干什么，我第一节课大概就送你们一句话吧：做任何事情切不可浅尝辄止，啥都会一点与啥都不会没什么两样。唯有专心致志与持之以恒的坚持，才能让你在你的道路上渐行渐远。



### 课后作业

#### Level -1.

有一台你自己的Linux机子

#### Level 0.

抽出空余的时间，至少刷完下面链接的阶段1课程，截图检查

https://edu.aliyun.com/roadmap/linux



#### Level 1.

学习Git的用法，注册一个Github账号，并申请学生包以获得一个免费的顶级域名。

使用任何方式 **(不包括宝塔)** 搭建一套属于你自己的博客系统，绑定上一步获取的域名，并将你搭建的过程作为你的第一篇博文上传至你的博客，将博客的地址作为作业提交至我的邮箱。



#### Level 2.

用你的学生邮箱注册一个Jetbrain账号，并下载安装Pycharm专业版与Python 3为今后的学习做准备



#### Level 3.

- 学习先进的Docker，与portainer的使用
- 用docker-compose搓一个lnmp环境，并把你的博客迁移过去
- 截图检查portainer的容器页面

#### Level 4.

- 搭建一个MC服务器，与寝室的小伙伴一起愉快玩耍吧 (提供多人联机与控制台的截图)
- (选做) 选购并配置一台软路由，在提供长期服务的同时，享受愉快的网络环境吧 (交openwrt主界面截图)



### 作业要求

- 所有作业严禁抄袭!!!后果自负~(你可以没有做,你可以没做起,但不要抄,顺便说一句,抄和借鉴是两码事儿)
- level 0 的完成周期为1周
- level 1 的周期为3周
- level 2 请在对应课开始之前完成
- level 3-4 为学期作业,不强制要求,而且你可以在搜索引擎上找到对应的教程 (如果你做起了,请群里@sajo)
- 交作业的方式为邮件,做完后请将你的作业按时发送至 wangziquan@redrock.team
- **以及,发邮件的时候,请简要学习一下邮件礼仪,如有任何问题都可提出,我会抽时间帮你解答.交作业时,请记得将标题取为:**Linux作业\_姓名_学号.
- 大家,好好学习,天天向上!
