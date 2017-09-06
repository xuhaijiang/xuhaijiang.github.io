#### Linux

**Linux：** 是一套免费使用和自由传播的类Unix操作系统内核。

**GNU：** 英语：GNU General Public License，缩写：GNU GPL、GPL，是一个自由软件许可协议条款

##### 推荐书

- **系统自带的文档**

- 一本好入门教材 -> 一本linux指令参考手册 -> linux系统管理手册 -> 讲解linux系统原理的书

##### 版本
- 内核版本
    - Linux内核版本号的格式是x.y.zz-www
- 发行版版本
    - 发行版本号由各个发行公司或者组织制定
        - Redhat Linux
        - Mandrake Linux
        - SUSE Linux
        - 红旗 Linux

*Debian GNU/Linux是一套非常特殊的Linux发行版*

##### 常用网址

- 国外
    - [kernel.org](http://www.kernel.org)
    - [linux.com](http://linux.com)
    - [linux.org](http://www.linux.org)
    - [linuxhelp.org](http://www.linuxhelp.org)
- 国内
    - [linuxforum.net](http://www.linuxforum.net)
    - [linuxfans.org](http://www.linuxfans.org)
    - [linuxaid.com.cn](http://www.linuxaid.com.cn)

##### 基础知识

###### Linux 目录
 
- **bin** 存放Linux常用命令
- **boot** 存放系统启动时要用到的程序
- **dev** 包含Linux系统需使用的所有外部设备，例如键入`cd /dev/mouse` 即可查看鼠标相关文件
- **cdrom** 刚安装完系统时是空的，你可以将光驱文件系统挂在这个目录下，例如键入`mount /dev/cdrom /cdrom`
- **etc** 存放系统的各种配置文件和子目录，例如网络配置文件、文件系统、X系统配置文件、设备配置信息、设置用户信息等
- **sbin** 存放系统管理员的系统管理程序
- **home** 当建立用户xxx时，那么在/home目录下就会有对应的`/home/xxx`路径，用来存放用户的主目录
- **lib** 存放系统动态链接库
- **mnt** 刚安装完系统时是空的,你可以临时将别的文件系统挂在该目录下
- **proc** 可以在该目录下获取系统信息
- **root** 超级用户的主目录
- **tmp** 存放程序执行时产生的临时文件
- **usr** 存放用户的应用程序和文件


