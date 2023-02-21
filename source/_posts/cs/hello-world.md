---
title: Hello, World!
author: Conless
date: 2023-01-19 22:56
categories:
- [Computer Science]
---

欢迎来到 [Conless 的新博客](https://conless.dev)！本博客使用 [Hexo](https://hexo.io) 搭建，采用了 [Shoka](https://shoka.lostyu.me/) 主题，希望大家喜欢。

## 搭建过程

### 安装并配置 Hexo

1. 安装 Git, Node
2. 安装 hexo-cli
```bash
npm install -g hexo-cli
```
3. 初始化项目
```bash
hexo init conless.github.io
cd conless.github.io
npm install
hexo server
```
4. 接下来就可以通过访问 https://localhost:4000 访问博客了.

### 配置 Shoka

首先安装主题与依赖插件
```bash
git clone https://github.com/amehime/hexo-theme-shoka.git ./themes/shoka
npm install --save hexo-renderer-multi-markdown-it hexo-autoprefixer hexo-algoliasearch hexo-symbols-count-time hexo-feed
```
再修改站点配置
```yml
theme: shoka
```
并新建 _config.shoka.yml

接下来可以进行相关配置，完成后通过
```bash
hexo g -d
```
传到远端即完成了建站。

### GitHub Pages 与自定义域名
```cpp
// TODO
```