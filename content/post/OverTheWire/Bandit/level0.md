---
title: 'OverTheWire: Bandit 解題筆記｜Level 0'
date: 2024-05-24T00:33:14+08:00
image: 
math: true
license: 
hidden: false
comments: true
categories:
- OverTheWire
- Bandit
tags:
- OverTheWire
- Linux
- 資訊安全
---
# Bandit: Level 0
**關卡目標**
這一關的目標是讓你使用 SSH 登入遊戲。你需要連接的伺服器是 `bandit.labs.overthewire.org`，埠 `2220`。用戶名是 `bandit0`，密碼是 `bandit0`。登入後，請前往 [第 1 關](https://overthewire.org/wargames/bandit/bandit1.html) 頁面，了解如何通過 [第 1 關](https://overthewire.org/wargames/bandit/bandit1.html) 。

<!-- more -->

**你可能需要用到的指令**
- [ssh](https://man7.org/linux/man-pages/man1/ssh.1.html)

**有用的閱讀資料**
- [Secure Shell (SSH) on Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell)
- [How to use SSH on wikiHow](https://www.wikihow.com/Use-SSH)

## 解題思路
從題目可以知道，要進入遊戲要透過 SSH 登入遠端的主機。所以我們的重點就是去了解要怎麼透過 `ssh` 指令來進入遠端的主機。

如果對題目的一些名詞不太熟悉的話這邊列出幾個會要了解的知識：
- [Wiki: IP 網際網路協定](https://zh.wikipedia.org/wiki/網際網路協定)
- [Wiki: 埠](https://zh.wikipedia.org/wiki/通訊埠)
- [Wiki: 域名](https://zh.wikipedia.org/wiki/域名)
- [Wiki: Secure Shell](https://zh.wikipedia.org/zh-tw/Secure_Shell)

那簡單來說，我們在使用網路上網的時候。網路上的資源是透過類似現實生活中的信件、包裹的方式傳送資料（網頁、影片...等等）。

就如同寄信的時候會需要寄件人以及收件人一樣，電腦也需要被編號成不同的地址，也就是所謂的 IP 地址（IP address）。

而埠（通訊埠，port），可以想像成一棟大樓的許多樓層及房間。在寄包裹時我們也會標示要給幾號幾樓幾室的某某某。在電腦和電腦之間溝通時，除了必須指定地址外，也必須標示清楚要透過哪一個埠來傳輸資料。

域名則是幫 IP 地址取一個綽號。人們可以用簡單易懂的名稱來取代原本一坨數字的 IP 地址，例如告訴你 `172.217.160.110` 這個 IP 地址，會知道這個地址是 Google(google.com) 的 IP 地址嗎？幾乎是不太可能。

SSH 是一種遠端連線到電腦的協定，可以透過加密方式建立安全的遠端連線。而我們通常會透過 `ssh` 來連接到其他電腦。

# 詳解
首先要先理解如何使用 `ssh`。這個我就直接問 Chat GPT 了。
:::info
連接到特定通訊埠：

如果 SSH 伺服器使用非默認通訊埠（22），可以使用 `-p` 選項指定通訊埠：
```
ssh -p port_number username@remote_host
```
:::
這就簡單了，以此類推，要連接上題目要求的伺服器可以這樣下指令：
```zsh
$ ssh -p 2220 bandit0@bandit.labs.overthewire.org
```
然後就會跳出一個大大的 BANDIT 要求你輸入密碼，這時把 `bandit0` 輸入進去就好（輸入沒顯示文字是正常的）。

那恭喜你成功進入了 level 0 🎉。成功登入之後，會顯示一大堆資訊在螢幕上，大致上在講這個遊戲的資訊、規則，可以斟酌閱讀。

接著就進入 [Level 0 → Level 1](/NbmShGg7RjqrfzCni_t3Mg) 吧。