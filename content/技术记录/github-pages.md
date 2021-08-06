---
title: "Github Pages"
date: 2021-08-06T23:55:31+08:00
---

GitHub pages相当于自己的网站，域名为`<username>.github.io`。

Github pages支持**html格式**的文件和**markdown格式**的文件。入口文件为`index.html`或`index.md`。

## 概述

例子使用markdown文件，并且用loppo工具来生成html文件。使用GitHub Actions自动化执行生成html文件操作，并且自动部署到docs分支下。

使用loppo的主要原因是它可以自动生成索引，不需要自己写一个文件作为索引。

## 流程

1. 在master分支下编写loppo.yml、.github/workflows/<自定义文件名>.yml文件，使用`npm init`生成package.json文件。
2. 在docs文件夹下编写markdown文件。
3. Push到GitHub，自动执行Actions。

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

使用`npm init`命令生成。注意添加**dependencies**属性。

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

### GitHub Actions配置

见[GitHub Actions](../github-actions)。

## 修改GitHub Pages默认显示分支

Settings -> Pages -> Branch改为docs。
