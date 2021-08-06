---
title: "Github Actions"
date: 2021-08-06T23:54:36+08:00
---

GitHub actions是一个非常好用的自动化工具，可以在满足某种条件下，自动执行某些任务。比如当代码push到master时，在Ubuntu平台下执行node.js脚本等。

## 如何使用

### 创建工作流

在GitHub网页上点击`Actions`创建一个新的工作流。

### 模板介绍

```yaml
name: CI

# 任务触发条件
on:
  # 当push到master时触发
  push:
    branches: [ master ]
  # 当pr到master时触发
  pull_request:
    branches: [ master ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  build-pages:
    # 该job运行平台
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2

      # 安装node.js
      - name: Setup Node.js
        uses: actions/setup-node@main
        with:
          node-version: '12.18.3'

      # 安装依赖，使用package.json文件
      - name: Install dependencies
        run: npm install

      # 运行package.json文件里的build命令
      - name: Build pages
        run: npm run build
        
      # 把dist文件夹的内容部署到docs分支下
      - name: Deploy to website
        uses: JamesIves/github-pages-deploy-action@4.1.4
        with:
          branch: docs # The branch the action should deploy to.
          folder: dist # The folder the action should deploy.
```
