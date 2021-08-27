---
title: "Github Pages"
date: 2021-08-06T23:55:31+08:00
---

GitHub Pages 相当于自己的网站，域名为 <username>.github.io。

Github Pages 支持 **html 格式**的文件和 **markdown 格式**的文件。入口文件为 index.html 或 index.md。

## 概述

例子使用 markdown 文件，并且用 loppo 工具来生成 html 文件。使用 GitHub Actions 自动化执行生成 html 文件操作，并且自动部署到 docs 分支下。

使用 loppo 的主要原因是它可以自动生成索引，不需要自己写一个文件作为索引。

## 流程

1. 在 master 分支下编写 loppo.yml、.github/workflows/<自定义文件名>.yml 文件，使用 `npm init` 生成 package.json 文件。
2. 在 docs 文件夹下编写 markdown 文件。
3. Push 到 GitHub，自动执行 Actions。

## 配置文件介绍

### loppo.yml

```yaml
dir: docs # 源文件夹
output: dist # 目标文件夹
site: Documents
theme: oceandeep
customization: false
themeDir: loppo-theme
direction: ltr
id: JetYang98.github.io
```

### package.json

使用 `npm init` 命令生成。注意添加 **dependencies** 属性。

```json
{
  "name": "jetyang98.github.io",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "directories": {
    "doc": "docs"
  },
  "scripts": {
    "build": "loppo"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/jetyang98/JetYang98.github.io.git"
  },
  "author": "Jet Yang",
  "license": "Apache",
  "bugs": {
    "url": "https://github.com/jetyang98/JetYang98.github.io/issues"
  },
  "homepage": "https://github.com/jetyang98/JetYang98.github.io#readme",
  "dependencies": {
    "loppo": "^0.6.23"
  }
}
```

### GitHub Actions 配置

见[GitHub Actions](../github-actions)。

## 修改 GitHub Pages 默认显示分支

Settings -> Pages -> Branch 改为 docs。
