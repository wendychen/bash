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

## watch

我的理解:
可以 `watch ls`, 但是不能 `watch ll`, 也就是說無法 `watch` 某個 alias. 

Gemini說是, watch常用在:

- 監控系統資源
- 監控進度或狀態
- 監控API或網路服務

## crontab

先用 `crontab -e` 進入定時任務頁面, 再設定什麼時間要做什麼.
我自己嘗試了crontab東西, 然後用`watch ls`監看變化, 是成功的.
問AI是不是好的做法. 結果查到watch的其他用法. 


