# System Monitoring

## free
```bash
free -htw -s 2 -c 3
```

-h human-redable	人類可讀 (電腦自動選擇最適的表達單位)
-t total		(RAM + Swap 合計)
-w width 		寬模式

## uptime

```bash
uptime -s
```
-s代表-since, 開機時間點

```bash
uptime -p
```
-p代表-pretty, show uptime in pretty format. 變成只顯示開機開了多久

```bash
uptime -V
```
-V代表-Version, 顯示版本, 然而我不知道是顯示什麼的版本.
我得到的結果是`update from procps-ng 4.0.4`, 是什麼意思呢?
`procps-ng 4.0.4`是什麼意思呢?


