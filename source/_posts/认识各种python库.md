---
title: python库记录
date: 2026-01-07 15:30:00
tags: [python库,认识]
categories: 
    - 教程系列
    - 常用工具
---

# python自带模块
argparse	解析命令行参数（如 --samples、--count 等）。
dataclasses	定义结构化配置类 StoneConfig、StoneMesh。
importlib.util	用于判断 scipy 是否可用。
pathlib.Path	文件路径与目录处理（输出 .obj）。
typing	类型标注（如 Literal、Tuple）。
from __future__ import annotations	让类型注解延迟解析，避免前向引用问题。

# 第三方库
**numpy**
用途：数值计算、随机采样、向量/矩阵运算（采样点、归一化方向、比例缩放等都用到）。
**scipy**
用途：用于 ConvexHull 生成凸包面片，否则只能输出点云（没有面）。
