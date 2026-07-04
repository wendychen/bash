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


## rsync

這是做資料複製的, 最小化需要複製的東西.

```bash
rsync -av dir dir2
```

-a 代表歸檔模式, 保留權限, 時間戳, 軟link等 (不知道自己在說什麼)
-v 顯示詳細過程

## netstat / ss

netstat是舊的. ss是新的.

```bash
ss -tlnp | grep 3306
```
查看3306端口被誰占用
Port 3306 is the default TCP port used by the MySQL database management system to establish network connections, read and write data, and generate dynamic web content.

## ifconfig / ip

ifconfig是舊的. ip是新的.

如果服務器網路不通, 可以這麼做:

```bash
ip addr show
ip route show
ss -tulnp
```

第一行代表ip配置對不對? (不知道什麼意思.)
第二行問的是, 網關路由在不在?
第三行問的是, 服務端口起來沒?


