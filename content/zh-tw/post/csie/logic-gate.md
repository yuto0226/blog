---
title: 二進位制 & 邏輯閘實作
categories:
  - [計算機科學]
tags:
  - 筆記
date: 2021-06-16 17:26:48
cover: https://i.imgur.com/6cbLa4f.png
top_img: https://i.imgur.com/6cbLa4f.png
comments: true
---
# 前言
我們都知道在 C++ 裡面
如過要實現加法的話可以寫成
```cpp
int a=1;
int b=2;

a+b;
```
答案理所當然會是 3
雖然我們是用 C++ 去編寫的
但是電腦執行的卻是編譯過的機械碼
繞我不禁好奇，電腦是如何進行加法的 ?
不是透過寫程式碼讓他編譯，而是最原始的方法
單純的電子訊號，也就是 0 和 1

# 二進位制
`5+5` ，只要有好好學過數學的人都應該會知道答案是 10
這種進位制即是大家最熟悉的 `10 進位制` ，也就是當數字加到 10 時要進一位
`2 進位制` 也是一樣的概念，當數字加到 2 時要進一位
舉例來說 `1+1` 的答案就會是 10

`2 進位制` 廣泛被運用在電腦上面，而一個數字也被稱作位元

# 邏輯閘
邏輯閘是在積體電路上的基本組件。這些電晶體的組合可以使代表兩種訊號的高低電平在通過它們之後產生高電平或者低電平的訊號。高、低電平可以分別代表邏輯上的「真」與「假」或二進位當中的1和0，從而實現邏輯運算。常見的邏輯閘包括與閘，或閘，非閘，互斥或閘（也稱：互斥或）等等。([維基百科][邏輯閘])

[邏輯閘]: https://zh.wikipedia.org/wiki/%E9%82%8F%E8%BC%AF%E9%96%98

## AND
| \ | 1 | 0 |
| - | - | - |
| 1 | 1 | 0 |
| 0 | 0 | 0 |

## OR
| \ | 1 | 0 |
| - | - | - |
| 1 | 1 | 1 |
| 0 | 1 | 0 |
## XOR
| \ | 1 | 0 |
| - | - | - |
| 1 | 0 | 1 |
| 0 | 1 | 0 |

# 實作
這次的實作是參考 [Ben Eater][BenEater] 的 [Learn how computers add numbers and build a 4 bit adder circuit][Learn how computers add numbers and build a 4 bit adder circuit]

[BenEater]: https://www.youtube.com/channel/UCS0N5baNlQWJCUrhCEo8WlA
[Learn how computers add numbers and build a 4 bit adder circuit]: https://www.youtube.com/watch?v=wvJc9CZcvBc

影片透過觀察 `2進位制` 加法 的規律，歸納出了以下電路圖

![](https://i.imgur.com/6cbLa4f.png)

知道要怎麼接之後就簡單了
剩下的就只是把它實做出來而已
成品長這樣

![](https://i.imgur.com/caBdKaA.jpg)

01001 + 01100 的結果為 10101
和實際操作的結果一樣

![](https://i.imgur.com/SK9QZdl.jpg)
