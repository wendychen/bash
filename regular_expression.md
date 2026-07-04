
# Regular Expressions

regular expressions有分basic regex syntax和extended regular expressions.

Basic Regular Expressions, 叫做BRE.
Extended Regular Expressions, 叫做ERE.

BRE和ERE通用的部分:

```bash
符號 	含意 				示例 		匹配
.	任意單個字符			a.c		abc, a1c, a@c
^	前一個字符出現0次或多次		go*d		gd, god, good
$	行首錨點			^root		以root開頭的列
*	行尾錨點			sh$		以sh結尾的列
[abc]	字符類: a, b或c之一		[cb]at		bat, cat		
[0-9]	範圍:任意數字			[0-9][0-9]	00~99
\	轉义特殊字符			3\.14		字面的"3.14"
```

ERE:

```bash
元字符	  含意				示例		匹配
+	  前一個字符出現1次或多次	go+d		god, good(不匹配gd)
?	  前一個字符出現0次或1次	colou?r		color, colour
{n}	  恰好n次			[0-9]{3}	恰好3位數字
{n,m}	  n 到 m 次			a{2,4}		aa, aaa, aaaa
|	  或(alternation)	 	cat | dog	cat 或 dog	
()	  分組				(ab)+		ab, abab, ababab
```

```bash
grep -E 'go+d' test.txt
```
`-E` 代表啟用 延伸正規表達式(Extended Regular Expression, ERE).



