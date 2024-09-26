---
title: 'OverTheWire: Bandit 解題筆記｜Level 1 → Level 2'
date: 2024-05-25T00:46:14+08:00
image: 
math: true
comments: true
categories:
- OverTheWire
- Bandit
tags:
- OverTheWire
- Linux
- 資訊安全
---
# Bandit: Level 1 → Level 2
## 登入
```shell
$ ssh -p 2220 bandit1@bandit.labs.overthewire.org
```
密碼：`ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

## 題目
**關卡目標**
下一關的密碼存儲在主目錄中的一個名為-的文件中。

**你可能需要用到的命令**
[ls](https://man7.org/linux/man-pages/man1/ls.1.html), [cd](https://man7.org/linux/man-pages/man1/cd.1p.html), [cat](https://man7.org/linux/man-pages/man1/cat.1.html), [file](https://man7.org/linux/man-pages/man1/file.1.html), [du](https://man7.org/linux/man-pages/man1/du.1.html), [find](https://man7.org/linux/man-pages/man1/find.1.html)

**有用的閱讀資料**
- [Google 搜索 “dashed filename”（帶破折號的文件名）](https://www.google.com/search?q=dashed+filename)
- [Advanced Bash-scripting Guide - Chapter 3 - Special Characters](http://tldp.org/LDP/abs/html/special-chars.html)

<!--more-->

## 解題思路

## 詳解

```shell
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

[OverTheWire: Bandit 解題筆記｜Level 2 → Level 3](/FMhBk2TQSUmGUh-yTerFwg)