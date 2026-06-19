# STOP EXECUTION

`exit` 後面帶的數字, 就叫做 Exit Code.

Exit Code	Meaning
Exit 0		成功
Exit 1		失敗

```bash
#!/bin/bash

echo "Step 1: Start checking..."

filename="error.txt"
if [ ! -f $filename ]; then
  echo "Error: $filename  NOT EXIST, STOP EXECUTION!"
  exit 1
fi

echo "Step 2: File exist, keep executing..."
echo "Step 3: Done!"
exit 0
```

實作上 `[`和`!]之間的空白是需要有的.

```bash
bash myscript.sh
echo $?
```

透過這個方式可以檢查上一個命令的 exit code.
