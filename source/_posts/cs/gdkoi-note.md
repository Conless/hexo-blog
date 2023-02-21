---
title: GDKOI2021 游记
date: 2021-01-20 11:25:43
categories:
- [Computer Science]

---
## Day -1
从学农回来了，已经快两个月没碰过信息学了。。

晚上家长还发了期末考排名。。挂的很厉害，要不是理科保命前20都没了。。

看了看自己的博客发现noip游记果然咕了，等WC2021退役后再来统一更吧

## Day 0
划水

## Day 1 (21.1.30)
进场用了半小时看题，感觉 $T1\ T2\ T3$ 可做，$T2$ 很像之前 $gsh$ 出的一题，但没深入想

### T3
按照开题顺序写吧，想了十分钟感觉可以直接预处理中心回文串+二分答案

本来想上 $manacher$ 的，感觉自己不是很熟悉...

码线段树打到一半发现可以直接静态用ST表做，然后花了大概40min写完过了大样例

### T2
之前没有认真想gsh那道题，导致这题搞了好久都没有搞出啥东西

最后写了个 $O((R-L)logn)$ 的暴力，期望分40-60

### T1
是个构造题，先打了送的 $50pts$，最后50分想不到遂写了个很吃数据的寻找增广路

### T4
没做

出来后发现大家T3也基本都用马拉车切了，感觉自己的多个log应该也没太大问题

T1好像随机化比枚举找增广路更优，希望能骗到点分吧...

T2大家都说是原题，裂开

T4是一个任意模NTT，好像有些人想到了但是没有码
估分50+50+100=200

裂开了...T1T2全挂完了，T1给我搞了个 $Restrict\ Function$，迷惑...

实际0+10+100

gsh rk16 wlr也很高

裂开

## Day 2

感觉 $T1\ T3$ 好像都不难，$T4$ 依旧没认真看题，先开 $T3$ 

### T3
还是回文串，还是不准备写 $manacher$（埋下伏笔）

预处理完就很自然的从前往后推就好了

### T1
是一个很烂的线性期望，之前甚至做过很类似的题

大概15分钟就码完了

### T2
送了 $40pts$

然后苦思冥想了2h...

感觉应该是用数据结构维护后缀最小值，但是想了想感觉还是优化不了多少

最后半小时发现确实是直接维护后缀边数就行了，赶紧乱码了个线段树跑过大样例

预测要挂分，所以把暴力特判加了上去

### T4
没做

T4送了30，心态炸裂

前三题大家都做得差不多，T2甚至还没多少人做出来，突然赶紧rank不会太低...

估分100+(60~100)+100+0=260~300

继续裂开...又挂分了

T3二分哈希被卡了30pts

T2果然有很多细节没处理

实际100+40+70=210，rk60，又是noip的排名...

dby拿了320的准标准分，rk20
day1+day2 gsh进队线了

## Day 3
看完题心态就有点小崩了，感觉除了T2都不可做，说不定今天连100pts都难

T2想了半小时还是只会暴力，遂先开T1

### T1
很容易想到枚举重边再加上可能性，但是误以为只有一个或零个公共点的情况很难处理（实际上是最开始一直把 $\Pi$ 当成 $\Sigma$ 了..）

以为是这里出了问题，导致小样例都过不去，只能跳了
最后才发现是累乘，直接裂开

### T3
试图找 $n=1$ 的规律，结果画错了。。。

遂暴力，期望得分15

### T4
今天反而觉得T4是最好拿分的，速切了 $subtask 2+3$，1居然没有深入想，出考场发现是个裸的状压，血亏

### T2
想了半天数据结构，但是感觉应该搞不了，然后再想了想应该是一个多项式的东西，却不会卷...

最后用 $unordered\_map$ 写了个暴力+去重，期望复杂度 $O(nlogn+nm)$（$m$ 是 $a$ 的前缀和中不同数的个数）

出考场发现大家估分都不高，$MCAdam$ 切了 $T1$ 大样例但是没处理细节，$T2$ 果然是个卷积，$T3$ n=1性质很显然，而我甚至连打表都没想过...

感觉今天难度远高于去年联合省选，感觉 $NOI2020\ Day1$ 可做的分都更多...

估分0+60+15+40=115

$T2$ 没过 $n=50000$，gsh和czy $n^2$ 过5万...

$T4$ 挂了，每个捆绑测试点各挂了一两个点...

今天连T2标准分60都没拿到，直接rk200，裂开了

## 总结
三天加起来挂了差不多200，不过必须说确实是自己实力不济，做题量和速度不够导致没时间对拍其实也是必然的。

总分375，rk60-80，还是noip水平，不过这几个月确实完全没有做题，所以也确实是真实水平吧

gsh rk16，在纪中校线限制下rk10，感觉应该稳队了

初三的xzd rk30，又被吊打了

必须要说其他人比自己就是努力多很多，所以这样的结果只能坦然接受，确实是技不如人

其他的话WC以后再说吧，WC于我而言应该纪念意义更强吧，毕竟冲击省队的希望确实不大，就当放松心情的娱乐周咯

先这样吧。