---
title: '[C++]BIT 樹狀樹組'
slug: bitree
categories:
  - 計算機科學
  - 資料結構 & 演算法
tags:
  - 筆記
  - C++
  - 資料結構
date: 2022-04-01 11:52:00
image: https://i.imgur.com/ISJQZSj.png
comments:
---
# BIT
>A Fenwick tree or binary indexed tree is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers.
>-wiki

樹狀數組也稱作 Fenwick Tree 或 Binary Indexed Tree(BIT)，用來儲存資料，且可以快速求出前綴和或區間加總。對於一個長度 n 的陣列，可以在 O(n) 的時間初始化，在 O(n) 時間詢問一個前綴的訊息例如前綴和，以及在 O(n) 的時間修改其中一個值。但是 BIT 的缺點就是有些問題無法轉為前綴間的運算，無法個別操作元素。

![bit](https://i.imgur.com/d611u7b.png)

由上面這張圖可了解 BIT 儲存的區間。`Index[]` 為儲存資料的陣列，`BIT[]` 為實際上儲存的區間。

通常一個數狀數組會有 3 個函式:
- `uptade(idx,delta)`: 將 delta 加到 idx 的節點上
- `query(index)`: 查詢從第一個位置到 idx 的所有節點的加總
- `range_query(idx_this,idx_that)`: 查詢從 idx_this 到 idx_that 間所有節點的總和

## lowbit()
lowbit 是為了求一個二進位數中最低位1的值(最靠近右邊的 1 的值)，構成 BIT 的核心
```cpp
int lowbit(int x) {return x&(-x);}
```
在程式碼中 -x 會是 x 的補數加 1 ，把 x 和 -x 做 and 運算，得到的數即是 x 的 lowbit。以 `lowbit(4)` 為例，4 的二進位置表示是 4(2)=0100，其補數為 ~4(2)=1011，我們便可以求出 -x=1011+1=1100，再把 0100 和 1100 進行 and 運算即可求出其 `lowbit(4)`=0100。

![](https://i.imgur.com/i2tNBPO.png)

## Update Tree
![](https://i.imgur.com/ISJQZSj.png)

在 Update Tree 中可以看出如何將值加到節點上。當更新一個節點時，會沿著節點間的邊(edge)向上把每個父節點(parent)都加上同樣的值。例如在一號節點上加上 5，那麼節點 2、4、8 也都會加上 5。

- 節點 i 的父節點是 i-lowbit(i)

## Query Tree
![](https://i.imgur.com/USjovHL.png)
在 Query Tree 中可以看出怎麼求出該索引的前綴。查詢某索引的前綴時，回傳的值會是該索引對應節點的值沿著邊把所有祖先(ancestor)的值相加。例如要求索引 7 的前綴，回傳的值會是節點 4、6、7 的相加。

- 節點 i 的父節點是 i+lowbit(i)

# 程式碼
```cpp
#include <bits/stdc++.h>
#define bit_capacity 100001

class bit{
    public:
        int length;
        // 更新元素值
        void update(int i,int delta);
        // 前綴和
        int query(int i);
        // 區間查詢
        int query(int f,int l);
        // 實際儲存的陣列
        int *bitree=index;
    private:
        int lowbit(int x) {return x&(-x);}
        int index[bit_capacity];
};

void bit::update(int i,int delta){
    while(i<=length){
        index[i]+=delta;
        i+=lowbit(i);
    }
}

int bit::query(int i){
    int sum =0;
    while(i>0){
        sum+=index[i];
        i-=lowbit(i);
    }
    return sum;
}
int bit::query(int f,int l){
    return query(l)-query(f);
}

int main(){
    bit tree;
    tree.length=10;
    for(int i=1;i<=10;i++) tree.update(i,i);
    for(int i=1;i<=10;i++){
        std::cout<<"BIT["<<i<<"]="<<tree.bitree[i]<<std::endl;
   }
    return 0;
}
```
