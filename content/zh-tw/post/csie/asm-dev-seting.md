---
title: 組合語言開發環境設定
date: 2022-10-10 22:09:59
cover:
top_img:
categories:
    - 計算機科學
tags:
    - Linux
    - 組合語言
---
之前曾經嘗試在Windows上學寫組合語言，得到的回饋只有滿滿的問號。編譯過程出現了很多跟在Linux上不同的例外，這更證明了學習程式語言不難，難的是設定開發環境。
山不轉路轉路不轉人轉，我們直接用WSL上的環境去開發，就可以直接省去很多只會阻饒你學習的問題。而關於Windows Terminal和WSL的安裝可以參考[Before the Course](./csie/missing-semester/missing-semester-00/)

# 編譯工具
回歸正題，編譯組合語言會需要兩個程式: `nasm`、`ld`。`nasm`是用來把`.asm`檔轉成`.o`檔，而`ld`則是再把`.o`轉成可以執行的檔案。

## 更新 apt
安裝套件前要把apt更新上去，不然有機會會找不到東西安裝冏事發生(本人我還真的卡了一下)
```bash WSL command:("[root@localhost] $":1-2)
sudo apt-get update
sudo apt upgrade
```

## nasm
其實安裝NASM很簡單，直接用Ubuntu內建的套件管理包安裝就行了。
```bash WSL command:("[root@localhost] $":1)
sudo apt install nasm
```

## ld
ld的話在GCC裡面有內建，所以如果要裝的話要裝GCC，也就是編譯C/C++的工具。
```bash WSL command:("[root@localhost] $":1)
sudo apt install nasm
```