## Bash Scripting

### Common Mistake

1.
變數存值的時候不加$, 所以用age
取值的時候才加$, 用$age

2.
數字比較用 -lt / -gt

### 


```bash
#!/bin/bash

age=15

if [ $age -le 18 ]; then
  echo "Access denied."
  exit 1
else
  echo "Access granted."
  exit 0
fi
```
