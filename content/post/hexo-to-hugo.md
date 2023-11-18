---
title: '从hexo到hugo的迁移'
date: 2023-11-11T09:57:59+08:00
description: 本篇文章记录一下自己的博客系统由hexo转到hugo的过程
tags:
    - 博客
---
# 本地部分
## 安装hugo框架
我选择使用winget在本地先部署
```
winget install Hugo.Hugo.Extended
```
如果使用其他包管理器或系统请参考hugo官方文档

## 搭建hugo系统
example为你的博客名字
```
hugo new site example
```
然后cd到该文件夹下
```
cd example
```
初始化git仓库
```
git init
```
安装主题，我这里采用直接从仓库clone安装，以stack主题为例
```
git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
```
由于我习惯使用`yaml`格式来敲配置，所以我们将设置文件改为`hugo.yaml`  
然后将所有的`=`改为`:`  
同时我们还要修改`archetypes`目录下的`default.md`，全部替换为以下内容
```markdown
---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: {{ .Date }}
draft: true
---
```
修改根目录下的`hugo.yaml`文件，添加以下配置来应用主题
```yaml
theme: 'hugo-theme-stack'
```
其中`'hugo-theme-stack'`为你theme目录下的主题名  
可以参考[我的配置文件](https://github.com/h3ll0www0rld/hugo-blog-source/blob/main/hugo.yaml)


## 关于搜索、归档、链接等
进入`themes/hugo-theme-stack/exampleSite/content/page`中，将所有内容覆盖到你的`content`文件夹里

## 写一篇文章
来到根目录下，输入
```
hugo new post/example.md
```
然后会在`content/post`文件夹下生成`example.md`  
然后就可以通过markdown开始写作了

## 关于美化
我这里不多赘述，自行谷歌或百度


# 云端部署
这里简述一下原理：  
源码提交到Github -> Github Actions自动构建并推送到另一Github分支 -> Github Pages
途中试过使用Vercel托管，但不知道为啥会报错

# 开源地址
如果你想直接抄作业的话，[repo](https://github.com/h3ll0www0rld/hugo-blog-source)