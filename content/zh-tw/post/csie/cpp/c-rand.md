---
title: 'C語言rand()函式的用法'
date: 2022-11-21 23:09:10
cover:
top_img:
categories:
    - [計算機科學]
tags:
    - C
---
# stdlib.h
## rand()
```c
int rand(void);
```
產生介於0~RAND_MAX(=32767)之間的隨機亂數，需要透過srand()來初始化
## srand()
```c
void srand(unsigned int seed);
```
透過傳進來的seed初始化rand()，seed若不改變則每次所產生的亂數皆會相同。

# time.h
## time()
```c
time_t time(time_t* timer);
```
`time(NULL)`會回傳自1970年午夜到現在所經過的秒數，可以用作`srand`的seed，每次執行的seed皆會不一樣

# rand() scaled and shifted
```c
int scale_rand(int start,int end) return start+rand()%end;
```