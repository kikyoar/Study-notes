<center><font color=#D87093>Linux命令行和shell脚本编程大全知识点</font></center>
========================================
<center>第二部分        SHELL脚本编程基础</center>
----------------------------------------

<p align = "right" >人没有牺牲就什麽都得不到，为了得到什麽东西，就需要付出同等的代价</p>
## 构建基本脚本

> **使用多个命令**：&emsp;&emsp;&emsp;&emsp;shell可以让你将多个命令串起来，一次执行完成。如果要两个命令一起运行，可以 把它们放在同一行中，彼此间用分号隔开  
> **创建shell脚本**：&emsp;&emsp;&emsp;&emsp;PATH环境变量被设置成只在一组目录中查找命令。要让shell找到test1脚本，只需采取以下两种方法之一：
>> * 将shell脚本文件所处的目录添加到PATH环境变量中（echo $PATH查看)
>> * 在提示符中用绝对或相对文件路径来引用shell脚本文件（使用./，然后赋予脚本权限)  
>> <font color=#D87093>在创建shell脚本文件时，必须在文件的第一行指定要使用的shell。其格式为: #!/bin/bash</font>  

> **显示消息**:&emsp;&emsp;&emsp;&emsp;echo命令可用单引号或双引号来划定文本字符串。如果在字符串中用到了它们，需要在文本中使用其中一种引号，而用另外一种来将字符串划定起来  
> **使用变量**:  
>> * **环境变量**:&emsp;&emsp;&emsp;&emsp;在脚本中，可以在环境变量名称之前加上美元符($)来使用这些环境变量  
>> <font color=#D87093>反斜线允许shell脚本将美元符解读为实际的美元符</font>  
>> * **用户变量**：&emsp;&emsp;&emsp;&emsp;定义变量允许临时存储数 据并在整个脚本中使用；用户变量可以是任何由字母、数字或下划线组成的文本字符串，长度不超过20个；用户变量区分大小写；在变量、等号和值之间不能出现空格  
>> * **命令替换**：&emsp;&emsp;&emsp;&emsp;shell脚本中最有用的特性之一就是可以从命令输出中提取信息，并将其赋给变量：反引号字符(`)，如testing='date'、$()格式，如testing=$(date)  

> **输入输出重定向**:  
>> * **输出重定向**:&emsp;&emsp;&emsp;&emsp;最基本的重定向将命令的输出发送到一个文件中。bash shell用大于号(>)来完成这项功能；用双大于号(>>)来追加数据，不覆盖文件原有内容  
>> * **输入重定向**:&emsp;&emsp;&emsp;&emsp;输入重定向将文件的内容重定向到命令:输入重定向符号是小于号(<);内联输入重定向符号是远小于号(<<):无需使用文件进行重定向，只需要在命令行中指定用于输入重定向的数据  

> **管道**:&emsp;&emsp;&emsp;&emsp;管道被放在命令之间，将一个命令的输出重定向 到另一个命令中:command1 | command2；如rpm -qa | sort > rpm.list    
> **执行数学运算**:&emsp;&emsp;&emsp;&emsp;使用expr命令来进行数学运算  
> ```在bash中，在将一个数学运算结果赋给某个变量时，可以用美元符和方括号($[ operation ])将数学表达式围起来，如：var4=$[$var1 * ($var2 - $var3)]```  
>> * **bc的基本用法**：&emsp;&emsp;&emsp;&emsp;bash计算器实际上是一种编程语言，它允许在命令行中输入浮点表达式，然后解释并计算该表达式，最后返回结果，bash计算器能够识别：数字（整数和浮点数）、变量（简单变量和数组）、注释(以#或C语言中的/* */开始的行)、表达式、编程语句（如if--then语句）、函数  
>> <font color=#D87093>浮点运算是由内建变量scale控制的。必须将这个值设置为你希望在计算结果中保留的小数位数，否则无法得到期望的结果;scale变量的默认值是0</font>  
>> * **在脚本中使用bc**:&emsp;&emsp;&emsp;&emsp;语法格式为：variable=$(echo "options; expression" | bc);第一部分options允许你设置变量。如果你需要不止一个变量，可以用分号将其分开。expression参数定义了通过bc执行的数学表达式  

>>
                    #!/bin/bash
                    var1=20
                    var2=3.14159
                    var3=$(echo "scale=4; $var1 * $var1" | bc)
                    var4=$(echo "scale=4; $var3 * $var2" | bc)
                    echo The final result is $var4

>> <font color=#D87093>最好的办法是使用内联输入重定向，它允许你直接在命令行中重定向数据。在shell脚本中， 你可以将输出赋给一个变量，语法格式为：variable=$(bc << EOF  options  statements  expressions  EOF )<b>(此处空格为回车);EOF文本字符串标识了内联重定向数据的起止。记住，仍然需要命令替换符号将bc命令的输出赋给变量</b></font>  
>> 
                    #!/bin/bash
                    var1=10.46
                    var2=43.67
                    var3=33.2
                    var4=71
                    var5=$(bc << EOF
                    scale = 4
                    a1 = ( $var1 * $var2)
                    b1 = ($var3 * $var4)
                    a1 + b1
                    EOF
                    )  
>> **以下是混合用法**   
>>                 
			 	#!/bin/bash
                var1=20
                var2=3.14159
                var3=$(echo "scale=5; $var1 * $var2" | bc)
                var4=$(echo "scale=5; $var3 / $var2" |bc)                 
                var5=$(bc << EOF
                scale=5
                a1=($var1 * $var2)
                a2=($var3 * $var4)
                a1+b1
                EOF
                )               
                echo The final answer for this mess is $var3
                echo The final answer for this mess is $var4
                echo The final answer for this mess is $var5  

> **退出码**:&emsp;&emsp;&emsp;&emsp;shell中运行的每个命令都使用退出状态码(exit status)告诉shell它已经运行完毕。退出状态码是一个0~255的整数值，在命令结束运行时由命令传给shell；Linux提供了一个专门的变量$?来保存上个已执行命令的退出状态码  
>
			        状态码 |           描述    
			        -------------- | ------------
			        0       |   	命令成功结束
			        1       |   	一般性未知错误
			        2       |   	不适合的shell命令
			        126     |   	命令不可执行
			        127     |   	没找到命令
			        128     |   	无效的退出参数
			        128+x   |   	与Linux信号x相关的严重错误
			        130     |   	通过Ctrl+C终止的命令
			        255     |  	 	正常范围之外的退出状态码 
> **exit命令**:&emsp;&emsp;&emsp;&emsp; exit命令允许你在脚本结束时指定一个退出状态码；当查看脚本的退出码时，会得到作为参数传给exit命令的值；也可以在exit命令的参数中使用变量  
> <font color=#D87093>退出状态码最大只能是255；如果大于这个值，指定的数值除以256后得到的余数则为返回值，退出状态码被缩减到了0~255的区间</font> 


## 使用结构化命令
> **使用if-then语句**：&emsp;&emsp;&emsp;&emsp;bash shell的if语句会运行if后面的那个命令。如果该命令的退出状态码是0 (该命令成功运行)，位于then部分的命令就会被执行。如果该命令的退出状态码是其他值，then部分的命令就不会被执行，bash shell会继续执行脚本中的下一个命令。fi语句用来表示if-then 语句到此结束
> **使用if-then-else语句**：&emsp;&emsp;&emsp;&emsp;当if语句中的命令返回退出状态码0时，then部分中的命令会被执行，这跟普通的if-then语句一样。当if语句中的命令返回非零退出状态码时，bash shell会执行else部分中的命令  
>>
	$ cat test4.sh
	#!/bin/bash
	# testing the else section
	#
	testuser=NoSuchUser
	#
	if grep $testuser /etc/passwd then
   		echo "The bash files for user $testuser are:"
	   	ls -a /home/$testuser/.b*
   		echo
	else
   		echo "The user $testuser does not exist on this system."
   		echo
	fi  

>>$ ./test4.sh

>>The user NoSuchUser does not exist on this system.

> **嵌套if**：&emsp;&emsp;&emsp;&emsp;有时需要检查脚本代码中的多种条件，可以使用嵌套的if-then语句  
> <font color=#D87093>可以使用else部分的另一种形式:elif。这样就不用再书写多个if-then语句了。elif使用另一个if-then语句延续else部分;如果elif后命令的退出状态码是0，则bash会执行第二个then语句部分的命令</font>
>>  
	if command1 
	then
		command set 1 
	elif command2
	then
		command set 2 
	elif command3 
	then
		command set 3 
	elif command4 
	then
		command set 4
	fi  
>> *每块命令都会根据命令是否会返回退出状态码0来执行。记住，bash shell会依次执行if语句，
只有第一个返回退出状态码0的语句中的then部分会被执行*  

> **test命令**：&emsp;&emsp;&emsp;&emsp;test命令提供了在if-then语句中测试不同条件的途径。如果test命令中列出的条件成立，test命令就会退出并返回退出状态码0  
> *bash shell提供了另一种条件测试方法，无需在if-then语句中声明test命令*  
> 
	if [ condition ] 
	then
		commands
	fi  
> <font color=#D87093>方括号定义了测试条件。注意，第一个方括号之后和第二个方括号之前必须加上一个空格，否则就会报错</font>  
> **test命令可以判断三类条件**:数值比较、字符串比较、文件比较  
>> **数值比较**  
>>
							  比较   |           描述    
			     	-------------- | ------------
			     n1 -eq n2		|    检查n1是否与n2相等
			     n1 -ge n2		|	检查n1是否大于或等于n2
			     n1 -gt n2 		|	检查n1是否大于n2
			     n1 -le n2		|	检查n1是否小于等于n2 
			     n1 -lt n2 		|	检查n1是否小于n2
			     n1 -ne n2		| 	检查n1是否不等于n2  
>> <font color=#D87093>bash shell只能处理整数</font>  

>> **字符串比较**  
>> 
							  比较   |           描述    
			     	-------------- | ------------
			      str1 = str2		|    检查str1是否和str2相同
			      str1 != str2		|	检查str1是否和str2不同
			      str1 < str2 		|	检查str1是否和str2小
			      str1 > str2		|	检查str1是否和str2大 
			      -n str1 			|	检查str1的长度是否非0
			      -z str1				| 	检查str1的长度是否是0  
>> *1.字符串相等性*
>>
		#!/bin/bash
		# testing string equality testuser=baduser
		#
		if [ $USER != $testuser ] then
		   echo "This is not $testuser"
		else
		   echo "Welcome $testuser"
		fi  
>> *2.字符串顺序*  
>> <font color=#D87093>要测试一个字符串是否比另一个字符串大就是麻烦的开始：</font>  
>> <font color=#D87093>1.大于号和小于号必须转义，否则shell会把它们当作重定向符号，把字符串值当作文件名</font>  
>> <font color=#D87093>2.大于和小于顺序和sort命令所采用的不同</font>  
>>  
		$ cat test9b.sh
		#!/bin/bash
		# testing string sort order val1=Testing
		val2=testing
		#
		if [ $val1 \> $val2 ]
		then
		       echo "$val1 is greater than $val2"
		    else
		       echo "$val1 is less than $val2"
		    fi  

>>  	
		$ ./test9b.sh
		Testing is less than testing
		$ sort testfile
		testing
		Testing
		$  
>> <font color=#D87093>在比较测试中，大写字母被认为是小于小写字母的。但sort命令恰好相反;比较测试中使用的是标准的ASCII顺序，根据每个字符的ASCII数值来决定排序结果。sort命令使用的是系统的本地化语言设置中定义的排序顺序</font>  
>> *3.字符串比较*   
>> <font color=#D87093>-n和-z可以检查一个变量是否含有数据</font>
>>     	
		$ cat test10.sh #!/bin/bash
		# testing string length val1=testing
		val2=''
		#
		if [ -n $val1 ]
		then
		       echo "The string '$val1' is not empty"
		    else
		       echo "The string '$val1' is empty"
		    fi
		    #
		    if [ -z $val2 ]
		    then
		       echo "The string '$val2' is empty"
		    else
		       echo "The string '$val2' is not empty"
		    fi
		    #
		    if [ -z $val3 ]
		    then
		       echo "The string '$val3' is empty"
		    else
		       echo "The string '$val3' is not empty"
		fi
>>  		
		$
		$ ./test10.sh
		The string 'testing' is not empty 
		The string '$val2' is empty
		The string '$val3' is empty  
>> <font color=#D87093>空的和未初始化的变量会对shell脚本测试造成灾难性的影响。如果不是很确定一个变量的内容，最好在将其用于数值或字符串比较之前先通过-n或-z来测试一下变量是否含有值</font>  

>> **文件比较**
>>  
							  比较   |           描述    
			     	-------------- | ------------
			      -d file		|    检查file是否存在并是一个目录
			      -e file		|	检查file是否存在
			      -f file 		|	检查file是否存在并是一个文件			      
			      -r file		|	检查file是否存在并可读
			      -s file 			|	检查file是否存在并非空			      
			      -w file			| 	检查file是否存在并可写
			      -x file			|	检查file是否存在并可执行
			      -O file			|	检查file是否存在并属当前用户所有
			      -G file			|	检查file是否存在并且默认组与当前用户相同
			      file1 -nt file2		| 	检查file1是否比file2新
			      file1 -ot file2 		|	检查file1是否比file2旧  

>> *1.检查目录*  
>> <font color=#D87093>-d测试会检查指定的目录是否存在于系统中。如果你打算将文件写入目录或是准备切换到某个目录中，先进行测试总是件好事情</font>  
>>   
	$ cat test11.sh
	#!/bin/bash
	# Look before you leap
	# jump_directory=/home/arthur #
	if [ -d $jump_directory ] then
	       echo "The $jump_directory directory exists"
	       cd $jump_directory
	       ls
	    else
	       echo "The $jump_directory directory does not exist"
	fi  
>> *2.检查对象是否存在*  
>> <font color=#D87093>-e比较允许你的脚本代码在使用文件或目录前先检查它们是否存在</font>  
>> 
	$ cat test12.sh
	#!/bin/bash
	# Check if either a directory or file exists #
	location=$HOME
	file_name="sentinel"
	#
	if [ -e $location ]
	then #Directory does exist
	   echo "OK on the $location directory."
	   echo "Now checking on the file, $file_name."
	   #
	   if [ -e $location/$file_name ]
	   then #File does exist
	       echo "OK on the filename"
	       echo "Updating Current Date..."
	       date >> $location/$file_name
	   #
	   else #File does not exist
	       echo "File does not exist"
	       echo "Nothing to update"
	   fi
	#
	else   #Directory does not exist
	   echo "The $location directory does not exist."
	   echo "Nothing to update"
	fi  
>> *3.检查文件*
>> <font color=#D87093>-e比较可用于文件和目录。要确定指定对象为文件，必须用-f比较</font>
>>   
	$ cat test13.sh
	#!/bin/bash
	# Check if either a directory or file exists #
	item_name=$HOME
	echo
	echo "The item being checked: $item_name" echo
	#
	if [ -e $item_name ]
	then #Item does exist
	       echo "The item, $item_name, does exist."
	       echo "But is it a file?"
	       echo
	       #
	       if [ -f $item_name ]
	       then #Item is a file
	           echo "Yes, $item_name is a file."
	       #
	       else #Item is not a file
	           echo "No, $item_name is not a file."
	fi #
	    else   #Item does not exist
	       echo "The item, $item_name, does not exist."
	       echo "Nothing to update"
	fi
	#
	$ ./test13.sh
	    The item being checked: /home/Christine
	    The item, /home/Christine, does exist.
	    But is it a file?
	    No, /home/Christine is not a file.  
>> *4. 检查是否可读*  
>> <font color=#D87093>在尝试从文件中读取数据之前，最好先测试一下文件是否可读。可以使用-r比较测试</font>  
>>   
	$ cat test14.sh
	#!/bin/bash
	# testing if you can read a file pwfile=/etc/shadow
	#
	# first, test if the file exists, and is a file 
	if [ -f $pwfile ]
	then
	       # now test if you can read it
	       if [ -r $pwfile ]
	       then
	          tail $pwfile
	       else
	          echo "Sorry, I am unable to read the $pwfile file"
	       fi
	    else
	       echo "Sorry, the file $file does not exist"
	fi
	$
	$ ./test14.sh
	Sorry, I am unable to read the /etc/shadow file  
>> *5. 检查空文件*  
>> <font color=#D87093>应该用-s比较来检查文件是否为空，尤其是在不想删除非空文件的时候。要留心的是，当-s比较成功时，说明文件中有数据</font>  
>>   
	$ cat test15.sh
	#!/bin/bash
	# Testing if a file is empty #
	file_name=$HOME/sentinel
	#
	if [ -f $file_name ]
	then
	       if [ -s $file_name ]
	       then
	          echo "The $file_name file exists and has data in it."
	          echo "Will not remove this file."
	#
	else
	          echo "The $file_name file exists, but is empty."
	          echo "Deleting empty file..."
	          rm $file_name
	fi else
	       echo "File, $file_name, does not exist."
	    fi
	#
	$ ls -l $HOME/sentinel
	-rw-rw-r--. 1 Christine Christine 29 Jun 25 05:32 /home/Christine/sentinel $
	$ ./test15.sh
	The /home/Christine/sentinel file exists and has data in it.
	Will not remove this file.  
>> *6. 检查是否可写*  
>>  <font color=#D87093>-w比较会判断你对文件是否有可写权限</font>   
>>   
	#!/bin/bash
	var1=/Users/jumporange/Downloads/test.sh
	echo
	echo "The item being checked: $var1"
	echo
	if [ -f $var1 ]
	then
	    echo "YES,This is a file"
	    echo "let's check it write"
	    echo
	    if [ -e $var1 ]
	    then
	        echo "Writing current time to $var1"
	        date +%H%M >> $var1
	    else
	        echo "this file is not write"
	    fi
	else
	    echo "No, $item_name is not a file."
	fi  
>> *7. 检查文件是否可以执行*  
>> <font color=#D87093>-x比较是判断特定文件是否有执行权限的一个简单方法</font>   
>>   
	$ cat test17.sh #!/bin/bash
	# testing file execution #
	if [ -x test16.sh ]
	then
	       echo "You can run the script: "
	       ./test16.sh
	    else
	       echo "Sorry, you are unable to execute the script"
	    fi
	$
	$ ./test17.sh
	You can run the script: [...]
	$
	$ chmod u-x test16.sh $
	$ ./test17.sh
	Sorry, you are unable to execute the script  
>> *8. 检查所属关系*  
>> <font color=#D87093>-O比较可以测试出你是否是文件的属主</font>  
>>   
	$ cat test18.sh 
	#!/bin/bash
	# check file ownership #
	if [ -O /etc/passwd ] 
	then
	 	echo "You are the owner of the /etc/passwd file"
	else
		echo "Sorry, you are not the owner of the /etc/passwd file"
	fi
	$
	$ ./test18.sh
	Sorry, you are not the owner of the /etc/passwd file 
	$   
>> *9. 检查默认属组关系*  
>> <font color=#D87093>-G比较会检查文件的默认组，如果它匹配了用户的默认组，则测试成功。-G比较只会检查默认组而非用户所属的所有组</font>  
>> *10. 检查文件日期*  
>> <font color=#D87093>-nt比较会判定一个文件是否比另一个文件新。如果文件较新，那意味着它的文件创建日期更近。-ot比较会判定一个文件是否比另一个文件旧。如果文件较旧，意味着它的创建日期更早</font>  
>>   
	$ cat test20.sh 
	#!/bin/bash
	# testing file dates
    #
    if [ test19.sh -nt test18.sh ]
    then
       echo "The test19 file is newer than test18"
    else
       echo "The test18 file is newer than test19"
    fi
    if [ test17.sh -ot test19.sh ]
    then
      echo "The test17 file is older than the test19 file"
    fi  

> **复合条件测试**  
> if-then语句允许你使用布尔逻辑来组合测试。有两种布尔运算符可用:  
> <font color=#D87093>[ condition1 ] && [ condition2 ]</font>    
> <font color=#D87093>[ condition1 ] || [ condition2 ]</font>  
> 第一种布尔运算使用AND布尔运算符来组合两个条件。要让then部分的命令执行，两个条件都必须满足    
> 第二种布尔运算使用OR布尔运算符来组合两个条件。如果任意条件为TRUE，then部分的命令就会执行     
>  
	$ cat test22.sh
	#!/bin/bash
	# testing compound comparisons
	#
	if [ -d $HOME ] && [ -w $HOME/testing ] 
	then
	   echo "The file exists and you can write to it"
	else
	   echo "I cannot write to the file"
	fi
	$
	$ ./test22.sh
	I cannot write to the file $
	$ touch $HOME/testing $
	$ ./test22.sh
	The file exists and you can write to it  
> **if-then的高级特性**  
> <font color=#D87093>1.用于数学表达式的双括号</font>  
> <font color=#D87093>2.用于高级字符串处理功能的双方括号</font>  
>> *1.使用双括号*:&emsp;&emsp;&emsp;&emsp;双括号命令允许你在比较过程中使用高级数学表达式  
>> 双括号命令的格式:(( expression ))  
>> 
							  符号   |           描述    
			     	-------------- | ------------
			      val++	|    后增
			      val--		|	后减
			      ++val 		|	先增			      
			      --val		|	先减
			      ! 			|	逻辑求反			      
			      ~			| 	位求反
			      **			|	幂运算	
			      >>			|	右位移
			      <<		|	左位移
			      &		| 	位布尔和
			      \| 		|	位布尔或  
			      && 		|	逻辑和
			      \|\| 		|	逻辑或  
>> 
	$ cat test23.sh
	#!/bin/bash
	# using double parenthesis #
	val1=10
	#
	if (( $val1 ** 2 > 90 )) then
	       (( val2 = $val1 ** 2 ))
	       echo "The square of $val1 is $val2"
	    fi
	$
	$ ./test23.sh
	The square of 10 is 100  
>> *1.使用双方括号*:&emsp;&emsp;&emsp;&emsp;双方括号命令提供了针对字符串比较的高级特性  
>> 双方括号命令的格式: [[ expression ]]   
>> <font color=#D87093>双方括号里的expression使用了test命令中采用的标准字符串比较。但它提供了test命令未提供的另一个特性——模式匹配(pattern matching)</font>  
>>   
	$ cat test24.sh
	#!/bin/bash
	# using pattern matching
	if [[ $USER == r* ]]
	then
		echo "Hello $USER"
	else
	    echo "Sorry, I do not know you"
	fi
	$ ./test24.sh
	Hello rich  

> **case命令**:&emsp;&emsp;&emsp;&emsp;case命令会采用列表格式来检查单个变量的多个值      
> <font color=#D87093>case variable in</font>  
> <font color=#D87093>pattern1 | pattern2) commands1;;</font>  
> <font color=#D87093>pattern3) commands2;;</font>  
> <font color=#D87093>*) default commands;;</font>  
> <font color=#D87093>esac</font>  
> *case命令会将指定的变量与不同模式进行比较。如果变量和模式是匹配的，那么shell会执行为该模式指定的命令。可以通过竖线操作符在一行中分隔出多个模式模式。星号会捕获所有与已知模式不匹配的值*  
>  
	$ cat test26.sh #!/bin/bash
	# using the case command #
	case $USER in
	rich | barbara)
	       echo "Welcome, $USER"
	       echo "Please enjoy your visit";;
	    testing)
	      echo "Special testing account";;
	    jessica)
	       echo "Do not forget to log off when you're done";;
	    *)
	       echo "Sorry, you are not allowed here";;
	    esac
	$
	$ ./test26.sh
	Welcome, rich
	Please enjoy your visit