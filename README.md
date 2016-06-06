# shell
##简述
Shell 是一种具备特殊功能的程序，他提供了用户与内核进行交互操作的一种接口。她接收用户输入的命令，并把它送入内核去执行。内核是Linux系统的心脏，从开机自检时就驻留在计算机的内存中，直到计算机关闭为止，而用户的应用程序存储在计算机的硬盘上，仅当需要时才被调入内存。Shell是一种应用程序，当用户登录Linux系统时，Shell就会被调入内存执行。Shell独立于内核，它是连接内核和应用程序的桥梁，并由输入设备读取命令，再将其转为计算机可以理解的机械码，Linux内核才能执行该命令。Shell在Linux系统中的位置，如下图：
![enter image description here](http://bizfe.meilishuo.com/md-imgs/941fdce2c97499a267e5da34e195dbbf.png "91747CFA-6C54-410A-AEEA-392E7509C391")

简单点说：在登录到注销期间，输入的每个命令都会经常解译及执行，而这个负责的机制就是Shell.

##Shell的种类
	  [work(0)@yz-lab-675 12:04:57 ~]# ls -l /bin/*sh
	  -rwxr-xr-x. 1 root root 906792 Sep  5  2014 /bin/bash
	  -rwxr-xr-x. 1 root root 106216 Oct 17  2012 /bin/dash
	  lrwxrwxrwx. 1 root root      4 Jun 14  2015 /bin/sh -> bash

**更改使用某种类型的shell:**
**chsh -s 输入新的shell** 		比如：/bin/dash
		       
	[work(0)@yz-lab-675 16:38:36 ~]# chsh -s /bin/dash
	Changing shell for work.
	Password: 
需要用root账号更改:
	
	[root(0)@yz-lab-675 16:44:11 ~]# chsh -s /bin/dash
	Changing shell for root.
	Shell changed. 
生效需要注销重新登录:

	[root(0)@yz-lab-675 16:44:31 ~]# logout  (或exit)
	2014-019deMacBook-Pro:fedev MLS$ relay rdlab root
	# 
	# ls 

**当前的Shell，及当前操作系统的环境变量**

	[work(0)@yz-lab-675 12:12:06 ~]# env
	HOSTNAME=yz-lab-675.meilishuo.com
	TERM=xterm-256color
	SHELL=/bin/bash
	HISTSIZE=1000
	SSH_CLIENT=10.8.1.13 38059 22
	SSH_TTY=/dev/pts/0
	JRE_HOME=/home/service/source/jdk1.7.0_55/jre
	USER=work
	LS_COLORS=rs=0:di=38;5;27:ln=38;5;51:mh=44;38;5;15:pi=40;38;5;11:so=38;5;13:do=38;5;5:bd=48;5;232;38;5;11:cd=48;5;232;38;5;3:or=48;5;232;38;5;9:mi=05;48;5;232;38;5;15:su=48;5;196;38;5;15:sg=48;5;11;38;5;16:ca=48;5;196;38;5;226:tw=48;5;10;38;5;16:ow=48;5;10;38;5;21:st=48;5;21;38;5;15:ex=38;5;34:*.tar=38;5;9:*.tgz=38;5;9:*.arj=38;5;9:*.taz=38;5;9:*.lzh=38;5;9:*.lzma=38;5;9:*.tlz=38;5;9:*.txz=38;5;9:*.zip=38;5;9:*.z=38;5;9:*.Z=38;5;9:*.dz=38;5;9:*.gz=38;5;9:*.lz=38;5;9:*.xz=38;5;9:*.bz2=38;5;9:*.tbz=38;5;9:*.tbz2=38;5;9:*.bz=38;5;9:*.tz=38;5;9:*.deb=38;5;9:*.rpm=38;5;9:*.jar=38;5;9:*.rar=38;5;9:*.ace=38;5;9:*.zoo=38;5;9:*.cpio=38;5;9:*.7z=38;5;9:*.rz=38;5;9:*.jpg=38;5;13:*.jpeg=38;5;13:*.gif=38;5;13:*.bmp=38;5;13:*.pbm=38;5;13:*.pgm=38;5;13:*.ppm=38;5;13:*.tga=38;5;13:*.xbm=38;5;13:*.xpm=38;5;13:*.tif=38;5;13:*.tiff=38;5;13:*.png=38;5;13:*.svg=38;5;13:*.svgz=38;5;13:*.mng=38;5;13:*.pcx=38;5;13:*.mov=38;5;13:*.mpg=38;5;13:*.mpeg=38;5;13:*.m2v=38;5;13:*.mkv=38;5;13:*.ogm=38;5;13:*.mp4=38;5;13:*.m4v=38;5;13:*.mp4v=38;5;13:*.vob=38;5;13:*.qt=38;5;13:*.nuv=38;5;13:*.wmv=38;5;13:*.asf=38;5;13:*.rm=38;5;13:*.rmvb=38;5;13:*.flc=38;5;13:*.avi=38;5;13:*.fli=38;5;13:*.flv=38;5;13:*.gl=38;5;13:*.dl=38;5;13:*.xcf=38;5;13:*.xwd=38;5;13:*.yuv=38;5;13:*.cgm=38;5;13:*.emf=38;5;13:*.axv=38;5;13:*.anx=38;5;13:*.ogv=38;5;13:*.ogx=38;5;13:*.aac=38;5;45:*.au=38;5;45:*.flac=38;5;45:*.mid=38;5;45:*.midi=38;5;45:*.mka=38;5;45:*.mp3=38;5;45:*.mpc=38;5;45:*.ogg=38;5;45:*.ra=38;5;45:*.wav=38;5;45:*.axa=38;5;45:*.oga=38;5;45:*.spx=38;5;45:*.xspf=38;5;45:
	SSH_AUTH_SOCK=/tmp/ssh-kdDby14317/agent.14317
	MAVEN_HOME=/home/service/source/apache-maven-3.3.3
	MAIL=/var/spool/mail/work
	PATH=/home/service/source/apache-maven3.3.3/bin:/home/service/source/go/bin:/home/service/source/jdk1.7.0_55/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/work/bin
	PWD=/home/work
	JAVA_HOME=/home/service/source/jdk1.7.0_55
	LANG=en_US.UTF-8
	HISTCONTROL=ignoredups
	SHLVL=1
	HOME=/home/work
	GOROOT=/home/service/source/go
	LOGNAME=work
	CVS_RSH=ssh
	CLASSPATH=.:/home/service/source/jdk1.7.0_55/lib/dt.jar:/home/service/source/jdk1.7.0_55/lib/tools.jar
	SSH_CONNECTION=10.8.1.13 38059 10.8.250.194 22
	LESSOPEN=|/usr/bin/lesspipe.sh %s
	RELAY_USER=ningli
	G_BROKEN_FILENAMES=1
	_=/bin/env 

##Shell脚本
文件的第一行必须是“#!/bin/bash”，“#！”符号成为“Sha-bang”符号，是Shell脚本的其实符号，“#！”符号是指定一个文件类型的特殊标记，它告诉Linux系统这个文件的执行需要指定一个解析器。“#！”符号之后是一个路径名，这个路径名指明了解释器在系统中的位置，对于一般的Shell脚本而言，解释器是bash，也可以是sh，即：#/bin/bash 
或 #!/bin/sh

	[work(0)@yz-lab-675 12:21:52 ~]# cat first.sh
	#!/bin/bash  #-----符号#!用来告诉系统它后面的参数是用来执行该文件的程序
	hostname
	date
	who
	[work(0)@yz-lab-675 12:21:56 ~]# sh first.sh 
	yz-lab-675.meilishuo.com
	Fri Mar 18 12:22:00 CST 2016
	work     pts/0        2016-03-18 10:18 (10.8.1.13)
