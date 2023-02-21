---
title: 数据结构（四）：树链剖分 (updating)
author: Conless
date: 2023-01-27 14:03:43
categories:
- [Computer Science]
---

## 学习计划

|     事项     |                        详情                        | 时间  |
| :----------: | :------------------------------------------------: | :---: |
| 重温基本概念 |                 参考课本与 OI-wiki                 |  1h   |
| 基础题目练习 | 复习 P2590,P2146,P3178，完成 P4427,ACMOJ1473 |  2.5h   |
| 概念细节与拓展 | 课本，OI-wiki，完成或学习 P1505 / P3979 | 2.5h |

## 思想

将一棵树划分为若干条链，转化为线性结构，从而用其它数据结构维护相关信息。

重链剖分可以将树上的任意一条路径划分成不超过 $O(\log n)$ 条连续的链，每条链上的点深度互不相同（即是自底向上的一条链，链上所有点的 LCA 为链的一个端点）。

重链剖分还能保证划分出的每条链上的节点 DFS 序连续，因此可以方便地用一些维护序列的数据结构（如线段树）来维护树上路径的信息。

## 重链剖分

重链剖分是最常用的树链剖分方式：

定义 重子节点 表示其子节点中子树最大的子节点。如果有多个子树最大的子节点，取其一。如果没有子节点，就无重子节点。

定义 轻子节点 表示剩余的所有子节点。

从这个节点到重子节点的边为 重边。

到其他轻子节点的边为 轻边。

若干条首尾衔接的重边构成 重链。

把落单的节点也当作重链，那么整棵树就被剖分成若干条重链。

## 实现

运用到的数据结构为支持 单点/区间 修改/查询 的线段树，记作

```cpp
sjtu::SegmentTree<int, MAXN> stree;
```

首先进行两遍 dfs 建树
```cpp
void dfs(int u, int last) {
    int maxsiz = 0;
    siz[u] = 1;
    fa[u] = last;
    for (int i = head[u]; i; i = edge[i].next) {
        int v = edge[i].v;
        if (v == last)
            continue;
        h[v] = h[u] + 1;
        dfs(v, u);
        siz[u] += siz[v];
        if (siz[v] > maxsiz) {
            maxsiz = siz[v];
            mson[u] = v;
        }
    }
}

void build(int u, int last, int top) {
    key[u] = ++ti;
    tp[u] = top;
    data[ti] = w[u];
    if (mson[u])
        build(mson[u], u, top);
    for (int i = head[u]; i; i = edge[i].next) {
        int v = edge[i].v;
        if (v == last || v == mson[u])
            continue;
        build(v, u, v);
    }
    las[u] = ti;
}
```
