## Setting Up Bash

### .bashrc

Linux:
~/.bashrc

Mac:
~/.bash_profile

打開來編輯:

nano ~/.bashrc
vim ~/.bashrc

改完之後生效:

source ~/.bashrc

rc stands for?

### Customize Prompt

Default:

```bash
user@hostname:~$
```

在 `~/.bashrc` 加入:

```bash
PS1="\u @ \w $ "
```


`\u` - username
`\h` - hostname
`\w` - working directory
`\t` - time

### aliases

aliases 是別名.

輸入 `alias`查看所有alias.
輸入 `unalias ll`取消 `ll` 這個alias.

