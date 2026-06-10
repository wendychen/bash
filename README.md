---
title: "Learning Log"
author: "Wendy Chen"
date: "2026-06-06"
CJKmainfont: "WenQuanYi Zen Hei Mono"
fontsize: 12pt
linestretch: 1.5
geometry: margin=2.5cm
---

# Bash

## vim

```bash
ctrl + f: forward
ctrl + b: backward
```

scroll the full page.

```bash
ctrl + u: up
ctrl + d: down
```

scrol half the page.



## awk

```bash
awk '{ print $1 }' log.txt
```

找出log.txt, 打印每行第1列

公式:

```bash
awk 'pattern { action }' file
```

## .md to .pdf

```bash
pandoc learning_log.md -o learning_log.pdf \
  --pdf-engine=xelatex \
  --from markdown+hard_line_breaks
```

```bash
okular.exe learning_log.pdf
```

先用pandoc將md轉成pdf, 使用指定的pdf-engine. 這裡需要先確保套用指定的中文字型, 使用fc-list查看支援的中文字型,
並且需要將markdown的new line解讀為pdf的new line.
然後在.md的開頭寫YAML的資訊, 包含指定顯示的中文字型. 然後用okular這個軟體查看pdf.
okular這個軟體可以做annotation

## fc-list

```bash
fc-list :lang=zh | cut -d: -f2 | sort -u
```

## seq

```bash
seq 1 50 > numbers.txt
```
seq = sequence

## sed

```bash
sed -i 's/localhost/127.0.0.1/g' config.txt
```
-i = in-place
g = global

在config.txt中, 找localhost, 替換成127.0.0.1



## head & tail

```bash
head numbers.txt
```
預設顯示首10行

```bash
tail numbers.txt
```
預設顯示末10行

```bash
head -n 15 numbers.txt
```
首15行

```bash
tail -n 15 numbers.txt
```
末15行

```bash
tail -n +15 numbers.txt
```
從第15行開始到最後

```bash
head -n 2 numbers.txt app.log
```
兩個檔案的首2行都印出來

## tail - monitor log

```bash
tail -f app.log
echo "2026-05-30 ERROR 新錯誤!" >> app.log
```

先開一個real-time監控日誌, 另開一個terminal, echo一個新entry到app.log
本來監控日誌裡就會即時看到答案

```bash
tail -n -30 us_tax_tool2.md | head -n 20
```
找出特定的paragraph, 或指定lines來閱讀. tail -n -30 us_tax_tool2.md是從這md file裡面找出倒數(tail)30行, 加上行號(-n = -number),
並且, 在這30行中, 取出首(head) 20行, 加上行號

# less

less 算是...閱讀器?

```bash
less numbers.txt
```

進去之後, j下一行, k上一行, 空格 到下一頁, b 回上一頁, q退出

```bash
less app.log
```

輸入/ERROR 搜索"ERROR"字串, 所有匹配結果會反白, n跳到下一個匹配, N跳到上一個匹配

-> 重複使用這技能來查詢文件

------------------------------------------------

## Bash Scripting

### Analysis

#### wc

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


#### sort

```bash
echo -e "3\n1\n2\n4\n2\n7\n" | sort -n
echo -e "3\n1\n2\n4\n2\n7\n" | sort -nr
```

r是reverse, 倒著排. `sort -n`是正著排.

#### uniq

```bash
echo -e "wendy\nwendy\nchen\nwendy" | uniq
echo -e "wendy\nwendy\nchen\nwendy" | uniq -c
```

-c 可以計算每個unique詞出現的幾次

#### nl

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


#### 綜合應用

媽想知道, 一堆水果裡, 每種出現幾次, 從多到少排好, 還編上號:

```bash
echo -e "蘋果\n香蕉\n蘋果\n橘子\n蘋果\n香蕉" | sort | uniq -c | sort -nr | nl
```

-------------------------------------------------



## mkdir

wow i love this:

```bash
mkdir -p ~/exam/{logs,src/{java,python},config,backup}
```

a simple way to represent a tree structure in one line.
it saves cpu & gpu (i guess).

## grep v.s. find

grep 是找內容, find 是找文件

## grep

grep [什麼參數] [查找什麼內容] [在什麼位置]
e.g.

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

## find
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


使用find找出~/exam 下的所有directory:

```bash
find ~/exam/ -type d
```

## Job Control


你是廚房老闆(bash), 你手下有很多的任務(job),
比如:煮一鍋湯, 炒一盤菜.

前台 foreground: 這道菜正站著你全部注意力, 你站旁邊盯著它, 別的啥也幹不了.
後台 background: 這道菜丟一邊自己慢慢燉, 你騰出手去幹別的.
掛起 suspend: 把火關了, 菜暫停在那兒, 等你回頭處理.

所以, fg就是拉到前台, bg就是拉去後台, Ctrl+Z暫停當前任務, 像是關火.
jobs看看現在有那些任務

[1] 25647

代表是Job 1, 然後Process ID是25647



