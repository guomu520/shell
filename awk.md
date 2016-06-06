# awk 文本处理

### 1、核心思想：
 * 程序语言；包含变量、算术、字符串操作符、循环、条件等
 * 数据驱动；描述你要处理的数据以及在在你找到他之后要做什么
 * 结构化的数据；所有操作的关键，没有结构化的数据，就不能找到pattern，就无从action

### 2、语法：
```bash
pattern {action}
pattern {action}
...
```

### 3、运行方式：
* （1）awk [options] [--] program-text    file ...
* （2）awk [options] -f program-file [--] file ...

### 4、常用的选项：
* -F '[' ：指定用于输入数据的列分隔符[
* -v var=value ：在awk程序执行之前（BEGIN区块）指定一个值value给变量var
* -f program-file ：指定一个awk程序文件，代替直接指定awk指令
* -- ：根据POSIX参数解析约定，此选项表示命令行选项的结束。

### 5、条件语句
if (conditon1) body1 [else if (condition2) body2] [else body3]
```bash
$ cat file.txt
miaoyongfei-57
oulinan-98
zhaoxianlie-60

$ awk 'BEGIN {FS="-"} {if ($2 < 58) {print "weight < 58KG : "$1} else if ($2 > 90) {print "weight > 90KG : "$1} else {print "weight >= 58kG && weight <= 90KG : "$1}}' file.txt
weight < 58KG : miaoyongfei
weight > 90KG : oulinan
weight >= 58kG && weight <= 90KG : zhaoxianlie
```

### 6、变量和操作符
```bash
$ cat file.txt
miaoyongfei-57
oulinan-98
zhaoxianlie-60

$ awk 'BEGIN {n=0} {n++} END {print n}' file.txt
3
```
|运算|符号|表达式|
|-|
|加法|`+`|n=n+3|
|减法|`-`|n=n-3|
|乘法|`*`|n=n*3|
|除法|`/`|n=n/3|
|取余|`%`|n=n%3|
|幂乘|`^`或者`**`|n=n^3 或者 n=n**3|
|自加一|`++`|n++|
|自减一|`--`|n--|
|赋值||n+=3,n-=3,n*=3,n/=3等|

### 7、特殊变量（内置变量）
| 变量名称 | 语义说明 | 额外说明 | case |
|-|
|    $0    | 当前行数据                  | awk会自动将此变量的值设置为当前行数据 | awk '{print $0}' file.txt |
|  $1 ~ $n | 当前记录的第n个字段，字段之间FS分隔 | awk会自动将对应的字段赋值给对应变量$n | awk '{print $1,$2}' file.txt|
|-|
|    FS    | （Field Separator）列分隔符 | 不一定是单个字符，可以是正则表达式 | awk 'BEGIN {FS="\t+"} {print $1}' file.txt |
|    RS    | （Row Separator）输入的数据的记录(行)分隔符 | 默认：换行符| awk 'BEGIN {FS=" ";RS="\t"} {print $0}' file.txt |
|-|
|    OFS   | （Output Field Separator）输出的列分隔符 | 默认：换行符| awk 'BEGIN {FS="\t+";OFS=" [ "} {print $1,$2}' file.txt |
|    ORS   | （Output Row Separator）输出的行分隔符| 默认：一个空格 | awk 'BEGIN {RS="\t+";ORS="\r\n"} {print $0}' file.txt |
|-|
|    NF    | （Number of Field）列的数量 | awk会自动将此变量的值设置为当前记录中列的个数 | awk 'NF == 3 {print $0}' file.txt |
|    NR    | （Number of Row）行的数量   | awk会自动将此变量的值设置为当前记录的行数，从1开始 | awk '{if (NR > 2) {print NR".\t"$0}}' file.txt |
|-|
|   FNR    | （Front Number of Row）当前的行号 | awk会自动将此变量的值设置为当前记录的行号，从1开始 | awk '{print FNR"\t"$0}' file.txt |
|-|
| FILENAME | 当前文件的名字 | awk会自动将当前文件的名字赋值给FILENANE | awk '{print FILENAME}' file.txt |
|FIELDWIDTHS| 输入字段宽度的空白分隔字符串 | 默认是空格 | $ cat file.txt<br>20151126<br>$ awk 'BEGIN {FIELDWIDTHS ="4 2 2"} {print $1,$2,$3}' file.txt<br>2015 11 26 |
|   OFMT   | （Output ForMaT） | 默认：%.6g | $ awk 'BEGIN {OFMT="%.3f"} {print 2/3,123.111111111}' file.txt<br>0.667 123.111 |

### 8、循环（while、for）
（1）while语法
```bash
while (condition)
    body
```
case
```bash
$ cat file.txt
beijing shanghai shengzhen
hangzhou tianjin nanjing
quzhou jinhua zunyi

$ awk '{
    i=2;
    while (i < 2) {
        print $i
        i++
    }
}' file.txt

```
（2）do while语法
```bash
do {
    body
} while (condition)
```
case
```bash
$ cat file.txt
beijing shanghai shengzhen
hangzhou tianjin nanjing
quzhou jinhua zunyi

$ awk '{
    i=2;
    do {
        print $i
        i++
    } while (i < 2)
}' file.txt
shanghai
tianjin
jinhua
```
（3）for语法
```bash
for (init; condition; increment) 
    body
```
case
```bash
$ cat file.txt
beijing shanghai shengzhen
hangzhou tianjin nanjing
quzhou jinhua zunyi

$ awk '{
    for (i = 1; i < 2; i++) {
        print $1
    }
}' file.txt
beijing
hangzhou
quzhou
```
