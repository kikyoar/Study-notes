<center><font color=#D87093>Linux命令行和shell脚本编程大全知识点</font></center>
========================================
<center>第一部分        Linux命令行</center>
----------------------------------------

<p align = "right" >人没有牺牲就什麽都得不到，为了得到什麽东西，就需要付出同等的代价</p>
* Linux 文件系统
```
ext                     扩展文件系统，最早的Linux文件系统
ext2                    第二扩展文件系统，在ext的基础上提供了更多的功能
ext3                    第三扩展文件系统，支持日志功能
ext4                    第四扩展文件系统，支持高级日志功能
hpfs                    OS/2高性能文件系统
jfs                     IBM日志文件系统
iso9660                 ISO 9660文件系统（CD-ROM）
minix                   MINIX文件系统
msdos                   微软的FAT16          
ncp                     Netware文件系统
nfs                     网络文件系统
ntfs                    支持Mircrosoft NT文件系统
proc                    访问系统信息
ReiserFS                高级Linux文件系统，能提供更好的性能和硬盘恢复功能
smb                     支持网络访问的Samba SMB文件系统
sysv                    较早期的Unix文件系统
ufs                     BSD文件系统
umsdos                  建立在msdos上的类Unix文件系统
vfat                    Windows 95文件系统（FAT32）
XFS                     高性能64位日志文件系统
```

* 常见的Linux目录名称
```
/                       虚拟目录的根目录。通常不会再这里存储文件
/bin                    二进制目录，存放许多用户级的GNU工具
/boot                   启动目录，存放启动文件
/dev                    设备目录，Linux在这里创建设备节点
/etc                    系统配置文件目录
/home                   主目录，Linux在这里创建用户目录
/lib                    库目录，存放系统和应用程序的库文件
/media                  媒体目录，可移动媒体设备的常用挂载点
/mnt                    挂载目录，另一个可移动媒体设备的常用挂载点
/opt                    可选目录，常用于存放第三方软件包和数据文件
/proc                   进程目录，存放现有硬件及当前进程的相关信息
/root                   root用户的主目录
/sbin                   系统二进制目录，存放许多GNU管理员级工具
/run                    运行目录，存放系统运作时的运行时数据
/srv                    服务目录，存放本地服务的相关文件
/sys                    系统目录，存放系统硬件信息的相关文件
/tmp                    临时目录，可以在该目录中创建和删除临时工作文件
/usr                    用户二进制目录，大量用户级的GNU工具和数据文件都存储在这里
/var                    可变目录，用以存放经常变化的文件，比如日志文件

```

