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

