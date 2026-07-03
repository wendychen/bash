# Progress Management

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


## nohup

```bash
nohup ./age_checker.sh > age_output.log 2>&1 &
```

nohup是就算terminal關閉了也還回執行的process


## process substitution

# 比較兩個命令的輸出, 而無須創建中間文件
`diff <(ls dir1) <(ls dir2)`

上面這個嘗試了. 下面這兩個還沒嘗識

# 比較兩個遠程文件的內容
diff <(ssh server1 cat /etc/hosts) <(ssh server2 cat /etc/hosts)

# 將排序後的結果作為文件傳給join命令
join <(sort file1.txt) <(sort file2.txt)


