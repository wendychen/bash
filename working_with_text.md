---
title: "Learning Log"
author: "Wendy Chen"
date: "`git log -1 --format=%ad --date=short`"
CJKmainfont: "WenQuanYi Zen Hei Mono"
fontsize: 12pt
linestretch: 1.5
geometry: margin=2.5cm
---

# Bash

# Bash Scripting

## Analysis

### wc

指令:
```bash
wc -l config.txt
wc -w config.txt
```

-l 只顯示行數 (lines)
-w 只顯示詞數 (words)
-c 只顯示字節數 (characters)


結果:

w config.txt

指令:

```bash
wc config.txt
```

結果:
3 3 40 config.txt

3 - lines -l
3 - words -w
40 - bytes -c

第一個3是行數, 第二個3是單詞數, 第三個40是字節數.

練習題:
```bash
echo -e "蘋果\n香蕉\n橘子" | wc -l
```

然後把-l改成-w, -c


### sort

```bash
echo -e "3\n1\n2\n4\n2\n7\n" | sort -n
echo -e "3\n1\n2\n4\n2\n7\n" | sort -nr
```

r是reverse, 倒著排. `sort -n`是正著排.

### uniq

```bash
echo -e "wendy\nwendy\nchen\nwendy" | uniq
echo -e "wendy\nwendy\nchen\nwendy" | uniq -c
```

-c 可以計算每個unique詞出現的幾次

### nl

```bash
echo -e "第一句話\nRUST\n第三句話" | nl
```

nl是number lines, 可以為每一行加上行號

所以我們也可以這樣做:

```bash
cat app.log | nl
```

把app.log裡面的內容取出來, 加上編號.


這個語法可以讓所有行都加上編號:

```bash
nl -ba FILE_NAME
```

舉例比較:

```bash
wendy:~/projects/bash$ cat fruit.txt | nl
     1  apple 10 red
     2  banana 5 yellow


     3  cherry 20 purple
     4  orange 15 orange
wendy:~/projects/bash$ cat fruit.txt | nl -ba
     1  apple 10 red
     2  banana 5 yellow
     3
     4
     5  cherry 20 purple
     6  orange 15 orange
```


### 綜合應用

媽想知道, 一堆水果裡, 每種出現幾次, 從多到少排好, 還編上號:

```bash
echo -e "蘋果\n香蕉\n蘋果\n橘子\n蘋果\n香蕉" | sort | uniq -c | sort -nr | nl
```

nl負責標, wc負責數, sort負責排, uniq負責併.
遵守Unix哲學: 每個指令只做一件事, 用管道 | 串起來, 成了分析流水線.


## mkdir

wow i love this:

```bash
mkdir -p ~/exam/{logs,src/{java,python},config,backup}
```

a simple way to represent a tree structure in one line.
it saves cpu & gpu (i guess).


--
# Working with Text

## combination skill

grep + head + tail + find + cut + paste + join + split + tr + sed + awk


先建立一個練習文件:

```bash
cat > staff.txt << 'EOF'
101,Alice,Engineering,90000
102,Bob,Marketing,75000
103,Carol,Engineering,95000
104,Dave,Marketing,70000
105,Eve,Engineering,88000
EOF
```

### View & Search

找出所有的Engineering:

```bash
grep "Engineering" staff.txt
```

打印staff.txt的首三行:

```bash
head -n 3 staff.txt
```

打印staff.txt的末兩行:

```bash
tail -n 2 staff.txt
```

在當前目錄中找尋所有.txt文件:

```bash
find . -name "*.txt"
```

### Text Transform

在staff.txt這份文件中, 只取出名字:

```bash
cut -d',' -f2 staff.txt
```

在staff.txt這份文件中, 首先, 只cut出名字, 存到name.txt.
接著, 只cut出名字, 存到salaries.txt.
之後, 把name.txt 和 salaries.txt paste在一起打印:

```bash
cut -d',' -f2 staff.txt > names.txt
cut -d',' -f4 staff.txt > salaries.txt
paste names.txt salaries.txt
```

join 用共同字段合併兩個文件:

