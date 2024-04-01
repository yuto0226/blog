---
title: 向量 Vector(STL)
date: 2022-01-05 20:24:37
cover: https://i.imgur.com/LV9jk0s.png
top_img: https://i.imgur.com/LV9jk0s.png
categories:
    - [計算機科學,C++,STL]
tags:
    - vector
    - C++
    - 筆記
---
# 前言
在學寫C++的過程當中，從 Array 到 Vector 一直是很難跨越的障礙，
因為我的物件導向和指標不是學的很完善，導致會有點看不懂程式碼在做什麼，
所以這次我透過邊實作邊學習的方式來盡量彌補我知識上的不足，
順便做個筆記來記錄。

# 簡介
Vector 是 C++ 標準程式庫中的一個 class，可視為會自動擴展容量的陣列，
是C++標準程式庫中的眾多容器(container)之一，以循序(Sequential)的方式維護變數集合，
使用前預先 `#include <vector>` 即可。

## 特色
+ 支援隨機存取
+ 集合尾端增刪元素很快 : 常數時間 O(1)
+ 集合中間增刪元素比較費時 : 線性時間 O(n)
+ 以模板(泛型)方式實現，可以儲存任意類型的變數，包括使用者自定義的資料型態。

# 成員函式
vector 類別是以容器(Container)模式為基準設計的，也就是說，基本上它有 `begin()`、`end()`、`size()`、`max_size()`、`empty()` 以及 `swap()` 這幾個方法。
## 存取元素的方法
+ `v[i]` : 存取索引值為 i 的元素值 (索引值從零起算，故第一個元素是v[0]。)
+ `v.at(i)` : 存取索引值為 i 的元素的值
+ `v.front()` : 回傳 vector 第一個元素的值
+ `v.back()` : 回傳 vector 最尾端元素的值

>用 operator `[]` 可能會 **Segmentation Fault**。以 `at()` 存取會做**陣列邊界檢查**，如果存取越界將會拋出一個**例外**，這是與 operator `[]` 的唯一差異。撰寫較嚴肅、安全性較高的程式時使用 `at()`。

## 新增或移除元素的方法
+ `v.push_back()` - 新增元素至 vector 的尾端，必要時會進行記憶體配置。
+ `v.pop_back()` - 刪除 vector 最尾端的元素。
+ `v.insert()` - 插入一個或多個元素至 vector 內的任意位置。
+ `v.erase()` - 刪除 vector 中一個或多個元素。
+ `v.clear()` - 清空所有元素。

>少依賴 `push_back()` 的自動記憶體配置，不是不要用 `push_back()`，是不要讓 `push_back()` 自己判定記憶體需求，能自己要記憶體的就自己要，善用 `reserve()`、`resize()` 或建構子(constructor)引數。

## 取得長度/容量
`v.size()` - 取得 vector 目前持有的元素個數。
`v.empty()` - 如果 vector 內部為空，則傳回 true 值。
`v.capacity()` - 取得 vector 目前可容納的最大元素個數。這個方法與記憶體的組態有關，它通常只會增加，不會因為元素被刪減而隨之減少。

## 重新組態/重設長度
`v.reserve()` - 擴大 vector 的容量大小(組態更多的記憶體)。
`v.resize()` - 改變 vector 目前持有的元素個數。

>+ `reserve()` 的目的是**擴大容量**。
>做完時，vector 的長度不變，capacity 只會長大不會縮小，資料所在位置可能會移動 (因為會重配空間)。因為 vector 一開始是空的，立刻預留顯然比填了資料後才預留省了拷貝資料的時間。
>+ `resize()` 的目的是**改變 vector 的長度**。
>做完時，vector 的長度會改變為指定的大小，capacity 則視需要調整，確保不小於 size，資料所在位置可能會移動。如果變小就擦掉尾巴的資料，如果變大就補零。補零如果會超過容量，會做重配空間的動作。

## 迭代 (Iterator)
`v.begin()` - 回傳一個 Iterator，它指向 vector 第一個元素。
`v.end()` - 回傳一個 Iterator，它指向 vector 最尾端元素的下一個位置(非最末元素)。
`v.rbegin()` - 回傳一個反向 Iterator，它指向 vector 最尾端元素的。
`v.rend()` - 回傳一個 Iterator，它指向 vector 的第一個元素的前一個位置。

