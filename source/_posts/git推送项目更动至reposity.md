---
title: Git使用教程——将本地修改的代码推送至git仓库
date: 2026-01-07 15:30:00
tags: [git,使用教程]
categories: 
    - 教程系列
    - 常用工具
---

使用密钥将仓库和本地代码关联后，后续的修改上传至仓库主要经过以下步骤：
## 终端方式
1. **收集修改**
`git add .`
2. **确认存档**
`git commit -m "备注，例如：修复了碰撞检测的bug"`
3. 上传云端
`git push`

## 图形界面
VSCode中，选择左侧**source control** -> 点击**Changes旁边的+号** -> **Message**写备注 -> **Commit**

`git status`查看文件是否修改、add、commit。

网页推送：
1. 存稿
git add .
git commit -m "新增文章: ......"
git push origin source
2. 发布
npx hexo clean && npx hexo g && npx hexo d