# 建站全过程实录

## 安装并配置 Hexo

1. 安装 Git, Node
2. 安装 hexo-cli
```
npm install -g hexo-cli
```
3. 初始化项目
```
hexo init conless.github.io
cd conless.github.io
npm install
hexo server
```
4. 接下来就可以通过访问 https://localhost:4000 访问博客了.

## 配置 Shoka

首先安装主题与依赖插件
```
git clone https://github.com/amehime/hexo-theme-shoka.git ./themes/shoka
npm install --save hexo-renderer-multi-markdown-it hexo-autoprefixer hexo-algoliasearch hexo-symbols-count-time hexo-feed
```
再修改站点配置
```
theme: shoka
```
并新建 _config.shoka.yml

接下来可以进行相关配置
