## The output of `ls`

例如說:

```bash
-rw-r--r-- 1 root adm 48194 May 2 10:20 dmesg
```

- 代表file,
接下來3個字元一組,
`rw-`, `r--`, `r--`.
第一組是owner的權限, 第二組是group的權限, 第三組是other的權限.
再來那個1, 代表hard link.
再來root是Owner, 然後adm是Group.

## Permisson

關於權限設定, 分成rwx, read, write, execute.
然後配上數字0-7來設定permissions.

absolute mode:

digit	meaning
0	no access
1	execute
2	write
3	write+execute
4	read
5	read+execute
6	read+write
7	read+write+execute


## chgrp

`chgrp <group> <objects>`

```bash
drwxr-xr-x 2 student1 student1 4096 Jul  7 11:29 student1
root@ubuntu:/home/student1$ chgrp student2 student1
```

會變成:

```bash
drwxr-xr-x 2 student1 student2 4096 Jul  7 11:29 student1
```

