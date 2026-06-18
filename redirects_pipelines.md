## Redirects & Pipelines

### Standard Streams (stdin/stdout/stderr)

每個程式運行時, Linux都自動給它打開三條通道:

名字		編號	默認來源/去向 	 用途
stdin		0	鍵盤輸入	 程序讀取輸入
stdout		1	終端屏幕	 程序正常輸出
stderr		2	終端屏幕	 程序錯誤輸出


鍵盤 -> [ stdin (0) ] -> 程序 -> [ stdout (1) ] -> 屏幕
			     --> [ stderr (2) ] -> 屏幕

### stdout 重定向 `>`

```bash
>  	# 輸出重定向 (覆蓋)
>> 	# 輸出重定向 (追加)
<	# 輸入重定向
2>	# 錯誤重定向
```

```bash
echo "hello" > output.txt

echo "world" > output.txt

cat output.txt
```

可以使用 `-n` 抑制換行:

```bash
echo -n "hello" > output.txt
echo -n " world" >> output.txt
cat output.txt
```

也可以使用 `printf`:

```bash
printf "hello" > output.txt
printf " world\n" >> output.txt
cat output.txt
```

### stderr 重定向 `2>`

```bash
ls 不存在的文件 2> error.txt

cat error.txt
```

結果是:
`ls: cannot access '不存在的文件': No such file or directory`

所以透過 `2> error.txt` 可以寫入錯誤訊息到error.txt


### stdout + stderr 分別重定向

```bash
ls 存在的文件 不存在的文件 > out.txt 2> err.txt
```
這樣可以把 `ls 存在的文件`的正常結果redirect到out.txt
把 `ls 不存在的文件`的錯誤訊息redirect到err.txt


### stdout + stderr 合併

```bash
# 把 stderr 合并到 stdout（最常用写法）
ls 存在的文件 不存在的文件 > all.txt 2>&1

# 新写法（bash 4+）
ls 存在的文件 不存在的文件 &> all.txt
```
2>&1 意思是：把2号通道 接到 1号通道现在指向的地方

### stdin 重定向 `<`

```bash
# 从文件读取输入，而不是键盘
cat < input.txt

# 实际例子：把文件内容喂给命令
sort < names.txt
```

### 丟棄輸出（黑洞） `/dev/null`

```bash
# 不想看到正常输出
ls > /dev/null

# 不想看到错误信息（最常用！）
ls 不存在 2> /dev/null

# 什么都不想看到
ls 不存在 &> /dev/null
```

### 管道 `|` （stdout 接 stdin）

```bash
# 把前一个命令的 stdout 接到下一个命令的 stdin
cat file.txt | grep "hello" | sort | uniq
#     ↓stdout      ↓stdin stdout↓    ↓stdin
```

### 總結一張圖

```bash
命令 < input.txt	# stdin 從文件讀
命令 > output.txt	# stdout 寫到文件
命令 >> output.txt	# stdout 追加到文件
命令 2> error.txt	# stderr 寫到文件
命令 2>&1		# stderr 合併到 stdout
命令 &> all.txt		# stdout+stderr 都寫到文件
命令 2> /dev/null	# 丟棄 stderr
命令1 | 命令2		# stdout 接到下一個 stdin
```

