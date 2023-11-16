---
title: '[C++]鏈接串列 Linked List'
date: 2022-01-01 21:00:11
cover: https://i.imgur.com/qkADZ5a.png
top_img: https://i.imgur.com/qkADZ5a.png
categories:
    - [計算機科學,資料結構 & 演算法]
tags:
    - 筆記
    - C++
    - Linked List
    - 資料結構
---
# 簡介
何謂**鏈接串列(Linked List)**?串列是一種常見的資料結構，
使用節點儲存資料，且透過接點的指標指向下一個節點，
形成一串記憶體位置不相連的資料串。

![](https://i.imgur.com/qkADZ5a.png)

# Linked List vs Array
### Array
**Pros**
+ random access：只要利用**index**即可在`O(1)`時間對**Array**的資料做存取。
+ 較Linked list為節省記憶體空間：因為**Linked list**需要多一個**pointer**來記錄下一個節點的記憶體位置。

**Cons**
+ 新增/刪除資料很麻煩：若要在第一個位置新增資料，就需要`O(N)`時間把矩陣中所有元素往後移動。同理，若要刪除第一個位置的資料，也需要`O(N)`時間把矩陣中剩餘的元素往前移動。
+ 若資料數量時常在改變，要時常調整矩陣的大小，會花費`O(N)`的時間在搬動資料(把資料從舊的矩陣移動到新的矩陣)。

**適用時機**
+ 希望能夠快速存取資料。
+ 已知欲處理的資料數量，便能確認矩陣的大小。
+ 要求記憶體空間的使用越少越好。

### Linked List
**Pros**
+ 新增/刪除資料較**Array**簡單，只要對`O(1)`個節點調整**pointer**即可，不需要如同**Array**般搬動其餘元素。
+ Linked list的資料數量可以是動態的，不像**Array**會有resize的問題。

**Cons**
+ 因為**Linked list**沒有**index**，若要找到特定節點，需要從頭(Node *first)開始找起，搜尋的時間複雜度為`O(N)`。
+ 需要額外的記憶體空間來儲存**pointer**。

**適用時機**
+ 無法預期資料數量時，使用**Linked list**就沒有resize的問題。
+ 需要頻繁地新增/刪除資料時。
+ 不需要快速查詢資料。

# 用 class 實作
```cpp
#include <bits/stdc++.h>
using std::cout;
using std::endl;

class Linkedlist;

class Node{
    private:
        int data;
        Node *next;
    public:
        Node():data(0),next(0){};
        Node(int x):data(x),next(0){};

        friend class LinkedList;
};

class LinkedList{
    private:
        Node *first;
    public:
        LinkedList():first(0){};
        void printlist();
        void push_front(int x);
        void push_back(int x);
        void erase(int x);
        void clear();
        void reverse();
};
void LinkedList::printlist(){
    if(first==0){
        cout<<"List is empty.\n";
        return;
    }
    Node *current=first;
    while(current!=0){
        cout<<current->data<<" ";
        current=current->next;
    }
    cout<<endl;
}
void LinkedList::push_front(int x){
    Node *newNode=new Node(x);
    newNode->next=first;
    first=newNode;
}
void LinkedList::push_back(int x){
    Node *newNode=new Node(x);
    if(first==0){
        first=newNode;
        return;
    }

    Node *current=first;
    while(current->next!=0){
        current=current->next;
    }
    current->next=newNode;
}
void LinkedList::erase(int x){
    Node *current=first;
    Node *previous=0;

    while(current!=0&&current->data!=x){
        previous=current;
        current=current->next;
    }

    if(current==0){
        cout<<"There's no "<<x<<" in list.\n";
        return;
    }else if(current=first){
        first=current->next;
        delete current;
        current=0;
        return;
    }else{
        previous->next=current->next;
        delete current;
        current=0;
        return;
    }
}
void LinkedList::clear(){
    Node *current=first;
    first=first->next;
    delete current;
    current=0;   
}
void LinkedList::reverse(){
    if(first==0||first->next==0) return;

    Node *previous=0,
         *current=first,
         *preceding=first->next;

    while(preceding!=0){
        current->next=previous;
        previous=current;
        current=preceding;
        preceding=preceding->next;
    }

    current->next=previous;
    first=current;
}

int main(){
    LinkedList list;
    list.push_front(1);
    list.push_front(2);

    list.printlist();
    return 0;
}

```

# Reference

http://alrightchiu.github.io/SecondRound/linked-list-introjian-jie.html
