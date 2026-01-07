---
title: Isaac Sim4.5.0及Isaac Lab2.0在Ubuntu22.04LTS上安装指南(无头服务器版)
date: 2026-01-05 18:40:00
tags: [Isaac Sim,Isaac Lab,Ubuntu，安装教程]
categories: 
    - 教程系列
    - 常用工具
---

Isaac Sim4.5.0下载链接：https://docs.isaacsim.omniverse.nvidia.com/4.5.0/installation/download.html
## 获取Isaac Sim4.5.0压缩包并解压
Isaac Sim4.5.0下载链接：https://docs.isaacsim.omniverse.nvidia.com/4.5.0/installation/download.html
进入一个下载目录:
`cd ~/下载`
点击下载链接中——**Latest Release**右侧的Linux版本，等待下载，得到一个名为isaac-sim-standalone-4.5.0-linux-x86_64.zip的压缩包。
下载完成后，将.zip安装包解压到目标目录~/isaacsim：
`mkdir -p ~/isaacsim`
`cd ~/isaacsim`
`unzip "isaac-sim-standalone-4.5.0-linux-x86_64.zip" -d ~/isaacsim`
## 工作站设置
参考官网说明：https://docs.isaacsim.omniverse.nvidia.com/4.5.0/installation/install_workstation.html
终端运行：
`./post_install.sh`
`/isaac-sim.selector.sh`
PS:如果使用无头服务器安装，那么`/isaac-sim.selector.sh`可以先忽略。
## 设置环境变量
参考官网说明：https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/binaries_installation.html
**验证isaac-sim安装**
`export ISAACSIM_PATH="${HOME}/isaacsim"`
`export ISAACSIM_PYTHON_EXE="${ISAACSIM_PATH}/python.sh"`
**验证python路径**
`${ISAACSIM_PYTHON_EXE} -c "print('Isaac Sim configuration is now complete.')"`
PS:如果之前装过别的版本又删了，建议重置用户配置
`${ISAACSIM_PATH}/isaac-sim.sh --reset-user`

## 无头启动方式
`cd ~/isaacsim
./isaac-sim.sh --no-window \
  --/rtx/verifyDriverVersion/enabled=false \
  --/isaac/startup/ros_bridge_extension= \
  --/app/quitAfter=20`


### 后续的内容为个人遇到报错的简要记录，请勿参考
第一次load大约花了三分钟：`[202.795s] Isaac Sim Full App is loaded.`

## 一键启动脚本
在~/isaacsim下新建`run_headless.sh`
```
cat > ~/isaacsim/run_headless.sh <<'SH'
#!/usr/bin/env bash
set -e
cd "$(dirname "$0")"
./isaac-sim.sh --no-window \
  --/rtx/verifyDriverVersion/enabled=false \
  --/isaac/startup/ros_bridge_extension= \
  "$@"
SH
chmod +x ~/isaacsim/run_headless.sh
```
启动方式：
`~/isaacsim/run_headless.sh --/app/quitAfter=5`

