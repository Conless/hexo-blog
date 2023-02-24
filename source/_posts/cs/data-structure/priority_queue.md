---
title: 数据结构（三）：堆与 STL priority_queue
date: 2023/02/21 11:32:00
categories:
- [Computer Science, Data Structure (CS1951@SJTU)]
---
# 堆
## 简介
相较于平衡树等，堆是一种约束较为自由的数据结构，只需要满足父节点的键值大于/小于子节点即可。
## 二叉堆
下面讲解以二叉堆方式实现的大根堆，它是一棵完全二叉树，其保持平衡的基本方式是向上调整（子节点与父节点交换）与向下调整。
### 插入
在插入时，将新的节点插入到完全二叉树的最后一个位置，然后不断向上调整；
### 删除
在删除根节点时，将其与最后一个节点交换，将其删除，然后将新的根节点不断向下调整。
### 建树
假设直接按照顺序构建出一棵完全二叉树，然后对其调整使得满足堆的性质，有两种方案：
1. 从根开始，不断向上调整，这样在越深处越多节点，走的距离期望越长，总的复杂度期望为 $O(n\log n)$。
2. 从叶子节点开始，不断向下调整，这样在越深处越多节点，但走的距离期望短，总的复杂度期望为 $O(n)$。
   
因此，采取第二种方案更加合理。
### 应用
对顶堆：一个小根堆与一个大根堆结合，共同维护序列的第 $k$ 大数。

## 左偏树
左偏树是一种可并堆。它是一棵具有“左偏”性质的二叉树。
### 左偏性
dist：一个节点到子节点中外节点的最短距离，其中外节点指没有左儿子或没有右儿子的节点。
左偏性：若一棵二叉树中任意节点左儿子的 dist 大于右儿子的 dist，称其具有左偏性。
### 合并
合并操作是一个左偏树的核心操作，他同时完成了合并两组数据与维持树的高度两个操作。其核心思想是，尽可能地往右子树里面添加东西，如果发现添加出了问题，就将左右子树交换。递归地讲：
1. 对于两个左偏树，去值较小的根作为树根
2. 将另一棵树与右子树合并
3. 检查是否需要交换左右子树

### 其他操作
1. 插入：树与节点的合并
2. 删除：合并根的左右儿子
### 拓展操作
1. 删除任意节点：将左右儿子合并，向上更新 dist 直到无需更新
2. 整个堆进行算术操作：在根上打标记，删除/合并的时候 pushdown 即可

### 实现
```cpp
node *merge(node *x, node *y) {
    if (x == nullptr || y == nullptr) {
        if (x == nullptr)
            x = y;
        else
            y = x;
        return x;
    }
    if (x->data > y->data)
        swap(x, y);
    x->rson = merge(x->rson, y);
    x->rson->rt = x->rt;
    if (x->lson == nullptr || x->lson->dis < x->rson->dis)
        swap(x->lson, x->rson);
    x->dis = (x->rson != nullptr) ? x->rson->dis + 1 : 0;
    return x;
}

void erase(node *x) {
    x->rt = merge(x->lson, x->rson);
    if (x->lson)
        x->lson->rt = x->rt;
    if (x->rson)
        x->rson->rt = x->rt;
    x->dis = -1;
}
```

# STL priority_queue


对上面的两个操作进行简单包装即可，需要注意的是，STL 容器需要具备复制与析构等功能。首先是节点的实现与相关操作：
```cpp
struct tnode {
    T data;
    int dis;
    tnode *lson, *rson;
    tnode(const T &_data, int _dis = 0) : data(_data), dis(_dis), lson(nullptr), rson(nullptr) {}
} * rt;

tnode *tnode_copy(tnode *org) {
    tnode *tmp = new tnode(org->data, org->dis);
    if (org->lson)
        tmp->lson = tnode_copy(org->lson);
    if (org->rson)
        tmp->rson = tnode_copy(org->rson);
    return tmp;
}
void tnode_clean(tnode *org) {
    if (org == nullptr)
        return;
    if (org->lson) {
        tnode_clean(org->lson);
        org->lson = nullptr;
    }
    if (org->rson) {
        tnode_clean(org->rson);
        org->rson = nullptr;
    }
    delete org;
}
tnode *tnode_merge(tnode *nd1, tnode *nd2) {
    if (nd1 == nullptr)
        nd1 = nd2;
    if (nd2 == nullptr)
        nd2 = nd1;
    if (nd1 != nd2) {
        if (Compare()(nd1->data, nd2->data))
            std::swap(nd1, nd2);
        nd1->rson = tnode_merge(nd1->rson, nd2);
        if (nd1->lson == nullptr || nd1->lson->dis < nd1->rson->dis)
            std::swap(nd1->lson, nd1->rson);
        nd1->dis = nd1->rson ? (nd1->rson->dis + 1) : 1;
    }
    return nd1;
}
```
接下来队列相关的几个操作就较为简单了
```cpp
template <typename T, class Compare = std::less<T>> class priority_queue {
  public:
    /**
     * TODO constructors
     */
    priority_queue() : rt(nullptr), siz(0) {}
    priority_queue(const priority_queue &other) : rt(tnode_copy(other.rt)), siz(other.siz) {}
    /**
     * TODO deconstructor
     */
    ~priority_queue() { tnode_clean(rt); }
    /**
     * TODO Assignment operator
     */
    priority_queue &operator=(const priority_queue &other) {
        if (this == &other)
            return *this;
        tnode_clean(rt);
        rt = tnode_copy(other.rt);
        siz = other.siz;
        return *this;
    }
    /**
     * get the top of the queue.
     * @return a reference of the top element.
     * throw container_is_empty if empty() returns true;
     */
    const T &top() const {
        if (siz == 0)
            throw container_is_empty();
        return rt->data;
    }
    /**
     * TODO
     * push new element to the priority queue.
     */
    void push(const T &e) {
        tnode *tmp = new tnode(e);
        siz++;
        rt = tnode_merge(rt, tmp);
    }
    /**
     * TODO
     * delete the top element.
     * throw container_is_empty if empty() returns true;
     */
    void pop() {
        if (siz == 0)
            throw container_is_empty();
        tnode *tmp = rt;
        rt = tnode_merge(rt->lson, rt->rson);
        delete tmp;
        siz--;
    }
    /**
     * return the number of the elements.
     */
    size_t size() const { return siz; }
    /**
     * check if the container has at least an element.
     * @return true if it is empty, false if it has at least an element.
     */
    bool empty() const { return siz == 0; }
    /**
     * merge two priority_queues with at least O(logn) complexity.
     * clear the other priority_queue.
     */
    void merge(priority_queue &other) {
        rt = tnode_merge(rt, other.rt);
        siz += other.siz;
        other.rt = nullptr;
        other.siz = 0;
    }
};
```