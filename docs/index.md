
# 机器人运动规划与导航学习笔记

> Robot Motion Planning & Navigation Notes

欢迎来到我的个人技术博客！

本博客主要记录我在机器人自主导航、运动规划与轨迹跟踪领域的学习和实践，包括课程学习、科研论文阅读、C++ 算法实现、ROS 2 系统开发以及仿真实验。

目前重点研究**面向阿克曼转向无人车的运动规划与轨迹跟踪方法**。

---

## 🚗 一、项目简介

在机器人自主导航系统中，路径规划负责生成从起点到目标位置的参考路径，轨迹跟踪控制则负责使机器人沿参考路径运动。

对于阿克曼转向无人车，由于存在最大转向角、最小转弯半径和转向速率等约束，传统二维 A* 算法生成的路径不一定能够被车辆直接执行。

因此，本项目从基础 A* 算法出发，逐步实现 Hybrid A* 路径规划，并结合 Pure Pursuit 控制器研究车辆的轨迹跟踪性能。

### 项目技术路线

**二维地图 → A* / Hybrid A* → Pure Pursuit → 速度规划 → ROS 2 仿真**

当前研究主要围绕：

1. 基于搜索的路径规划算法。
2. 阿克曼车辆运动学建模。
3. Hybrid A* 运动学约束路径规划。
4. Pure Pursuit 轨迹跟踪控制。
5. 自适应前瞻距离与速度规划。
6. ROS 2 系统集成与 RViz2 可视化。

---

## 📚 二、博客内容导航

### 1. 运动规划课程学习

学习《Motion Planning for Mobile Robots》课程，主要包括：

- 移动机器人运动规划基础
- BFS、Dijkstra、A* 和 JPS
- PRM、RRT、RRT* 和 Informed RRT*
- State Lattice、运动基元和 Hybrid A*

[查看课程学习笔记](courses/index.md)

### 2. 科研论文精读

目前重点阅读了以下论文：

- Fast-Planner：动力学约束搜索与轨迹优化
- EGO-Planner：高效局部轨迹优化
- GCOPTER / MINCO：受约束轨迹优化
- FAST-LIO2：激光惯性里程计与建图
- SysNav：分层语义目标导航

[查看论文阅读笔记](papers/index.md)

### 3. C++ 运动规划算法实现

使用 C++17 和 CMake 搭建阿克曼无人车运动规划仿真系统。

主要实现：

- 二维栅格地图
- A* 路径规划
- Hybrid A* 路径规划
- 车辆运动学模型
- 碰撞检测与路径可视化

[查看 Hybrid A* 算法实验](algorithms/hybrid-a-star.md)

### 4. Pure Pursuit 轨迹跟踪实验

在 C++ 仿真环境中开展：

- Pure Pursuit 路径跟踪
- 固定与自适应前瞻距离对比
- 最大转向速率约束实验
- 曲率自适应速度规划
- 多场景控制性能评估

[查看 Pure Pursuit 实验结果](tracking/pure-pursuit-experiments.md)

### 5. ROS 2 系统集成

基于 WSL2 Ubuntu 24.04 和 ROS 2 Jazzy，逐步将 C++ 算法集成到机器人系统中。

已开展：

- ROS 2 工作空间与功能包创建
- Hybrid A* 规划节点
- 阿克曼车辆运动学仿真节点
- 地图、路径、里程计和 TF 发布
- RViz2 可视化

当前 ROS 2 仿真仍在完善在线闭环轨迹跟踪功能。

[查看 ROS 2 仿真教程](ros2/ackermann-ros2-simulation.md)

---

## 🛠️ 三、技术栈

| 分类 | 技术 |
|---|---|
| 编程语言 | C++17、Python |
| 开发工具 | Visual Studio 2022、VS Code |
| 构建工具 | CMake、colcon |
| 操作系统 | Windows、Ubuntu 24.04 |
| 机器人平台 | ROS 2 Jazzy |
| 可视化工具 | RViz2、SVG |
| 路径规划 | A*、Hybrid A* |
| 轨迹跟踪 | Pure Pursuit |
| 版本管理 | Git、GitHub |
| 博客平台 | MkDocs、GitHub Pages |

---

## 📊 四、阶段性研究成果

### 1. A* 与 Hybrid A* 路径规划

已完成两种路径规划算法的 C++ 仿真实现。

实验主要比较：

- 路径搜索成功情况
- 路径长度
- 规划计算时间
- 搜索扩展节点数量
- 车辆运动学可行性

### 2. Pure Pursuit 轨迹跟踪

已完成 Pure Pursuit 控制器及相关参数实验。

在五种仿真场景中，对四种前瞻距离与速度控制组合进行了对比。

已有实验结果表明，自适应速度规划能够在所测试场景中改善部分轨迹跟踪误差指标，但也会增加行驶时间。

### 3. ROS 2 车辆仿真

已实现 ROS 2 规划节点与车辆运动学仿真节点，并能够在 RViz2 中显示：

- 二维占据栅格地图
- Hybrid A* 规划路径
- 车辆模型
- 实际运动轨迹

下一阶段将实现规划路径与车辆控制器之间的实时闭环连接。

---

## 💻 五、项目源代码

本项目的独立 C++ 运动规划工程已公开到 GitHub。

### Robot-Motion-Planning

**项目地址：**

[https://github.com/zzy412/Robot-Motion-Planning](https://github.com/zzy412/Robot-Motion-Planning)

项目采用 C++17 和 CMake 开发，包含 A*、Hybrid A* 路径规划算法及相关实验文件。

代码仓库提供 Visual Studio 2022 的构建和运行说明。

部分后续轨迹跟踪实验及 ROS 2 系统代码仍在整理中，具体公开内容以仓库实际文件为准。

---

## 🎯 六、未来研究计划

接下来计划继续完善：

1. ROS 2 平台下的 Pure Pursuit 在线闭环控制。
2. Hybrid A* 路径规划与速度规划的协同优化。
3. 转向角与转向速率约束建模。
4. 复杂障碍物场景下的轨迹跟踪实验。
5. 不同规划和控制算法的性能对比。
6. 仿真实验向真实阿克曼无人车平台的迁移。

---

## 🔗 七、相关链接

- [我的 GitHub 主页](https://github.com/zzy412)
- [Robot-Motion-Planning 代码仓库](https://github.com/zzy412/Robot-Motion-Planning)
- [PythonRobotics](https://github.com/AtsushiSakai/PythonRobotics)
- [PathFinding.js 可视化](https://qiao.github.io/PathFinding.js/visual/)
- [ROS 2 Jazzy 官方文档](https://docs.ros.org/en/jazzy/)

---

*本博客将持续更新机器人运动规划领域的学习笔记、算法实现、仿真实验和科研进展。*
