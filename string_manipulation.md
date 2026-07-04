# String Manipulation

## String Length

計算name這個字串的長度:

```bash
${#name}
```

也可以用這個方法:
```bash
expr length "my string"
```

也可以用這個方法:
```bash
echo "my string" | awk '{print length}'
```

也可以用這個方法:
```bash
echo -n "my string" | wc -m
```

## Substring Extraction

```
str="Slinky Dog"
echo ${str:7:3}
```

從第7個位置(從0開始算), 取3個字元, 輸出到stdout


## Pattern Replacement

```bash
str="Hello World"
echo ${str/World/Bash}
```

`${str/old/new}` -> 替換第一個匹配的`old`為`new`
`${str//old/new}` -> 替換所有匹配的`old`為`new`
`/` -> 單個鞋槓表示只替換第一個
`//` -> 雙斜槓表示替換全部

## Case Conversion

```bash
str="Hello World"
```

```bash
echo ${str^^}			
```
Convert to all uppercase.


```bash
echo ${str,,}
```

Convert to all lowercase.


```bash
echo ${str^}
```

僅將首字轉換成大寫.

```bash
echo ${str,}
```

僅將首字轉換成小寫.