* 基本的 bash shell命令
<blockquote>
      - <b>Man</b>:&emsp;&emsp;&emsp;&emsp;```用来访问存储在Linux系统上的手册页面```
      - <b>ls</b>:<blockquote>ls -F:&emsp;&emsp;&emsp;```-F 参数在目录名后加了正斜线（/），方便用户在输出中辨认它们``` </blockquote>
                  <blockquote>ls -R:&emsp;&emsp;&emsp;```-R 参数列出了当前目录下包含的子目录中的文件``` </blockquote>
                  <blockquote>ls -l:&emsp;&emsp;&emsp;```-l 参数每一行都包含了关于文件（或目录）的下述信息：``` 
                              <blockquote>```文件类型，不如目录(d)、文件（-）、字符型文件（c）或块设备（b）；``` </blockquote>
                              <blockquote>```文件的权限；``` </blockquote>
                              <blockquote>```文件硬连接总数；``` </blockquote>
                              <blockquote>```文件属主的用户名；``` </blockquote>
                              <blockquote>```文件属主的组名；``` </blockquote>
                              <blockquote>```文件的大小（以字节为单位）；``` </blockquote>
                              <blockquote>```文件的上次修改时间；``` </blockquote>
                              <blockquote>```文件名或目录名；``` </blockquote>
                        </blockquote>
                  <blockquote>```过滤输出列表``` 
                              <blockquote>```问号（？）代表一个字符；``` </blockquote>
                              <blockquote>```星号（*）代表零个或多个字符。``` </blockquote>
                              </blockquote>
      - <b>touch</b>:&emsp;&emsp;&emsp;&emsp;```创建新文件，也可以用来改变文件的修改时间，这个操作不改变文件的内容```
      - <b>cp</b>:&emsp;&emsp;&emsp;&emsp;
                 <blockquote>cp -i:&emsp;&emsp;&emsp;```-i 参数强制shell询问是否需要覆盖已有文件``` </blockquote> 
                 <font color=#D87093>cp &emsp;-i &emsp; /etc/nginx.conf &emsp; .(其中这个.表示当前目录，..表示上一级目录)</font>
                 <p></p>
                 <blockquote>cp -R:&emsp;&emsp;&emsp;```-R 参数递归地复制整个目录的内容``` </blockquote>   
                 <font color=#D87093>也可以在cp命令中使用通配符</font>
                 <p></p>
      - <b>mv</b>:&emsp;&emsp;&emsp;&emsp;```移动文件，mv只影响文件名和位置，inode编号和时间戳保持不变，也可以使用-i，覆盖已有文件时，得到提示```
      - <b>mkdir</b>:&emsp;&emsp;&emsp;&emsp;```-p参数可以根据需要创建缺失的父目录，父目录包含目录树中下一级目录的目录```
      - <b>rmdir</b>:&emsp;&emsp;&emsp;&emsp;```rmdir命令只删除空目录，rm可删除非空目录```
      - <b>file</b>:&emsp;&emsp;&emsp;&emsp;```file命令能够探测文件的内部，并决定文件是什么类型的```   
      - <b>cat</b>:&emsp;&emsp;&emsp;&emsp;```显示文本中所有数据```
      		<blockquote>cat -n:&emsp;&emsp;&emsp;```-n 参数会给所有的行加上行号``` </blockquote>
      		<blockquote>tac -n:&emsp;&emsp;&emsp;```文本数据倒叙``` </blockquote>     
      - <b>less</b>:&emsp;&emsp;&emsp;&emsp;```less比more命令高级，less可以识别上下键以及上下翻页键```
      - <b>tail</b>:&emsp;&emsp;&emsp;&emsp;```tail和head命令中可以加入-n参数来修改所显示的行数```
      		<p></p>
      		<font color=#D87093>tail -f：tail命令会保持活动状态，并不断显示添加到文件中的</font> 
      		<p></p>
      - <b>ps</b>:&emsp;&emsp;&emsp;&emsp;```输出运行在系统上的所有程序的许多信息```
    		<blockquote>ps -ef:&emsp;&emsp;&emsp;```-e参数指定显示所有运行在系统上的进程；-f参数则扩展了输出，扩展信息如下：``` 
                              <blockquote>```UID：启动这些进程的用户；``` </blockquote>
                              <blockquote>```PID：进程的进程ID；``` </blockquote>
                              <blockquote>```PPID：父进程的进程号（如果该进程是由另一个进程启动的）；``` </blockquote>
                              <blockquote>```C: 进程生命周期中的CPU利用率；``` </blockquote>
                              <blockquote>```STIME：进程启动时的系统时间；``` </blockquote>
                              <blockquote>```TTY: 进程启动时的终端设备；``` </blockquote>
                              <blockquote>```TIME：运行进程需要的累积CPU时间；``` </blockquote>
                              <blockquote>```CMD: 启动的程序名称；``` </blockquote>
                        </blockquote>
      - <b>top</b>:&emsp;&emsp;&emsp;&emsp;```实时显示系统进程信息```
    		<blockquote>top:&emsp;&emsp;&emsp;```“q”退出查看；扩展信息如下：``` 
                              <blockquote>```PID：进程的ID；``` </blockquote>
                              <blockquote>```USER：进程属主的名字；``` </blockquote>
                              <blockquote>```PR：进程的优先级；``` </blockquote>
                              <blockquote>```NI: 进程的谦让度值；``` </blockquote>
                              <blockquote>```VIRT：进程占用的虚拟内存总量；``` </blockquote>
                              <blockquote>```RES: 进程占用的物理内存总量；``` </blockquote>
                              <blockquote>```SHR：进程和其他进程共享的内存总量；``` </blockquote>
                              <blockquote>```S: 进程的状态（D代表可中断的休眠状态，R代表在运行状态，S代表休眠状态，T代表跟踪状态或停止状态，Z代表僵化状态）；``` </blockquote>
                              <blockquote>```%CPU：进程使用的CPU时间比例；``` </blockquote>
                              <blockquote>```%MEM：进程使用的内存占可用内存的比例；``` </blockquote>
                              <blockquote>```TIME+：自进程启动到目前为止的CPU时间总量；``` </blockquote>
                              <blockquote>```COMMAND：进程所对应的命令行名称，也就是启动的程序名；``` </blockquote>
                        </blockquote>       
      - <b>kill</b>:&emsp;&emsp;&emsp;&emsp;```进程的属主或root用户可通过进程ID（PID）给进程发TERM信号（尽可能终止）```
      		<blockquote>kill -s:&emsp;&emsp;&emsp;```-s 参数支持指定其他信号（HUP挂起，INT中断，QUIT结束运行，TSTP停止或暂停，但继续在后台运行）``` </blockquote>
      		<blockquote>killall:&emsp;&emsp;&emsp;```通过进程名而不是PID来结束进程，killall也支持通配符``` </blockquote> 
      - <b>mount</b>:&emsp;&emsp;&emsp;&emsp;```输出当前系统上的挂载列表，以下为参数：```
            <blockquote>mount -a:&emsp;&emsp;&emsp;```-a 参数挂载/etc/fstab文件中指定的所有的文件系统``` </blockquote>
            <blockquote>mount -f:&emsp;&emsp;&emsp;```-f 参数模拟挂载设备，但并不真正的挂载``` </blockquote> 
      - <b>umount</b>:&emsp;&emsp;&emsp;&emsp;```通过设备文件或者是挂载点来指定要卸载的设备，如果有程序使用，则不能卸载```
            <p></p>
            <font color=#D87093>如果在卸载设备时，系统提示设备正忙，可用lsof命令获得使用它的进程信息，然后在应用中停止使用该设备或停止该进程，lsof命令名单：lsof&emsp;/path/to/device/node，或 lsof&emsp;/path/to/mount/point</font> 
            <p></p> 
      - <b>df</b>:&emsp;&emsp;&emsp;&emsp;```可以查看所有已挂载磁盘的使用情况```
      - <b>du</b>:&emsp;&emsp;&emsp;&emsp;```显示某个特定目录的磁盘使用情况：以下为常用参数：```
            <blockquote>du -c:&emsp;&emsp;&emsp;```-c 参数显示所有已列出文件总的大小```</blockquote>
            <blockquote>du -h:&emsp;&emsp;&emsp;```-h 参数按用户易读的格式输出，K代替千字节，M兆字节，G吉字节```</blockquote> 
            <blockquote>du -s:&emsp;&emsp;&emsp;```-s 参数显示每个输出参数的总计```</blockquote>   
      - <b>sort</b>:&emsp;&emsp;&emsp;&emsp;```对数据进行排序,以下为常用参数：```
            <blockquote>sort -n:&emsp;&emsp;&emsp;```-n sort命令把数字识别为数字而不是字符，并且按值排序```</blockquote>
            <blockquote>sort -M:&emsp;&emsp;&emsp;```-M 参数能识别三字符的月份名，并相应的排序```</blockquote> 
            <blockquote>sort -k:&emsp;&emsp;&emsp;```-k 参数排序从POS1位置开始，如果指定了POS2的话，到POS2的位置结束```</blockquote>
            <blockquote>sort -t:&emsp;&emsp;&emsp;```-t 参数指定一个用来区分键位置的字符```</blockquote>
            <blockquote>sort -r:&emsp;&emsp;&emsp;```-r 参数反序排序（升序变为降序）```</blockquote>
            <p></p>
            <font color=#D87093>-k和-t参数排序比较有用，对/etc/passwd根据用户ID进行数值排序，可以：sort -t ':' -k 3 -n /etc/passwd，这个命令的意思为数据已经按照第三个字段---用户ID的数值排序</font> 
            <p></p> 
            <font color=#D87093>du -sh * | sort -nr意思为目录下的哪些文件占用最多</font> 
            <p></p>
      - <b>grep</b>:&emsp;&emsp;&emsp;&emsp;```在指定的文件中查找包含匹配指定模式的字符的行，grep的输出就是包含了匹配的行，以下为常用参数：```
            <blockquote>grep -v:&emsp;&emsp;&emsp;```-v 参数是进行反向搜索（输出不匹配该模式的行）```</blockquote>
            <blockquote>grep -n:&emsp;&emsp;&emsp;```-n 参数显示匹配模式的行所在的行号```</blockquote> 
            <blockquote>grep -c:&emsp;&emsp;&emsp;```-c 参数只要知道有多少行含有匹配的模式```</blockquote>
            <blockquote>grep -e:&emsp;&emsp;&emsp;```-e 参数指定多个匹配模式，eg：grep -e t -e f file1，输出含有字符t或字符f的所有行```</blockquote>
      - <b>压缩数据</b>:&emsp;&emsp;&emsp;&emsp;```常用压缩工具，bzip2、gzip、zip：```
            <blockquote>gzip:&emsp;&emsp;&emsp;```用来压缩文件```</blockquote>
            <blockquote>gzcat:&emsp;&emsp;&emsp;```用来查看压缩过的文本文件的内容```</blockquote> 
            <blockquote>gunzip:&emsp;&emsp;&emsp;```用来解压文件```</blockquote>
      - <b>tar</b>:&emsp;&emsp;&emsp;&emsp;
            <blockquote>tar -c:&emsp;&emsp;&emsp;```-c 创建一个新的tar归档文件```</blockquote>
            <blockquote>tar -r:&emsp;&emsp;&emsp;```-r 追加文件到已有tar归档文件末尾```</blockquote>
            <blockquote>tar -t:&emsp;&emsp;&emsp;```-t 列出已有tar归档文件的内容```</blockquote>
            <blockquote>tar -f:&emsp;&emsp;&emsp;```-f 输出结果到文件或设备```</blockquote>
            <blockquote>tar -j:&emsp;&emsp;&emsp;```-j 将输出重定向给bzip2命令来压缩内容```</blockquote>
            <blockquote>tar -z:&emsp;&emsp;&emsp;```-z 将输出重定向给gzip命令来压缩内容```</blockquote> 
            <blockquote>tar -z:&emsp;&emsp;&emsp;```-v 在处理文件时显示文件```</blockquote>     
