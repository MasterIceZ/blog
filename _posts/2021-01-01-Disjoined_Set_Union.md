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