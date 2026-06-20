# Input/Output

source: https://ryanstutorials.net/bash-scripting-tutorial/bash-input.php


introduction.sh

```bash
#!/bin/bash
# Ask the user for their name
echo Hello, who am I talking to?
read varname
echo It\'s nice to meet you $varname
```

login.sh

```bash
#!/bin/bash
# Ask the user for login details
read -p 'Username: ' uservar
read -sp 'Password: ' passvar
echo
echo Thankyou $uservar we now have your login details
```

-p 是 prompt
-sp 是 silent prompt (不要顯示input)


summary.sh

```bash
#!/bin/bash
# A basic summary of my sales report
echo Here is a summary of the sales data:
echo ====================================
echo
cat /dev/stdin | cut -d' ' -f 2,3 | sort
```

接著這段是建立 `salesdata.txt` 然後把 `salesdata.txt`裡面的資料透過cat餵給./summary:

```bash
cat salesdata.txt
Fred apples 20 June 4
Susy oranges 5 June 7
Mark watermelons 12 June 10
Terry peaches 7 June 15
cat salesdata.txt | ./summary
```




