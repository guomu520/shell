# sort 文本文件行排序

sort [OPTION]... [FILE]...

## 1、常用用法

### 1.1、sort file.txt
key点：不带任何参数，sort默认按照`字母`顺序`正`排序
```bash
$ cat file.txt
abc
def
ghi
abc
100
1
10
2
20
$ sort file.txt
1
10
100
2
20
abc
abc
def
ghi
```

### 1.2、sort -n file.txt
key点：-n（--numeric-sort），sort按照`数值`顺序`正`排序
```bash
$ cat file.txt
abc
def
ghi
abc
100
1
10
2
20
$ sort -n file.txt
abc
abc
def
ghi
1
2
10
20
100
```

### 1.3、sort -u file.txt
key点：-u（--unique），sort移除所有重复的行
```bash
$ cat file.txt
abc
def
ghi
abc
100
1
10
2
20
$ sort -n file.txt
1
10
100
2
20
abc
def
ghi
```

### 1.4、sort -r file.txt
key点：-r（--reverse），sort按照`字母`顺序`倒`排序
```bash
$ cat file.txt
abc
def
ghi
abc
100
1
10
2
20
$ sort -r file.txt
ghi
def
abc
abc
20
2
100
10
1
```

## 2、用法进阶

### 2.1、sort -t ' ' -k 3n,3 -k 4.3,4.3nr file.txt
```bash
$ cat file.txt
sina zy 72 175
baidu yf 52 174
baidu xl 52 176
mls ln 98 190
mls ht 72 180
$ sort -t ' ' -k 3n,3 -k 4r,4 file.txt
baidu xl 52 176
baidu yf 52 174
mls ht 72 180
sina zy 72 175
mls ln 98 190
$ sort -t ' ' -k 3n,3 -k 4.3,4.3nr file.txt
baidu xl 52 176
baidu yf 52 174
sina zy 72 175
mls ht 72 180
mls ln 98 190
```
key点：
* （1）-t（--field-separator=SEP）指定列分隔符
* （2）-k [ FStart [ .CStart ] ] [ Modifier ] [ , [ FEnd [ .CEnd ] ][ Modifier ] ] 从哪一列开始比较（或者哪一列的哪个字符），到哪一列结束（或者哪一列的哪个字符）（默认到最后一列最后一个字符）

```comment
FStart   从哪一列(域Field)开始（默认从第一列）
CStart   从当前列(域Field)的哪个字符(character)开始（默认从第一个）
Modifier 修饰，如n（numeric-sort）、r（reverse）等

FEnd     到哪一列(域Field)结束（默认到最后一列）
CEnd     到当前列(域Field)的哪个字符(character)结束（默认到最后一个）
Modifier 修饰，如n（numeric-sort）、r（reverse）等
```

### 2.2、sort a.txt b.txt
```bash
$ cat a.txt
a
b
$ cat b.txt
a
d
$ sort a.txt b.txt
a
a
b
d
```


### 2.3、sort 和awk的联合用法 
**根据姓名对文件块进行排序**
```bash
[work(0)@yz-lab-675 16:39:59 ~]# cat a.txt 
J Luo #每个文件块由姓名、学校和地址组成
BeiJing University
BeiJing,China

Y Zhang
Vitory University
Melbourne, Australia

D Hou
BeiJing University
BeiJing,China

B Liu
Shanghai Jiaotong University
Shanghai,China
[work(0)@yz-lab-675 16:40:04 ~]# cat a.txt | awk -v RS="" '{gsub("\n","@");print}'| sort | awk -v ORS="\n\n" '{gsub("@","\n");print}' #将每个文件块合并到一行，对每行的记录排序，将排序后的行分块打印
B Liu
Shanghai Jiaotong University
Shanghai,China

D Hou
BeiJing University
BeiJing,China

J Luo
BeiJing University
BeiJing,China

Y Zhang
Vitory University
Melbourne, Australia
```
