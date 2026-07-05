# Error Handling

The methods and techniques used to detech, manage, and respond to errors that occur during the execution of a script.

It involves:

- Checking the exit status of commands
- Using conditional statements to handle different error scenarios
- Implementing mechanisms to gracefully exit or recover from errors, ensuring the script's reliability and preventing unexpected behavior.


## exit status

每條命令執行完, 都會返回一個數字, 代表退出狀態.
`0`表示成功, 非`0`表示失敗, 用`$?`查看退出狀態.

## set -e

`set -e`的設定是"一出錯就停".
`-e` 代表 errexit.

## set -o

`set -o errexit` 等於 `set -e`
`set -o nounset` 等於 `set -u`
`set -o xtrace` 等於 `set -x`

`set -o`是`set -e`, `set -u`, `set -x`的長寫法.
腳本開頭直接寫`set -euo pipefail`, 三合一, 是業界慣例. (這指令什麼意思? 我看不懂)


## set -u

`set -u`是用了沒有定義的variable, 就會報錯.
`-u`代表nounset

## trap

trap: 不管腳本怎麼結束, 都會有的收尾工作

## Error Logging

錯誤日誌是記錄script運行時"發生錯誤的過程",
包括記錄: 1) 錯誤類型 2) 發生時間 3) 出錯的代碼位置.

## set -euo pipefail

`-o pipefail`, 取的是管線(pipe)的回傳值, 取最後一個失敗指令的狀態.

如果沒有pipefail, `false | true`會回傳0, 因為只看true.
如果有pipefail, `false | true`會回傳非零，因為false失敗了.

簡言之, `set -euo pipefail`的遵守的是fail-fast, `快速失敗, 明確報錯`原則,
寫了這行之後, 程式碼會在遇到任何錯誤時立即停止.

