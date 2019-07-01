# Shell
## Shell基础知识
 - `history`为输入命令历史
 - ``!!``执行上一条执行的指令
 - `!n`执行命令历史中的第n条指令
 - `!字符串`可以执行以改字符串为开头的最近的一条指令
 - **Tab**补全一个指令/路径/文件名，连按两次会列出所有符合的指令和文件名
 - Shell文件开头必须添加：`#!/bin/bash`
 - 编写Shell脚本后，需要将脚本设置为可执行权限：`chmod +x 114.sh`
 - 反引号　\`　中的内容会被**优先执行**，同`$()`
 - `let` 命令是 BASH 中用于计算的工具，用于执行一个或多个表达式，变量计算中**不需要**加上 `$` 来表示变量。如果表达式中包含了空格或其他特殊字符，则必须引起来。语法格式：`let arg [arg ...]`

## Shell变量
### 定义变量
 ```
 your_name="yjspn.810"
 ```
 - 变量名和等号之间**不能有空格**
 - 只能使用英文字母，数字和下划线,**开头**不能为**数字**
 - 符号只能用**下划线**
 - 不能使用bash里的关键字

### 使用变量
```
your_name="yjspn"
echo $your_name
echo ${your_name}
```
 - 建议给变量加花括号
 - 使用变量时才使用`$`

### 变量操作
 - `readonly` 将变量变为只读
 - `unset` 删除变量，**只读的不能删除**

## Shell字符串

> 类似PHP

### 单引号
 - 所有字符均**原样输出**，变量无效
 - 串内不能出现**单独**的单引号，*转义了也不行*，但是**能成对**出现

### 双引号
 - 可以有变量
 - 可以有转义字符

### 获取字符串长度方法之一
```
echo ${#str}
```

## Shell数组

### 定义数组

```
array_name=(value0 value1 value2 value3)
```
 - 用空格分开，批量定义
 - 竖过来也行，还是要加空格
 - 单独定义：`array_name[0]=value0`

### 读取数组
 ```
 echo ${array_name[@]}
 ```

### 获取数组长度方法之一
 ```
 # 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
 ```

## Shell注释

### 通用
行首加`#`

### 多行注释
```
<<'EOF'
注释内容...
注释内容...
注释内容...
EOF
```
 - EOF可以替换为其他字符串或者符号
 - 仅推荐这种注释方法

## Shell传递参数
 - 脚本内获取参数的格式为：`$n`
 - `$0`为**文件名**
 - n 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推
 - `$10` 不能获取第十个参数，获取第十个参数需要`${10}`。当n>=10时，需要使用`${n}`来获取参数

| 参数处理 | 说明 |
| ---- | ---- |
|$# | 传递到脚本的参数**个数**|
$* | 以一个单字符串显示所有向脚本传递的参数。如"$*"用「"」括起来的情况、**以"$1 $2 … $n"的形式**输出所有参数。|
$$ | 脚本运行的当前进程ID号|
$! | 后台运行的最后一个进程的ID号|
$@ | 与$\*相同，但是使用时加引号，并在引号中返回每个参数。如"$@"用「"」括起来的情况、**以"$1" "$2" … "$n" 的形式**输出所有参数。|
$- | 显示Shell使用的当前选项，与set命令功能相同。
$? | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。|

#### $* 与 $@ 区别
 - 相同点：都是引用所有参数。
  - 不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了**一个**参数），而 "@" 等价于 "1" "2" "3"（传递了**三个**参数）。

## Shell基本运算符

### 算数运算符

 - 乘号`*`前必须加反斜杠`\`才能实现乘法运算.

 - 条件表达式要放在**方括号之间**，并且要有**空格**，例如: [$a==$b] 是错误的，必须写成 **[ $a == $b ]**。

### 关系运算符

 - 只支持数字，不支持字符串，除非字符串的值是数字

 | 运算符 | 说明 | 举例 |
 | ---- | ---- | ---- |
 |-eq | 检测两个数是否相等，相等返回 true。| `[ $a -eq $b ]` 返回 `false`。 |
 |-ne | 检测两个数是否不相等，不相等返回 true。| `[ $a -ne $b ]` 返回 `true`。 |
 |-gt | 检测左边的数是否大于右边的，如果是，则返回 true。| `[ $a -gt $b ]` 返回 `false`。 |
 |-lt | 检测左边的数是否小于右边的，如果是，则返回 true。| `[ $a -lt $b ]` 返回 `true`。 |
 |-ge | 检测左边的数是否大于等于右边的，如果是，则返回 true。| `[ $a -ge $b ]` 返回 `false`。 |
 |-le | 检测左边的数是否小于等于右边的，如果是，则返回 true。| `[ $a -le $b ]` 返回 `true`。 |

### 布尔运算符

|运算符|说明|举例|
|----|----|----|
|!|非运算，表达式为 true 则返回 false，否则返回 true。|`[ ! false ]` 返回 `true`。|
-o|或运算，有一个表达式为 true 则返回 true。|`[ $a -lt 20 -o $b -gt 100 ]` 返回 `true`。|
-a|与运算，两个表达式都为 true 才返回 true。|`[ $a -lt 20 -a $b -gt 100 ]` 返回 `false`。|

### 逻辑运算符

 - 与：`&&`
 - 或：`||`

 > *似乎和`-a` `-o`没有太大区别？*

### 字符串运算符

用于检测 Unix 文件的各种属性

 > 详细内容请自行百度（

## 输出命令

### echo

 > 类似PHP

 - 普通情况下双引号可以省略`echo It is a test`
 - 显示转义字符`echo "\"It is a test\""` *最外围双引号可以去掉*
 - 输出变量`echo $name It is a test`
 - `echo -e`转义，可以插入`\n`，`\t`，`\c`等
 - 原样输出使用单引号`'`：`echo '$name\'`
 - 反引号``　`　``输出命令执行结果``　echo `date`　``

### printf

 > 类似C

 ```
 printf  format-string  [arguments...]
 ```

 - format-string: 格式控制字符串
 - arguments: 参数列表。


## Shell测试命令

 - `test` 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试

 - `test` 和 `[]` 是等价的

### 数值测试

 > 同“关系运算符”

### 字符串测试

 - `-z` 字符串：字符串长度为0为真
 - `-n` 字符串：字符串长度不为0为真

### 文件测试

| 参数 | 说明|
| ---- | ----|
| -e 文件名 | 如果文件存在则为真 |
| -r 文件名 | 如果文件存在且可读则为真 |
| -w 文件名 | 如果文件存在且可写则为真 |
| -x 文件名 | 如果文件存在且可执行则为真 |
| -s 文件名 | 如果文件存在且至少有一个字符则为真 |
| -d 文件名 | 如果文件存在且为目录则为真 |
| -f 文件名 | 如果文件存在且为普通文件则为真 |
| -c 文件名 | 如果文件存在且为字符型特殊文件则为真 |
| -b 文件名 | 如果文件存在且为块特殊文件则为真 |

 - 另外，Shell还提供了与( -a )、或( -o )、非( ! )三个逻辑操作符用于将测试条件连接起来，其优先级为："!"最高，"-a"次之，"-o"最低。

 ## Shell流程控制
 - 和Java、PHP等语言不一样，sh的流程控制**不可为空**。如果else分支没有语句执行，就不要写这个else。

 ### if else-if else
 
 ```
 if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

 - 结尾有fi
 - 与一些编程语言不同，else if写为elif
 - expression和方括号之间必须有空格

```
#判断两个变量是否相等：
a=10
b=20
if [ $a == $b ]
then
   echo "a 等于 b"
elif [ $a -gt $b ]
then
   echo "a 大于 b"
elif [ $a -lt $b ]
then
   echo "a 小于 b"
else
   echo "没有符合的条件"
fi
```

### for 
```
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

写成单行的格式
```
for var in item1 item2 ... itemN; do command1; command2… done;
```

```
#顺序输出当前列表中的数字
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done
```

### while
用于不断执行一系列命令

```
while condition
do
    command
done
```

例：
```
#!/bin/bash
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done
```

- 使用中使用了 Bash let 命令，它用于执行一个或多个表达式，变量计算中不需要加上 $ 来表示变量
- while循环可用于读取键盘信息。下面的例子中，输入信息被设置为变量FILM，按<Ctrl-D>结束循环。

```
echo '按下 <CTRL-D> 退出'
echo -n '输入你最喜欢的网站名: '
while read FILM
do
    echo "是的！$FILM 是一个好网站"
done
```

#### 无限循环
```
while :
do
    command
done
```

或者

```
while true
do
    command
done
```

或者

```
for (( ; ; ))
```

### until

 - 循环执行一系列命令直至条件为 true 时停止。
 - until 循环与 while 循环在处理方式上刚好相反。
 - 一般 while 循环优于 until 循环，但在某些时候—也只是极少数情况下，until 循环更加有用。

语法格式:
```
until condition
do
    command
done
```

使用 until 命令来输出 0 ~ 9 的数字
```
#!/bin/bash

a=0

until [ ! $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
```

### case
```
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2）
    command1
    command2
    ...
    commandN
    ;;
esac
```

- 结尾有`esac`
- 取值后面必须为`in`，每一模式必须以右括号结束。取值可以为变量或常数。匹配发现取值符合某一模式后，其间所有命令开始执行直至 `;;`
- 取值将检测匹配的每一个模式。一旦模式匹配，则执行完匹配模式相应命令后不再继续其他模式。如果无一匹配模式，使用星号 * 捕获该值，再执行后面的命令。

提示输入1到4，与每一种模式进行匹配：
```
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```

### 跳出循环

#### break
跳出所有循环（终止执行后面的所有循环）

```
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```

#### continue
不会跳出所有循环，仅仅跳出当前循环

```
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字: "
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的!"
            continue
            echo "游戏结束"
        ;;
    esac
done
```

### esac

 - `case`的结束标记
 - 每个`case`分支用右圆括号，用两个分号表示break

 
## Shell函数

```
[ function ] funname [()]

{

    action;

    [return int;]

}
```

 - 可以带function fun() 定义，也可以直接fun() 定义,不带任何参数。
 - 参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255)

 ```
 #!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"
```

 - 函数返回值在调用该函数后通过 $? 来获得
 - **所有函数在使用前必须定义**


### 函数参数

 > 同“传递参数”


## 输入/输出重定向

大多数 UNIX 系统命令从你的终端接受输入并将所产生的输出发送回​​到您的终端。一个命令通常从一个叫标准输入的地方读取输入，默认情况下，这恰好是你的终端。同样，一个命令通常将其输出写入到标准输出，默认情况下，这也是你的终端。

| 命令 | 说明 |
| ---- | ---- |
| command > file | 将输出重定向到 file。
| command < file | 将输入重定向到 file。
| command >> file | 将输出以追加的方式重定向到 file。
| n > file | 将文件描述符为 n 的文件重定向到 file。
| n >> file | 将文件描述符为 n 的文件以追加的方式重定向到 file。
| n >& m | 将输出文件 m 和 n 合并。
| n <& m | 将输入文件 m 和 n 合并。
| << tag | 将开始标记 tag 和结束标记 tag 之间的内容作为输入。

 > 0 通常是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）

### 输出重定向
```
command1 > file1
```
 - 执行command1然后将输出的内容存入file1
 - 任何file1内的已经存在的内容将被新内容**替代**
 - 要将新内容**添加**在文件末尾，要使用`>>`操作符

### 输入重定向
```
command1 < file1
```
 - 从文件读取内容作为输入的命令

 >同时替换输入和输出，执行command1，从文件infile读取内容，然后将输出写入到outfile中
 `command1 < infile > outfile`

### 重定向和Linux命令 

一般情况下，每个 Unix/Linux 命令运行时都会打开三个文件：

 - 标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据。
 - 标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据。
 - 标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息。
 - 默认情况下，command > file 将 stdout 重定向到 file，command < file 将stdin 重定向到 file。

---

 - 希望 stderr 追加到 file 文件末尾，可以这样写：
 `command 2 >> file`
   - `2` 表示标准错误文件(stderr)

 - 如果希望将 stdout 和 stderr 合并后重定向到 file，可以这样写：
 `command > file 2>&1`或`command >> file 2>&1`

 - stdin 和 stdout 都重定向，可以这样写：`command < file1 >file2`
   -  command 命令将 stdin 重定向到 file1，将 stdout 重定向到 file2。

### Here Document

Shell 中的一种特殊的重定向方式，用来将输入重定向到一个交互式 Shell 脚本或程序

基本形式：
```
command << delimiter
    document
delimiter
```
 - 将两个 delimiter 之间的内容(document) 作为输入传递给 command
 - 结尾的delimiter 一定要顶格写，前面不能有任何字符，后面也不能有任何字符，包括空格和 tab 缩进。
 - 开始的delimiter前后的空格会被忽略掉。

通过Here Document计算行数：
```
$ wc -l << EOF
    欢迎来到
    菜鸟教程
    www.runoob.com
EOF
3          # 输出结果为 3 行
$
```
 - Here Document也可以运用在脚本中。

### /dev/null 文件
希望执行某个命令，但又不希望在屏幕上显示输出结果，那么可以将输出重定向到 /dev/null

```
command > /dev/null
```
 - 写入到/dev/null的文件都会回归虚无，读取该文件是什么都读取不到的
 - 将命令的输出重定向到它，会起到"禁止输出"的效果

希望屏蔽 `stdout` 和 `stderr`，可以这样写：`$ command > /dev/null 2>&1`


## Shell文件包含
Shell 也可以包含外部脚本，格式如下：
`. filename`或`source filename`
 - 点号(.)和文件名中间有一空格

### 实例
创建两个 shell 脚本文件。

test1.sh ：
```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

url="http://www.runoob.com"
```
test2.sh ：
```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

#使用 . 号来引用test1.sh 文件
. ./test1.sh

# 或者使用以下包含文件代码
# source ./test1.sh

echo "菜鸟教程官网地址：$url"
```
 - test2.sh需要可执行权限，被包含的文件test1.sh不需要