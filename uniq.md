# uniq [相邻行]文本去重
uniq [OPTION]... [INPUT [OUTPUT]]

## 1、-c（--count）、-d（--repeated）、-D（--all-repeated）、-u（--unique）、-f（--skip-field=N）
```bash
$ cat uniq.txt
a
b
a
a
c
d
f

$ uniq -c uniq.txt
      1 a
      1 b
      2 a
      1 c
      1 d
      1 f

#只显示重复的，并只显示一次
$ uniq -d uniq.txt
a

#只显示重复的，但是都显示
$ uniq -D uniq.txt
a
a

#只显示非重复的
$ uniq -u uniq.txt
a
b
c
d
f

$ cat uniq2.txt
a 1
a 2
b 1
c 1
d 2
#相邻行去重
$ uniq uniq2.txt
a 1
a 2
b 1
c 1
d 2
#忽略第一列，即从第二列开始去重
$ uniq -f 1 uniq2.txt
a 1
a 2
b 1
d 2
```

## 2、和sort联合使用，才能实现当前所有数据行去重
```bash
$ cat uniq.txt
a
b
a
a
c
d
f
#相邻行去重
$ uniq -c uniq.txt
      1 a
      1 b
      2 a
      1 c
      1 d
      1 f
#所有数据行去重
$ sort uniq.txt | uniq -c
      3 a
      1 b
      1 c
      1 d
      1 f
```

