---
title: 悠遊卡的資安問題
slug: the-security-of-easy-card-payment
date: 2024-02-26 00:00:00+0000
image: cover.png
categories:
    - 計算機科學
tags:
    - 資訊安全
    - RFID
---
近期悠遊卡公司與Apple進行把悠遊卡加到Apple的支付的事件，在網路上引發熱烈討論。然而，悠遊卡的資安問題也再度受到關注。

## 悠遊卡的運作原理

悠遊卡系統主要是應用 **法拉第電磁感應定律** 來傳遞資訊。卡片內部有埋設線圈，當卡片靠近讀卡機時，讀卡機所產生的電場會讓線圈產生電流，供應給裡面的晶片（IC）產生電磁波訊號，再由讀卡機接收並解析資料。

這個技術被稱為「無線射頻辨識系統」（radio frequency identification，RFID），而悠遊卡裡面的則是RFID規格則是採用NXP公司的MIFARE Classic。

## MIFARE的安全性

MIFARE是恩智浦半導體公司（NXP Semiconductors）擁有的一系列RFID技術。其成本低廉，讓他在目前市面上廣泛應用於各種系統，ex：門禁系統、圖書館借書證、識別卡...等等。

然而，MIFARE 的安全性備受質疑。早在 2007 年，就有駭客破解了 MIFARE 晶片的演算法，並且有相關論文探討。

> 2007年12月，在騷亂交流大會上Henryk Plötz和Karsten Nohl[6]發表了部分用於MIFARE晶片演算法上的逆向工程技術[7]。
> <br><cite>維基百科：MIFARE</cite>

而台灣的紀錄著名的則有：

>2010年7月，臺灣大學電機系教授鄭振牟團隊使用改進過的監聽封包（Sniffer-Based）的攻擊手法攻擊Mifare卡。將1張正常使用中的悠遊卡，將餘額從正100多元，更改成為負五百多元[12]。
> <br><cite>維基百科：MIFARE</cite>

在2021 SITCON 學生計算機年會，也有講者於「[RFID 硬體資安實戰](https://hackmd.io/YtbBU59oSoKJuiSCQss4eQ?view)」議程中分享MIFARE卡的資安問題。由此也可以看出其安全問題早已存在很久了。

## 悠遊卡公司的應對方式

遊遊卡公司面對這樣的資安問題，也只有透過補漏動的方式監督使用者。主要的作法為：

- 用法律方式來嚇阻
- 搭配後台的資料庫核對不正當的竄改資料。

## 改善方法

相較於於悠遊卡的MIFARE Classic技術，日本SUICA所使用的Felica技術具有更高的安全性，Apple也早已將SUICA整合進Apple Pay中。

此外，Apple也早已接納同是MIFARE家族，但安全性更高的MIFARE DESFire規格。

## 參考資料

- [一卡在手便利無窮，悠遊卡的設計原理——《我們的生活比你想的還物理》](https://pansci.asia/archives/359263)
- [悠遊卡遭駭，Mifare卡安全性遭質疑](https://www.ithome.com.tw/news/69970)
- [FeliCa、Mifareの違いを解説！ICカードの種類と特長を比較する](https://canon.jp/business/solution/pro-printer/idprinter/useful/iccardcategory)
- [Apple Pay為什麼不支援悠遊卡原因完全揭秘，金管會給出獨家答案](https://mrmad.com.tw/iphone-support-easycard-ipass)
- [Apple's Core NFC Framework](https://developer.apple.com/documentation/corenfc)
- [維基百科：悠遊卡](https://zh.wikipedia.org/zh-tw/%E6%82%A0%E9%81%8A%E5%8D%A1)
- [維基百科：MIFARE](https://zh.wikipedia.org/wiki/MIFARE)
