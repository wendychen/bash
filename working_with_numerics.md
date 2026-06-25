# Working with Numerics

原來bash原生的`$((...))`只能做整數運算

Try:

```bash
echo "10/3" | bc -l
echo "scale=2; 10/3" | bc
```

算個圓周率:

```bash
result=$(echo "scale=4; 22/7" | bc)
echo "$result"
```

