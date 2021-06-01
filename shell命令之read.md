> ***\*链接：https://www.cnblogs.com/wangtao1993/p/6136169.html\****

**1、read基本读取**

```javascript
  1 #!/bin/bash  2 #testing the read command  3   4 echo -n "Enter you name:"   #echo -n 让用户直接在后面输入   5 read name  #输入的多个文本将保存在一个变量中  6 echo "Hello $name, welcome to my program."                                      
```

执行：

```javascript
# ./read.shEnter you name: wangtaoHello wangtao, welcome to my program.
```

**2、read -p （\**直接在read命令行指定提示符\**）**

```javascript
  1 #!/bin/bash  2 #testing the read -p option  3 read -p "Please enter your age: " age  4 days=$[ $age * 365 ]  5 echo "That makes you over $days days old!"
```

执行：

```javascript
# ./age.shPlease enter your age: 23That makes you over 8395 days old!
```

**3、read -p （指定多个变量）**

```javascript
  1 #!/bin/bash  2 # entering multiple variables  3   4 read -p "Enter your name:" first last  5 echo "Checking data for $last, $first"
```

执行：

```javascript
# ./read1.shEnter your name: a bChecking data for b, a
```

**4、read 命令中不指定变量**，那么read命名将它收到的任何数据都放在特殊环境变量REPLY中

```javascript
 1 #!/bin/bash  2 # testing the REPLY environment variable  3   4 read -p "Enter a number: "  5 factorial=1                           6 for (( count=1; count<= $REPLY; count++ ))  7 do  8    factorial=$[ $factorial * $count ]   #等号两端不要有空格  9 done 10 echo "The factorial of $REPLY is $factorial"
```

执行：

```javascript
./read2.shEnter a number: 6The factorial of 6 is 720
```

**5、超时, 等待输入的秒数（read -t）**

```javascript
  1 #!/bin/bash  2 # timing the data entry  3   4 if read -t 5 -p "Please enter your name: " name     #记得加-p参数， 直接在read命令行指定提示符  5 then  6     echo "Hello $name, welcome to my script"  7 else  8     echo   9     echo "Sorry, too slow!" 10 fi
```

执行：

```javascript
# ./read3.shPlease enter your name: Sorry, too slow!
# ./read3.sh Please enter your name: wangHello wang, welcome to my script
```

5、read命令对输入的字符判断

```javascript
  1 #!/bin/bash  2 # getting just one character of input  3   4 read -n1 -p "Do you want to continue [Y/N]? " answer  5 case $answer in  6 Y | y) echo  7        echo "fine, continue on...";;  8 N | n) echo   9        echo "OK, goodbye" 10        exit;; 11 esac   
```

执行：

```javascript
# ./read4.shDo you want to continue [Y/N]? yfine, continue on..../read4.shDo you want to continue [Y/N]? nOK, goodbye
```

**6、隐藏方式读取（\**read -s\**）**

```javascript
  1 #!/bin/bash  2 # hiding input data from the monitor  3   4 read -s -p "Enter your passwd: " pass   #-s 参数使得read读入的字符隐藏  5 echo   6 echo "Is your passwd readlly $pass?"~                                          
```

执行：

```javascript
# ./read5.shEnter your passwd: Is your passwd readlly osfile@206?
```

**7、从文本中读取**

```javascript
  1 #!/bin/bash  2 # reading data from a file  3   4 count=1  5 cat test | while read line  6 do  7    echo "Line $count: $line"  8    count=$[ $count + 1 ]  9 done 10 echo "Finished processing the file"
```

执行：

```javascript
 ./read6.shLine 1: The quick brown dog jumps over the lazy fox.Line 2: This is a test, this is only a test.Line 3: O Romeo, Romeo! Wherefore art thou Romeo?Finished processing the file
```