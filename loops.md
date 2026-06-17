## Loops

### for

```bash
for i in 1 2 3 4 5
do
    echo "这是第 $i 次"
done
```

```
for i in 5 4 3 2 1
do
    echo "倒数 $i"
done
echo "🚀 发射！"
```

```bash
for i in {1..5}
do
    echo "第 $i 次"
done
```

```bash
for i in {5..1}
do
    echo "倒数 $i"
done
echo "🚀 发射！"
```

```bash
for folder in work study game
do
    mkdir $folder
    echo "$folder 建立完成！"
done
```

### while


```bash
count=1
while [ $count -le 5 ]
do
    echo "数字是 $count"
    count=$((count + 1))
done
```