</blockquote>

    * 理解shell
<blockquote>
         - <b>shell的类型</b>:&emsp;&emsp;&emsp;&emsp;```系统启动什么样的shell程序取决于个人的用户ID配置```
         - <b>shell的父子关系</b>:&emsp;&emsp;&emsp;&emsp;```父shell发出命令：bash，创建子shell，子shell发出命令：ps -ef，子shell的父进程ID和原始进程ID一致，也就是运行shell脚本也能创建出子shell```
         - <b>进程列表</b>:&emsp;&emsp;&emsp;&emsp;```可以在一行中指定要运行的一系列命令。可以通过命令列表实现，只要在命令之间加入分号（；）即可。若要成为进程列表，则这些命令必须包含在括号里，比如（pwd；ls；cd /etc；pwd；cd；pwd；ls），其括号内的命令为子shell```
         - <b>sleep</b>:&emsp;&emsp;&emsp;&emsp;```sleep命令接受一个参数，希望进程等待睡眠的秒数，若将命令置于后台模式，可以在命令末尾加上字符&；sleep 3000&：sleep命令会在后台睡眠3000秒；将进程列表置于后台（tar -cf Rich.tar /home/rich; tar -cf My.tar /home/christine)&```
         - <b>外部命令</b>:&emsp;&emsp;&emsp;&emsp;```有时候也叫文件系统命令，是存在于bash shell之外的程序，外部命令程序通常位于/bin、/usr/bin、/sbin或/usr/sbin中；ps就是一个外部命令，可以使用which和type命令找到```
         - <b>内建命令</b>:&emsp;&emsp;&emsp;&emsp;```内建命令不需要子进程来执行，它们已经和shell编译成了一体。cd和exit命令内建于bash shell.echo和pwd既有内建命令也有外部命令```
