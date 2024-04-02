---
title: '[C++]線段樹'
slug: segment-tree
date: 2022-11-13 20:21:16
image:
categories:
    - 計算機科學
    - 資料結構 & 演算法
tags:
  - 筆記
  - C++
  - 資料結構
---

# 程式碼
```cpp
#include <bits/stdc++.h>
using namespace std;

class Node{
public:
    int start;
    int end;
    int max;
    int min;
    int sum;
    Node *left=nullptr;
    Node *right=nullptr;
    Node(int start,int end,int max,int min,int sum,Node *left=nullptr,Node *right=nullptr):
    start(start),end(end),max(max),min(min),sum(sum),left(left),right(right){}
};

Node *build(int start,int end,int val[]){
    if(start==end){
        //cout<<"build: ["<<start<<", "<<end<<"] node->,max,min,sum="<<val[start]<<"\n";
        return new Node(start,end,val[start],val[start],val[start],nullptr,nullptr);
    }
    int mid=(start+end)/2;
    Node *left=build(start,mid,val);
    Node *right=build(mid+1,end,val);
    //cout<<"build: ["<<start<<", "<<end<<"]"<<" node->max="<<max(left->max,right->max)<<" node->min="<<min(left->min,right->min)<<" node->sum="<<left->sum+right->sum<<"\n";
    return new Node(start,end,max(left->max,right->max),min(left->min,right->min),left->sum+right->sum,left,right);
}

int query_sum(Node *root,int i,int j){
    int sum=0;
    //cout<<"query: ["<<i<<", "<<j<<"] @ ["<<root->start<<", "<<root->end<<"] root->sum="<<root->sum<<"\n";
    if(root->start==root->end) return root->sum;
    if(root->start==i&&root->end==j) return root->sum;
    int mid=root->start+(root->end-root->start)/2;
    if(j<=mid) return query_sum(root->left,i,j);
    else if(i>mid) return query_sum(root->right,i,j);
    else return query_sum(root->left,i,mid)+query_sum(root->right,mid+1,j);
}

int query_max(Node *root,int i,int j){
    int sum=0;
    //cout<<"query: ["<<i<<", "<<j<<"] @ ["<<root->start<<", "<<root->end<<"] root->max="<<root->max<<"\n";
    if(root->start==root->end) return root->max;
    if(root->start==i&&root->end==j) return root->max;
    int mid=root->start+(root->end-root->start)/2;
    if(j<=mid) return query_max(root->left,i,j);
    else if(i>mid) return query_max(root->right,i,j);
    else return max(query_max(root->left,i,mid),query_max(root->right,mid+1,j));
}

int query_min(Node *root,int i,int j){
    int sum=0;
    //cout<<"query: ["<<i<<", "<<j<<"] @ ["<<root->start<<", "<<root->end<<"] root->min="<<root->min<<"\n";
    if(root->start==root->end) return root->min;
    if(root->start==i&&root->end==j) return root->min;
    int mid=root->start+(root->end-root->start)/2;
    if(j<=mid) return query_min(root->left,i,j);
    else if(i>mid) return query_min(root->right,i,j);
    else return min(query_min(root->left,i,mid),query_min(root->right,mid+1,j));
}
```
