---
title: "Learning Log"
author: "Wendy Chen"
date: "`git log -1 --format=%ad --date=short`"
CJKmainfont: "WenQuanYi Zen Hei Mono"
fontsize: 12pt
linestretch: 1.5
geometry: margin=2.5cm
---

# Networking

## ping

ping 是為了測試IP (Internet Protocol)網路上的某個host的reachability.
透過傳送封包 (packets)給target host, 等待packets回傳, 來達成目的.
傳送的封包叫做ICMP的"echo request", ICMP是Internet Control Message Protocol.
傳回的封包是ICMP的"echo reply".

ping 指令會評估這些封包的round-trip time (RTT),
指出連線延遲(latency of the connection),
並回報任何的封包遺失(packet loss).

### 解讀回傳訊息

```bash
64 bytes from 8.8.8.8: icmp_seq=1 ttl=111 time=10.9 ms
```

64 bytes from 8.8.8.8: 從8.8.8.8收到了64字節的回覆
icmp_seq=1:            seq表示sequence, 序列. icmp_seq=1代表第一個packet
ttl=111:               ttl = time to live, 存活時間. 表示這個packet還能經過多少個router.
                       初始值通常是 64/128/255, 這裡是111, 表示中途經過了一些router跳轉.
time:                  10.9ms, 往返時間. 從發出到收回回覆花了10.9ms.
