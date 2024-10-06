---
title: Lecture 1:Course Overview + The Shell
date: 2022-09-26 17:30:41
cover:
top_img:
categories: 
  - [計算機科學, ./missing-semester]
tags: 
    - 'Shell'
    - 'Terminal'
    - 'Linux'
---
MIT的教授們所開設的課程。每堂課都有[線上筆記](https://missing.csail.mit.edu/)可以參考。

# The Shell
當你打開Shell，統常只會有一行字在做上方，稱作**系統提示(Shell Prompt)**。
```bash
[root@localhost] $
```
上面有使用者名稱(user name)跟現在使用的機器名稱還有現在所在的路徑(path)。你可以在系統提示輸入指令Shell會解析指令，例如最簡單的指令便是執行一個程式且帶有引數(argument):
```bash Windows Terminal command:("[root@localhost] $":1)
date
Tue Sep 27 08:40:51 CST 2022
```
以date這隻程式來說，他會把現在的日期跟時間印在shell上。
那當然也可以使用帶有引數的程式:
```bash Windows Terminal command:("[root@localhost] $":1)
echo hello
hello
```


```bash Windows Terminal command:("[root@localhost] $":1)
```