![](https://i.imgur.com/LV9jk0s.png)

# 使用 vector 實做
在實際使用 vector 之前，我們必須先了解如何宣告 vector 變數。
## 初始化
以下即是宣告一個 `int` 型的 vector，`size()` 是 0,  `capacity()` 也是 0。
```cpp
#include <vector>
using std::vector;

int main() {
    vector<int> v;
    return 0;
}
```

>使用萬用標頭檔(`<bits/stdc++.h>`)就可以不用再 `#include <vector>`。

在初始化時可以用用 operator `=` 就把值丟進去，
```cpp
vector<int> v={1, 2, 3, 4};
```
或是使用建構子，
```cpp
vector<int> v({1, 2, 3, 4});
```

若要從其他容器中把值複製過來可以用 operator `=`，
```cpp
vector<int> v1={1, 2, 3, 4};
vector<int> v2=v1;
```
同樣地也可以用建構子，
```cpp
vector<int> v1={1, 2, 3, 4};
vector<int> v2(v1);
```
還可以從 array 裡複製過來，
```cpp
int n[3]={1, 2, 3, 4};
vector<int> v(n, n+3);
```

範圍複製也是可以的，vector 的可以這樣寫，
```cpp
vector<int> v1 = {1, 2, 3, 4, 5};
vector<int> v2(v1.begin()+2, v1.end()-1); // {3, 4}

```
array 的可以這樣寫，
```cpp
int n[5] = {1, 2, 3, 4, 5};
vector<int> v(n+2, n+4); // {3, 4}

```

## 存取元素的方法
```cpp
vector<int> v={1, 2, 3, 4};
cout<<v[1]<<endl;   // 2
cout<<v.at(2)<<endl;   // 3
cout<<v.front()<<endl;   // 1
cout<<v.back()<<endl;   // 4
```

## 新增或移除元素的方法
```cpp
vector<int> v={1, 2, 3, 4};
v.push_back(5); // {1, 2, 3, 4, 5}
v.pop_back();   // {1, 2, 3, 4}
v.insert(2,5);  // {1, 2, 5, 3, 4}
v.erase(2);     // {1, 2, 3, 4}
v.clear();      // 此時所有元素被清空，但 capacity 為 5
```
### 用 swap() 刪除元素
成員函式 swap()，這個函式用來交換兩個 vector 容器中的元素。
因此可以與一個具有相同資料類型的內容為空的局部變數swap，從而實現徹底刪除元素、釋放容量的目的。
```cpp
vector<int> v1={1, 2, 3, 4};
vector<int> v2;
v1.swap(v2);    // v1 內的元素與 v2 交換，即 v1 內所有元素被刪除
```

## 長度/容量以及配置大小
```cpp
vector<int> v={1, 2, 3, 4};
v.reserve(10);  // 把 capacity 擴大為 10
cout<<v.size()<<endl;   // 4
cout<<v.capacity()<<endl;   // 10
cout<<v.empty()<<endl;  // 0
v.clear();
cout<<v.empty()<<endl;  // 1
v.resize(2);    // {1, 2, 3, 4, 0, 0}
```

## 尋訪元素
尋訪元素除了像陣列那樣寫以外，還可以用疊代器寫
```cpp
vector<int> v={1, 2, 3, 4, 5};

for(int i=0; i<v.size(); i++) cout << v[i] << " ";
cout<<endl;
for(int i=0; i<v.size(); i++) cout << v.at(i) << " ";
cout<<endl;

vector<int>::iterator it;
for(it=v.begin(); it!=v.end(); ++it) cout << *it << " ";
cout<<endl;
```

## vector::assign()
`vector::assign()` 是 C++ 中的 STL，它通過替換舊元素為向量元素分配新值。如果需要，它也可以修改向量的大小。
### 分配常量值
```cpp
vector<int> v;
v.assign(5, 10);   // {10, 10, 10, 10 ,10}
```
### 從 array 或 vector 分配值
除了上面有提過用 operator `=` 或建構子的方式在初始化時賦值，
也可以透過 `assign()` 來執行。
```cpp
int a[5]={1, 2, 3, 4, 5};
vector<int> v1;
vector<int> v2;

v1.assign(a,a+4);   // {1, 2, 3, 4}
v2.assign(v1.begin(),v1.begin()+2); // {1, 2}
```

### 修改 vector
```cpp
vector<int> v;
v.assign(5, 10);    // {10, 10, 10, 10 ,10}
v.assign(v.begin(), v.begin() + 3); // {10, 10, 10}
```


# Reference
+ [Mr. Opengate: C/C++ - Vector (STL) 用法與心得完全攻略](https://mropengate.blogspot.com/2015/07/cc-vector-stl.html)
+ [ShengYu Talk: C++ std::vector 用法與範例](https://shengyu7697.github.io/std-vector/)
+ [Wiki 維基百科: Vector (STL)](https://zh.wikipedia.org/wiki/Vector_(STL))
+ [純淨天空: C++ vector::assign()用法及代碼示例](https://vimsky.com/zh-tw/examples/usage/vector-assign-in-c-stl.html)
