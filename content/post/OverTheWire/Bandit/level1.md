---
title: 'OverTheWire: Bandit 解題筆記｜Level 0 → Level 1'
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
# Bandit: level 0 → Level 1

## 登入
```shell
$ ssh -p 2220 bandit0@bandit.labs.overthewire.org
```
密碼：`bandit0`

## 題目
**關卡目標**
下一關的密碼存儲在家目錄（~/）中的一個名為 `readme` 的檔案裡。使用這個密碼通過 SSH 登入到 `bandit1`。每當你找到一個關卡的密碼時，使用 SSH（埠 2220）登入到該關卡，然後繼續遊戲。

**你可能需要用到的命令**
[ls](https://man7.org/linux/man-pages/man1/ls.1.html), [cd](https://man7.org/linux/man-pages/man1/cd.1p.html), [cat](https://man7.org/linux/man-pages/man1/cat.1.html), [file](https://man7.org/linux/man-pages/man1/file.1.html), [du](https://man7.org/linux/man-pages/man1/du.1.html), [find](https://man7.org/linux/man-pages/man1/find.1.html)

## 解題思路
這題的題目很明瞭的告訴你密碼就在 `~/readme` 檔案中。所以問題是要如何開啟這個檔案，獲取裡面儲存的密碼。

這題需要了解的電腦知識：
- 電腦檔案的路徑
- `ls`、`cd`、`cat` 指令

## 詳解
既然都知道是在 `readme` 檔案裡面了，就只要利用 `cat` 指令將檔案內容印出即可。
```shell
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```
於是我們就可以輸入
```shell
$ exit
```
或著是按下鍵盤 `Ctrl` + `D`，退出連線，然後連接到 `bandit1` 的帳號
```shell
$ ssh -p 2220 bandit1@bandit.labs.overthewire.org
```
然後輸入剛剛拿到的密碼，進入 Level 1。

[Level 1 → Level 2](/l4ww02JDQz2gelf_PNMlnQ)