```bash
cat > dept.txt << 'EOF'
Engineering NewYork
Marketing London
EOF

awk -F',' '{print $3,$2}' staff.txt | sort > staff_dept.txt
sort dept.txt > dept_sorted.txt
join staff_dept.txt dept_sorted.txt
```

split 把文件每2行切成小文件:

```bash
split -l 2 staff.txt part_
cat part_aa
cat part_ab
```

tr - 把所有小寫換成大寫

```bash
cat staff.txt | tr 'a-z' A-Z'
```

sed - 把 Marketing 全部換成 Sales

```bash
sed 's/Marketing/Sales/g' staff.txt
```

```bash
awk -F',' '$4 > 80000 {print $2, $4}' staff.txt
```



## grep v.s. find

grep 是找內容, find 是找文件.

grep 是在文件內容裡搜尋.

## grep

grep [什麼參數] [查找什麼內容] [在什麼位置]
e.g.

```bash
cd ~/practice/project
grep "ERROR" logs/server.log
```

相當於先移動到 ~/practice/project
然後使用grep, 找出 logs/server.log 這份文件裡面包含 ERROR 的所有lines

我們可以加入一些常用參數, 例如 -n 顯示行號, -i 忽略大小寫. 也可以組合參數, 例如 -ni 就是顯示行號並且忽略大小寫.


```bash
grep -ic "info" ~/exam/logs/app.log
```

使用grep找出現在目錄中包含tax字串的結果, ignore大小寫, recursive遞迴的尋找, number列出行號

```bash
grep -rin "tax" .
```

列出歷史中使用的指令, 其中, 使用grep找出grep字串

```bash
history | grep "grep"
```

```bash
grep -r "React" src/
```

-r 是遞迴搜索. 這行指令是, 在 src/ 這資料夾裡面搜索,
搜索 React 這個詞, 包含這個詞的那個line, 列出path和內容.


## find

find 從哪找 -條件


```bash
find . -name "*.js"
```

從當前目錄及其子目錄, 找出所有.js的文件


```bash
find ~/practice -type f
```

在 ~/practice 這個目錄下, 了解什麼的type?
f = file (一般檔案)
`-type f` 只搜尋普通檔案(regular file)


搜尋最近7天改過的文件. mtime = modify time

```bash
find . -mtime -7
```

在working directory找檔名, 不分大小寫, 所以JPG, jpg. Jpg之類的都會找. *是不限內容, .JPG代表結尾需要.jpg但是不分大小寫 

```bash
find . -iname "*.JPG"
```

在working directory找出size大於100M的files

```bash
find . -size +100M
```

find進階(還沒用過)

```bash
find . -name "*.xx" -delete
find . -name "*.xx" -exec 命令 {} \;
```

{} => 找到的每個文件
\; => 命令結束

後面這行 find + exec 就是找到檔案並且做事.
舉一個例子：

```bash
find ~/findlab -name "*.log" -exec echo "找到了：" {} \;
```

先從findlab這個資料夾裡面，遞迴找出所有.log檔案，接著執行命令：
對於找到的每一個檔案，echo `找到了：` 加上檔案名稱，最後的 `\`代表命令結束。


使用find找出~/exam 下的所有directory:

```bash
find ~/exam/ -type d
```

## Wildcards

Wildcards 大陸叫做"通配符".

### *

星號是隨便什麼都行.

### ?

問號是單一替代符.


### [...]

方括號是 只代表括號內列出的其中1個字符.

例如說:

```bash
ls file[123].txt
```

合法的是 `file1.txt`, `file2.txt` 和 `file3.txt`

也可以改成寫範圍, 例如說:

```bash
ls file[a-z].txt
ls file[0-9].txt
```
從括號內指定的範圍中挑選的任一個字符皆合法.

### {...}

花括號是"手動列表符".
就是自己列出自己想要打撈/創建的東西.
例如說:

```bash
ls {cat,dog,bird}.txt
```

就會列出 `cat.txt`, `dog.txt` 和 `bird.txt`
並且, 逗號的之前和之後是不能有空白的.

我們也可以用{...}一次建立三個文件, 例如:

```bash
mkdir folder{1,2,3}
```

就會建立 `folder1`, `folder2` 和 `folder3`.


