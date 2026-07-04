# File Compression

主要有tar, zip/unzip, gzip/gunzip, bzip2, xz 這些方法.

gzip 壓縮率一班, 速度最快, 用於日常快速壓縮, 日誌.
bzip2 壓縮率較高, 速度較慢, 用於中等大小文件壓縮.
xz 壓縮率最高, 速度最慢, 用嫆分發軟件包, 內核源碼等等.


```bash
gzip -l output.txt.gz
```

這可以查看壓縮率
