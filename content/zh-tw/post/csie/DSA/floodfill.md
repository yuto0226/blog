---
title: '[C++]泛洪演算法 Flood Fill Alogrithm'
slug: floodfill
date: 2022-02-05 14:29:02
image: https://i.imgur.com/gZKSRXT.png
categories:
  - 計算機科學
  - 資料結構 & 演算法
tags:
  - 筆記
  - C++
---
# 簡介
Flood Fill 演算法是從一個區域中提取若干個連通的點與其他相鄰區域區分開(或分別染成不同顏色)的經典演算法(Algorithm)。因為其思路類似洪水從一個區域擴散到所有能到達的區域而得名。

# 實作方法
+ 深度優先搜尋(Depth-First Search,DFS)
+ 廣度優先搜尋(Breadth-First Search,BFS)

## BFS 實作
把最外面的點加入佇列(Queue)裡面，分別按照佇列中的點染色

![](https://i.imgur.com/2C9pVdq.gif)
```cpp
//  title: flood fill algorithm
//   date: 2/1
// author: 羅崧瑋
#include<bits/stdc++.h>
#include<unistd.h>  // terminal color font
using namespace std;

// matrix size
#define row 10
#define col 10

// 上,下,左,右
int nx[4]={0,1,0,-1};
int ny[4]={1,0,-1,0};
// pair type
typedef struct pair{
    int x;
    int y;
}pair_t;

void printa(int a[row][col]);

// (i,j) 起始位置
void floodfill(int a[row][col],int i,int j,int newc){
    // 染色佇列
    queue<pair_t> pos;
    pos.push({i,j});
    // 染色
    while(!pos.empty()){
        auto f=pos.front();
        i=f.x;
        j=f.y;
        pos.pop();
        // 邊界檢查 & 同色檢查
        if(a[i][j]<0 || a[i][j]==newc) continue;
        a[i][j]=newc;
        printa(a);
        for(int b=0;b<4;b++)
            pos.push({i+nx[b],j+ny[b]});
    }
}

void printa(int a[row][col]){
    system("clear");
    for(int i=0;i<row;i++){
        for(int j=0;j<col;j++){
            if(a[i][j]<0)
                cout<<"\033[37;7m"<<setw(3)<<a[i][j]<<"\033[0m";
            else if(a[i][j]==5)
                cout<<"\033[34;7m"<<setw(3)<<a[i][j]<<"\033[0m";
            else
                cout<<setw(3)<<a[i][j];
        }
        cout<<"\n";
    }
    cout<<"\n";
    usleep(200000);
}

int main() {
    // matrix
    int a[row][col]={{-1,-1,-1,-1,-1,-1,-1,-1,-1,-1},
                     {-1, 0, 0, 0, 0, 0,-1, 0, 0,-1},
                     {-1, 0, 0, 0, 0, 0,-1, 0, 0,-1},
                     {-1, 0, 0,-1, 0, 0, 0,-1,-1,-1},
                     {-1, 0, 0,-1, 0, 0,-1, 0, 0,-1},
                     {-1, 0, 0,-1, 0, 0,-1, 0, 0,-1},
                     {-1, 0,-1,-1, 0,-1, 0, 0, 0,-1},
                     {-1, 0, 0, 0, 0, 0, 0, 0, 0,-1},
                     {-1, 0, 0, 0, 0, 0, 0, 0, 0,-1},
                     {-1,-1,-1,-1,-1,-1,-1,-1,-1,-1}};
    floodfill(a,1,1,5);
    cout<<"final :\n";
    printa(a);

    return 0;
}

```

# Reference
+ [資訊之芽: Flood Fill Algorithm](https://www.csie.ntu.edu.tw/~sprout/algo2017/ppt_pdf/flood_fill.pdf)
+ [Inside code: Flood fill algorithm](https://www.youtube.com/watch?v=VuiXOc81UDM)
+ [Wiki: Flood Fill](https://zh.wikipedia.org/wiki/Flood_fill)
+ [hn_tzy: Linux C/C++ 如何輸出彩色字體](https://www.twblogs.net/a/5d072587bd9eee1ede03920a)