</blockquote>
        * 使用Linux环境变量
      <blockquote>
            - <b>环境变量</b>:&emsp;&emsp;&emsp;&emsp;```bash shell用环境变量的特性来存储有关shell会话和工作环境的信息，分为全局变量和局部变量```
             <blockquote>全局环境变量&emsp;&emsp;&emsp;```可以使用echo显示变量的值，引用某个变量的值前面$，也能够让变量作为命令行参数，比如ls $HOME，全局环境变量可用于进程的所有子shell```</blockquote>
            <p></p>
            <font color=#D87093>系统环境变量基本上都使用全大写字母，以区别于普通用户的环境变量，要查看环境变量，可以使用env或printenv命令，要显示个别环境变量的值，可以使用printenv命令，不要用env命令，比如printenv SHELL</font> 
            <p></p>
            <blockquote>局部环境变量&emsp;&emsp;&emsp;```只能在定义它们的进程中可见，set命令会显示为某个特定进程设置的所有环境变量，包括全局变量、局部变量以及用户定义变量```</blockquote>
            - <b>设置局部用户定义变量</b>:&emsp;&emsp;&emsp;&emsp;```通过等号给环境变量赋值，值可以是数值或字符串```
            <p></p>
            <font color=#D87093>自己创建的局部变量或者是shell脚本，使用小写字母；变量名、等号和值之间没有空格</font> 
            <p></p>
            - <b>设置全局环境变量</b>:&emsp;&emsp;&emsp;&emsp;```创建方法是先创建一个局部环境变量，然后再把它导出到全局环境中；这个过程通过export命令来完成，变量名前面不需要加$```
            <p></p>
            <font color=#D87093>修改子shell中全局环境变量并不会影响到父shell中该变量的值，子shell甚至无法使用export命令改变父shell中全局环境变量的值</font> 
            <p></p>
            - <b>删除环境变量</b>:&emsp;&emsp;&emsp;&emsp;```使用unset命令完成，在unset命令中引用环境变量时，不要使用$```
            <p></p>
            <font color=#D87093>如果要使用变量，使用$；如果要操作变量，不使用$。这个规则例外就是使用printenv显示某个变量的值</font>
            <p></p>
            - <b>设置PATH环境变量</b>:&emsp;&emsp;&emsp;&emsp;```PATH环境变量定义了用于进行命令和程序查找的目录```
            <p></p>
            <font color=#D87093>PATH中各个目录之间使用冒号分隔的，只需引用原来的PATH值，然后再给这个字符串添加新目录就可以了，对于PATH变量的修改只能持续到退出或重启系统</font>
            <p></p>
            - <b>定位系统环境变量</b>:&emsp;&emsp;&emsp;&emsp;```bash检查的启动文件取决于启动bash shell的方式```
            <blockquote>登录shell:&emsp;&emsp;&emsp;```登录shell从5个不同的启动文件里读取命令：/etc/profile、$HOME/.bash_profile、$HOME/.bashrc、$HOME/.bash_login、$HOME/.profile、```</blockquote>
            <blockquote>交互式shell进程:&emsp;&emsp;&emsp;```如果bash是作为交互式shell启动的，它就不会访问/etc/profile文件，只会检查用户HOME目录中的.bashrc文件（一是查看/etc目录下通用的bashrc文件，二是为用户提供一个定制自己的命名别名和私有脚本函数的地方）```</blockquote>
            <blockquote>非交互式shell:&emsp;&emsp;&emsp;```系统执行shell脚本时用的就是这种shell，不同的地方在于它没有命令提示符```</blockquote>
             - <b>数组变量</b>:&emsp;&emsp;&emsp;&emsp;```要给某个环境变量设置多个值，可以把值放在括号里，值于值之间用空格分隔```
      </blockquote>
               * Linux文件权限
            <blockquote>
                   - <b>/etc/passwd文件</b>:&emsp;&emsp;&emsp;&emsp;```/etc/passwd文件的字段包含如下信息：登录用户名、用户密码（用*表示）、用户账户的UID、用户账号的组ID、用户账户的文本描述、用户HOME目录的位置、用户的默认shell```
                   - <b>/etc/shadow文件</b>:&emsp;&emsp;&emsp;&emsp;```/etc/shadow文件对Linux系统密码管理提供了更多的控制，只有root才能访问/etc/shadow，每条记录中都有9个字段：与/etc/passwd文件中的登录名字段对应的登录名、加密后的密码、自上次修改后的天数密码（自1970年1月1日开始计算）、多少天后才能更改密码、多少天后必须更改密码、密码过期前提前多少提醒用户更改密码、密码过期后多少天禁用用户账户、用户账户被禁用的日期（自1970年1月1日到当天的天数表示）、预留字段给将来使用``` 
                   - <b>添加新用户</b>:&emsp;&emsp;&emsp;&emsp;```使用useradd -D显示创建用户的默认值，其中/etc/ske1目录下的内容会被复制到用户的HOME目录下，以下是命令行参数：```  
                     <blockquote>-c:&emsp;&emsp;&emsp;```给新用户添加备注```</blockquote> 
                     <blockquote>-d:&emsp;&emsp;&emsp;```为主目录指定一个名字（如果不想用登录名作为主目录名的话）```</blockquote>
                     <blockquote>-e:&emsp;&emsp;&emsp;```用YYYY-MM-DD格式指定一个账户过期的日期```</blockquote>
                     <blockquote>-f:&emsp;&emsp;&emsp;```指定这个账户密码过期后多少天被禁用，0表示已过期就禁用，-1表示禁用这个功能```</blockquote>
                     <blockquote>-g:&emsp;&emsp;&emsp;```指定用户登录组的GID或组名```</blockquote>
                     <blockquote>-G:&emsp;&emsp;&emsp;```指定用户除登录组外所属一个或多个附加组```</blockquote>
                     <blockquote>-m:&emsp;&emsp;&emsp;```创建用户的HOME目录```</blockquote>
                     <blockquote>-M:&emsp;&emsp;&emsp;```不创建用户的HOME目录```</blockquote>
                     <blockquote>-n:&emsp;&emsp;&emsp;```创建一个与用户登录名同名的新组```</blockquote>
                     <blockquote>-r:&emsp;&emsp;&emsp;```创建系统账户```</blockquote>
                     <blockquote>-p:&emsp;&emsp;&emsp;```为用户账户指定默认密码```</blockquote>
                     <blockquote>-s:&emsp;&emsp;&emsp;```指定用户使用的登录SHELL```</blockquote>
                     <blockquote>-u:&emsp;&emsp;&emsp;```为账户指定唯一的UID```</blockquote>
                  <p></p>
                  <font color=#D87093>可以使用useradd更改默认值，参数为-b：更改默认的创建用户HOME目录的位置、-e：更改默认新账户的过期日期、-f：更改默认的新用户从密码过期到账户禁用的天数、-g：更改默认的组名称或GID、-s：更改默认的登录shell。用法如：useradd -D -s /bin/tsch</font> 
                  <p></p>
                  - <b>删除用户</b>:&emsp;&emsp;&emsp;&emsp;```使用userdel命令只会删除/etc/passwd文件中的用户信息，而不会删除系统中属于该账户的任何文件```
                  <p></p>
                  <font color=#D87093>如果加上-r参数，userdel会删除用户的HOME目录以及邮件目录</font> 
                  <p></p>
                  - <b>修改用户</b>:&emsp;&emsp;&emsp;&emsp;``` ```
                     <blockquote>usermod:&emsp;&emsp;&emsp;```修改用户账户的字段，-c修改备注、-e修改过期日期、-g修改默认的登录组```</blockquote> 
                     <font color=#D87093>其中-l修改用户的登录名、-L锁定账户、-p修改账户的密码、-U解除锁定</font> 
                     <blockquote>passwd和chpasswd:&emsp;&emsp;&emsp;```passwd -e强制用户下次登录时修改密码、可以重定向命令来将含有userid:passwd对的文件重定向给chpasswd，例如chpasswd < user.txt```</blockquote>
                     <blockquote>chsh、chfn和chage:&emsp;&emsp;&emsp;```chsh命令用来快速修改默认的用户登录shell，例如chsh -s /bin/csh test；chfn用于修改/etc/passwd文件的备注字段；chage命令用来管理用户账户的有效期```</blockquote>
                  - <b>/etc/group文件</b>:&emsp;&emsp;&emsp;&emsp;```系统用户用的GID低于500，而用户组的GID从500开始，/etc/group文件有4个字段：组名、组密码、GID、属于改组的用户列表```
                  <p></p>
                  <font color=#D87093>当一个用户在/etc/passwd文件中指定某个组作为默认组时，用户账户不会作为该组成员再出现在/etc/group中</font> 
                  <p></p>
                  - <b>创建新组</b>:&emsp;&emsp;&emsp;&emsp;```在创建新组时，默认没有用户被分配到该组，使用（usermod -G 组  用户）这种方式添加```
                  <p></p>
                  <font color=#D87093>如果更改了已登录系统账户所属的用户组，需登录系统后再登录才生效。如果加了-g选项，指定的组名会替换掉该账户的默认组。-G选项则将该组添加到用户的属组的列表里，不影响默认组</font>
                  - <b>修改组</b>:&emsp;&emsp;&emsp;&emsp;```groupmod可以修改已有组的GID（-g选项）或组名（-n选项），修改组名时，GID和组成员不会变，只有组名改变```
                  - <b>使用文件权限符</b>:&emsp;&emsp;&emsp;&emsp;```-代表文件、d代表目录、l代表链接、c代表字符型设备、b代表块设备、n代表网格设备；rwxrwxrwx代表文件的属主、属组、其他用户权限```
                  - <b>默认文件权限</b>:&emsp;&emsp;&emsp;&emsp;```umask命令设置所创建文件和目录的默认权限，要把umask值从对象的全权限值中减掉，对文件来说，全权限的值为666（所有用户都有读写权限）；对于目录来说，则是777（所有用户都有读、写、执行权限），减去umask022，剩下的则为文件权限默认644，目录权限默认755```
                  - <b>改变权限</b>:&emsp;&emsp;&emsp;&emsp;```chmod命令用来改变文件和目录的安全性设置，chmod 760 newfile或者是chmod o+r newfile```
                  <p></p>
                  <font color=#D87093>ls命令的-F选项，能够在具有执行权限的文件名后加一个星号，chmod -R可以让权限的改变递归地作用到文件和子目录</font> 
                  <p></p>
                  - <b>改变所属关系</b>:&emsp;&emsp;&emsp;&emsp;```chown命令用来改变文件的属主，也支持改变属主（chown dan.shared newfile），chgrp命令用来改变文件的默认属组```
                  <p></p>
                  <font color=#D87093>chown -R可以让权限的改变递归地作用到文件和子目录；-h可以改变文件的所有符号链接文件的所属关系</font> 
                  <p></p>                
            </blockquote>

                  * Linux文件系统
               <blockquote>
                     - <b>fdisk</b>:&emsp;&emsp;&emsp;&emsp;```管理安装在系统上的任何存储设备上的分区：```
                     <blockquote>-a:&emsp;&emsp;&emsp;```设置活动分区标志```</blockquote>
                     <blockquote>-d:&emsp;&emsp;&emsp;```删除分区```</blockquote> 
                     <blockquote>-l:&emsp;&emsp;&emsp;```显示可以的分区类型```</blockquote>
                     <blockquote>-n:&emsp;&emsp;&emsp;```添加一个新分区```</blockquote> 
                     <blockquote>-p:&emsp;&emsp;&emsp;```显示当前分区表```</blockquote>   
                     <blockquote>-t:&emsp;&emsp;&emsp;```修改分区的系统ID```</blockquote>   
                     <blockquote>-u:&emsp;&emsp;&emsp;```改变使用的存储单位```</blockquote> 
                     <blockquote>-v:&emsp;&emsp;&emsp;```验证分区表```</blockquote> 
                     <blockquote>-w:&emsp;&emsp;&emsp;```将分区表写入磁盘```</blockquote> 
                     <p></p>
                     <font color=#D87093>有些发行版生成新分区后并不会自动提醒Linux系统，使用partprob或hdparm命令，或者重启系统，让系统读取更新过得分区表</font> 
                     <p></p>
                      - <b>创建文件系统</b>:&emsp;&emsp;&emsp;&emsp;```在将数据存储到分区之前，必须使用某种文件系统对其进行格式化：mkfs.ext4、mkfs.ext3、mkfs.xfs、mkfs.zfs```
                      - <b>文件系统的检查与修复</b>:&emsp;&emsp;&emsp;&emsp;```fsck命令能够检查和修复大部分类型的Linux文件系统```
                     <blockquote>-a:&emsp;&emsp;&emsp;```如果检测到错误，自动修复文件系统```</blockquote>
                     <blockquote>-A:&emsp;&emsp;&emsp;```检查/etc/fstab文件中列出的所有文件系统```</blockquote> 
                     <blockquote>-r:&emsp;&emsp;&emsp;```出现错误时提示```</blockquote>
                     <blockquote>-V:&emsp;&emsp;&emsp;```在检查时产生详细输出```</blockquote> 
                      <p></p>
                      <font color=#D87093>只能在为挂载的文件系统上运行fsck命令，对大多数文件系统来说，只需卸载文件系统来进行检查，检查完后重新挂载即可。因为根文件系统含有所需核心的Linux命令和日志文件，所以无法再处于运行状态的系统上卸载它。这样的话需要Linux LiveCD，使用LiveCD启动系统，然后在根文件系统上运行fsck命令</font> 
                      <p></p>
                      - <b>Linux中的LVM</b>:&emsp;&emsp;&emsp;&emsp;```允许在Linux上使用简单的命令行命令来管理一个完整的逻辑卷管理环境```
                     <blockquote>快照:&emsp;&emsp;&emsp;```创建在线逻辑卷的可读写快照，这个功能对快速故障转移或设计修改数据的程序试验（如果失败，需要恢复修改过的数据）非常有用```</blockquote>
                     <blockquote>条带化：&emsp;&emsp;&emsp;```有助于提高硬盘的性能，因为Linux可以将一个文件的多个数据块同时写入多个硬盘，而无需等待单个硬盘移动读写磁头到多个不同位置。这个改进同样适用于读取顺序访问的文件，因为LVM可同时从多个硬盘读取数据```</blockquote>
                      <p></p>
                      <font color=#D87093>LVM条带化不同于RAID条带化，LVM条带化不提供用来创建容错环境的校样信息。事实上，LVM条带化会增加文件因硬盘故障而丢失的概率。单个硬盘故障可能会造成多个逻辑卷无法访问</font> 
                      <p></p>
                     <blockquote>镜像:&emsp;&emsp;&emsp;```镜像是一个实时更新的逻辑卷的完整副本，当你创建镜像逻辑卷时，LVM会将原始逻辑卷同步到镜像副本中。一旦原始同步完成，LVM会为文件系统的每次写操作执行两次写入------一次写入到主逻辑卷，一次写入到镜像副本```</blockquote>
                     - <b>使用LVM</b>:&emsp;&emsp;&emsp;&emsp;``` ```
                     <blockquote>定义物理卷:&emsp;&emsp;&emsp;```在创建了基本的Linux分区后，使用t命令改变分区类型；使用pvcreate命令创建实际的物理卷，pvdisplay显示已创建的物理卷列表```</blockquote>
                     <blockquote>创建卷组:&emsp;&emsp;&emsp;```使用vgcreate创建卷组，使用vgdisplay命令来显示新创建的卷组的细节```</blockquote> 
                     <blockquote>创建逻辑卷:&emsp;&emsp;&emsp;```使用lvcreate来创建逻辑卷，使用lvdisplay命令来查看创建的逻辑卷的详细情况```</blockquote>
                     <p></p>
                      <font color=#D87093>-c指定快照逻辑卷的单位大小、-l指定分配给新逻辑卷的逻辑区段数，或者要用的逻辑区段的百分比、-L指定分配给新逻辑卷的硬盘大小、-s创建扩招逻辑卷、-n指定新逻辑卷的名称</font> 
                      <p></p>
                     <blockquote>创建文件系统:&emsp;&emsp;&emsp;```使用相应的命令行程序来创建所需要的文件系统（如mkfs.ext4），然后使用mount挂载文件系统，在/etc/fstab下设置成重启生效```</blockquote>
                     - <b>修改LVM</b>:&emsp;&emsp;&emsp;&emsp;```vgchange：激活或禁用居卷组、vgremove：删除卷组、vgextend：将物理卷加到卷组中、vgreduce：从卷组中删除物理卷、lvextend：增加逻辑卷的大小、lvreduce：减小逻辑卷的大小```
               </blockquote>
                     * 安装软件程序
                  <blockquote>
                        - <b>基于Debian的系统</b>:&emsp;&emsp;&emsp;&emsp;```dpkg命令是基于Debian系PMS工具的核心```
                           <blockquote>用aptitude管理软件包:&emsp;&emsp;&emsp;```dpkg -L package_name：所有根软件包相关的所有文件的列表、dpkg --search absolute_file_name:查找某个特定文件属于哪个软件包、aptitude search package_name：寻找软件包、aptitude install package_name：安装软件包、aptitude safe-upgrade：更新系统软件包、aptitude purge package_name：卸载软件包```</blockquote>
                         <p></p>
                        <font color=#D87093>aptitude仓库默认存储在文件/etc/apt/sources.list中、格式为  <font color="#90EE90">deb（deb-src） address distribution_name package_type_list</font>&emsp;&emsp;&emsp;deb或deb-src的值表明软件包的类型，deb的值说明这是一个已编译程序源、而deb-src值则说明这是一个源代码的源;distribution_name表示特定软件仓库的发行版版本的名称；package_type_list：表面仓库里面有什么类型的包</font> 
                        <p></p> 
                        - <b>基于Red Hat的系统</b>:&emsp;&emsp;&emsp;&emsp;```rpm命令是基于Red Hat系PMS工具的核心```
                           <blockquote>Yum:&emsp;&emsp;&emsp;```yum list installed：列出系统上安装的包、yum provides /etc/yum.conf：查找某个特定文件属于哪个软件包、yum localinstall package_name.rpm：本地安装rpm包、yum update package_name：更新软件包、yum remove package_name：只删除软件包而保留配置文件和数据文件、yum erase package_name：删除软件和它所有的文件、yum deplist package_name：显示了所有包的库依赖关系以及什么软件可以提供这些库依赖关系、yum repolist：显示目前在哪些仓库中获取软件```</blockquote>
                  </blockquote>