---
title: Isaac Sim4.5.0在Ubuntu22.04LTS上安装指南(无头服务器版)
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

**报错原因**
Omniverse/Kit 的技术要求里明确写出：535.255 以上在 Vulkan 里可能被错误上报导致误判不兼容。而本机恰好为535.255以上，所以导致“driver 不支持” 的误判。
需要禁用driver 校验：`--/rtx/verifyDriverVersion/enabled=false`

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

## 关闭默认的ROS2 Bridge
由于不需要ROS，所以需要把ROS2 Bridge置空
https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_ros_other_platforms.html
官方做法为改 `~/isaacsim/apps/isaacsim.exp.full.kit` 里的一行，把 ROS2 bridge 置空
先备份原文件：
`cp ~/isaacsim/apps/isaacsim.exp.full.kit ~/isaacsim/apps/isaacsim.exp.full.kit.bak`
回看当前值：
`grep -n "isaac.startup.ros_bridge_extension" ~/isaacsim/apps/isaacsim.exp.full.kit`
    输出：`147:isaac.startup.ros_bridge_extension = "" 149:isaac.startup.ros_bridge_extension = "isaacsim.ros2.bridge"`
将其置空：
`sed -i 's|^isaac\.startup\.ros_bridge_extension *=.*|isaac.startup.ros_bridge_extension = ""|g' \ ~/isaacsim/apps/isaacsim.exp.full.kit`
最后可以再运行查看当前值的指令确认一遍
    输出：`147:isaac.startup.ros_bridge_extension = "" 149:isaac.startup.ros_bridge_extension = ""`


## 安装Isaac Lab2.0
**设置环境变量**
需先退出conda环境，检查方式：`echo "$CONDA_PREFIX"`输出为空就ok。
接下来设置Isaac Sim环境变量：
```
export ISAACSIM_PATH="$HOME/isaacsim"
export ISAACSIM_PYTHON_EXE="$ISAACSIM_PATH/python.sh"
```
验证Isaac Sim的python能不能跑：`${ISAACSIM_PYTHON_EXE} -c "print('isaac sim python ok')"`
**Clone Isaac Lab**
```
cd ~
git clone https://github.com/isaac-sim/IsaacLab.git
cd IsaacLab
git checkout v2.0.2 #切换到v2.0.2版本
```
**建立_isaac_sim 符号链接**
```
cd ~/IsaacLab
ln -s "$ISAACSIM_PATH" _isaac_sim
ls -l _isaac_sim | head
```
输出`lrwxrwxrwx 1 gy gy 17  1月  7 20:51 _isaac_sim -> /home/gy/isaacsim`
**安装Isaac Lab
第一次安装时速度会较慢。
```
cd ~/IsaacLab
./isaaclab.sh --install rsl_rl
```
