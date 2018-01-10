<center><font color=#D87093>Linux命令行和shell脚本编程大全知识点</font></center>
========================================
<center>第二部分        SHELL脚本编程基础</center>
----------------------------------------

<p align = "right" >人没有牺牲就什麽都得不到，为了得到什麽东西，就需要付出同等的代价</p>
* 构建基本脚本
<blockquote>
    - <b>使用多个命令</b>:&emsp;&emsp;&emsp;&emsp;```shell可以让你将多个命令串起来，一次执行完成。如果要两个命令一起运行，可以 把它们放在同一行中，彼此间用分号隔开```
    - <b>创建shell脚本</b>:&emsp;&emsp;&emsp;&emsp;```PATH环境变量被设置成只在一组目录中查找命令。要让shell找到test1脚本，只需采取以下两种方法之一：1.将shell脚本文件所处的目录添加到PATH环境变量中（echo $PATH查看）;2.在提示符中用绝对或相对文件路径来引用shell脚本文件（使用./，然后赋予脚本权限）```
    <p></p>
<font color=#D87093>在创建shell脚本文件时，必须在文件的第一行指定要使用的shell。其格式为: #!/bin/bash</font>
    <p></p>
    - <b>显示消息</b>:&emsp;&emsp;&emsp;&emsp;```echo命令可用单引号或双引号来划定文本字符串。如果在字符串中用到了它们，需要在文本中使用其中一种引号，而用另外一种来将字符串划定起来```
    - <b>使用变量</b>:&emsp;&emsp;&emsp;&emsp;``` ```    
        - <b>环境变量</b>:&emsp;&emsp;&emsp;&emsp;```在脚本中，可以在环境变量名称之前加上美元符($)来使用这些环境变量```
        <p></p>
<font color=#D87093>反斜线允许shell脚本将美元符解读为实际的美元符</font>
        <p></p>
        - <b>用户变量</b>:&emsp;&emsp;&emsp;&emsp;```定义变量允许临时存储数 据并在整个脚本中使用；用户变量可以是任何由字母、数字或下划线组成的文本字符串，长度不超过20个；用户变量区分大小写；在变量、等号和值之间不能出现空格；```
        - <b>命令替换</b>:&emsp;&emsp;&emsp;&emsp;```shell脚本中最有用的特性之一就是可以从命令输出中提取信息，并将其赋给变量：反引号字符(`)，如testing='date'、$()格式，如testing=$(date)```   
    - <b>输入输出重定向</b>:&emsp;&emsp;&emsp;&emsp;``` ```
        - <b>输出重定向</b>:&emsp;&emsp;&emsp;&emsp;```最基本的重定向将命令的输出发送到一个文件中。bash shell用大于号(>)来完成这项功能；用双大于号(>>)来追加数据，不覆盖文件原有内容```
        - <b>输入重定向</b>:&emsp;&emsp;&emsp;&emsp;```输入重定向将文件的内容重定向到命令:输入重定向符号是小于号(<);内联输入重定向符号是远小于号(<<):无需使用文件进行重定向，只需要在命令行中指定用于输入重定向的数据```
    - <b>管道</b>:&emsp;&emsp;&emsp;&emsp;```管道被放在命令之间，将一个命令的输出重定向 到另一个命令中:command1 | command2；如rpm -qa | sort > rpm.list```
    - <b>执行数学运算</b>:&emsp;&emsp;&emsp;&emsp;```使用expr命令来进行数学运算```
        <p></p>
<font color=#D87093>在bash中，在将一个数学运算结果赋给某个变量时，可以用美元符和 方括号($[ operation ])将数学表达式围起来，如：var4=$[$var1 * ($var2 - $var3)]</font>
        <p></p> 
        - <b>bc的基本用法</b>:&emsp;&emsp;&emsp;&emsp;```bash计算器实际上是一种编程语言，它允许在命令行中输入浮点表达式，然后解释并计算该表达式，最后返回结果，bash计算器能够识别：数字（整数和浮点数）、变量（简单变量和数组）、注释(以#或C语言中的/* */开始的行)、表达式、编程语句（如if--then语句）、函数```
            <p></p>
        <font color=#D87093>浮点运算是由内建变量scale控制的。必须将这个值设置为你希望在计算结果中保留的小数位数，否则无法得到期望的结果;scale变量的默认值是0</font> 
            <p></p>
            - <b>在脚本中使用bc</b>:&emsp;&emsp;&emsp;&emsp;```语法格式为：variable=$(echo "options; expression" | bc);第一部分options允许你设置变量。如果你需要不止一个变量，可以用分号将其分开。expression参数定义了通过bc执行的数学表达式```
                    
                    #!/bin/bash
                    var1=20
                    var2=3.14159
                    var3=$(echo "scale=4; $var1 * $var1" | bc)
                    var4=$(echo "scale=4; $var3 * $var2" | bc)
                    echo The final result is $var4
                *该方法适合适用于较短的运算*
            <p></p>
                <font color=#D87093>最好的办法是使用内联输入重定向，它允许你直接在命令行中重定向数据。在shell脚本中， 你可以将输出赋给一个变量，语法格式为：variable=$(bc << EOF  options  statements  expressions  EOF )<b>(此处空格为回车);EOF文本字符串标识了内联重定向数据的起止。记住，仍然需要命令替换符号将bc命令的输出赋给变量</b></font> 
                    
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
            
            <p>以下是混合用法：</p>


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

    - <b>退出码</b>:&emsp;&emsp;&emsp;&emsp;```shell中运行的每个命令都使用退出状态码(exit status)告诉shell它已经运行完毕。退出状态码是一个0~255的整数值，在命令结束运行时由命令传给shell；Linux提供了一个专门的变量$?来保存上个已执行命令的退出状态码```

        状态码 |           描述    
        -------------- | ------------
        0       |   命令成功结束
        1       |   一般性未知错误
        2       |   不适合的shell命令
        126     |   命令不可执行
        127     |   没找到命令
        128     |   无效的退出参数
        128+x   |   与Linux信号x相关的严重错误
        130     |   通过Ctrl+C终止的命令
        255     |   正常范围之外的退出状态码 

    - <b>exit命令</b>:&emsp;&emsp;&emsp;&emsp;```exit命令允许你在脚本结束时指定一个退出状态码；当查看脚本的退出码时，会得到作为参数传给exit命令的值；也可以在exit命令的参数中使用变量```
            <p></p>
        <font color=#D87093>退出状态码最大只能是255；如果大于这个值，指定的数值除以256后得到的余数则为返回值，退出状态码被缩减到了0~255的区间</font> 
            <p></p>
</blockquote>


    * 使用结构化命令
    <blockquote>
        - <b>使用多个命令</b>:&emsp;&emsp;&emsp;&emsp;```shell可以让你将多个命令串起来，一次执行完成。如果要两个命令一起运行，可以 把它们放在同一行中，彼此间用分号隔开```
    </blockquote>
