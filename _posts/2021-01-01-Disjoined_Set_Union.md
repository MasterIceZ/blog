---
title: Disjoined Set Union
tags:
  - Cplusplus
  - Programming
  - Algorithm
date: 2021-01-01 17:00:00 +0700
---

Disjoined Set Union(DSU) เป็น Algorithm ที่เกี่ยวกับการดำเนินการของเซต(การ Union)
ใน DSU มีฟังก์ชันที่สำคัญคือ find_root
find_root source (C++) :
```cpp
int find_root(int u){
    if(parent[u]==u){
        return u;
    }
    parent[u] = find_root(parent[u]);
    return parent[u];
}
```

```txt
Example Tree[#1] : 
    [2]
    / \
  [1] [6]
  / \   \
 [3][4] [5]
```
2  เป็น root ของ Tree นั้
```txt
Example Tree[#2] :
   [8]
  /   \
[2]   [7]
```
สามารถรวม Tree[#1] กับ Tree[#2] ได้เป็น
```txt
Joined Tree :
     [8]
     / \
   [2] [7]
   / \
  [1] [6]
  / \   \
[3] [4] [5]
```
เปรียบได้กับ Tree เป็น Set
Tree[#1] = {1,2,3,4,5,6}
Tree[#2]={2,8,7}
Joined Tree คือ Set ที่ Union กัน
Joined Tree = {1,2,3,4,5,6,7,8}

Source Code(C++) :
```cpp
#include<iostream>
using namespace std;

const int MxN = 10010;
int parent[MxN];

int find_root(int u){
    if(parent[u]==u){
        return u;
    }
    parent[u] = find_root(parent[u]);
    return parent[u];
}

int32_t main(){
    ios::sync_with_stdio(0);
    cin.tie(0);
    for(int i=0;i<MxN;++i){
        parent[i] = i;
    }
    int n;cin >> n;
    for(int i=0;i<n;++i){
        int u,v;
        cin >> u >> v;
        parent[find_root(u)] = find_root(v);
    }
    int q;
    cin >> q;
    while(q--){
        int u,v;
        cin >> u >> v;
        if(find_root(u)==find_root(v)){
            cout << "Same Set";
        }
        else{
            cout << "Diffrent Set";
        }
        cout << endl;
    }
    return 0;
}
```
ตัวอย่างโจทย์ที่เกี่ยวกับ DSU :<br>
[General](https://beta.programming.in.th/tasks/1092)<br>
[Book Exchange](https://codeforces.com/contest/1249/problem/B2)