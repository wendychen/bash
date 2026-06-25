### bash 找出資料夾中最後更新的10個.md file

```bash
ls -lt *.md | head -n 10
```

### 怎麼計算當前folder內多少檔案?

```bash
find . -maxdepth 1 -type f | wc -l
```

### 怎麼一次編輯多個檔案?

vim file1.txt file2.txt file3.txt

### 但是不知道是怎麼一個一個看下一個檔案的?

Gemini:

切換至下一個檔案：輸入 :n 後按下 Enter。
切換至上一個檔案：輸入 :N 後按下 Enter。
直接切換到指定編號：輸入 :buffer 編號（例如 :buffer 2）或直接輸入 :b編號。

### 怎麼在vim中呼叫計算機?

Insert Mode -> `Ctrl+R + =` => 輸入數值 -> 輸出的數值會顯示在文件中

### 怎麼在ubuntu的terminal中進行計算?

1. 直接 `echo $((3+2))` 計算
2. bc (如果沒有安裝sudo apt-get install bc)

### 怎麼自動備份?


