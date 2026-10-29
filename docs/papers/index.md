# 机器人导航与运动规划论文阅读

本栏目主要记录机器人运动规划、轨迹优化、SLAM 和分层导航方向的论文学习笔记。

目前重点阅读了以下五篇论文。

## 1. Fast-Planner

**论文：** Robust and Efficient Quadrotor Trajectory Generation for Fast Autonomous Flight

**研究方向：** 动力学约束搜索与轨迹优化

论文结合 Kinodynamic Path Searching、B-spline 轨迹优化和时间分配方法，实现快速且满足运动约束的轨迹生成。

重点学习内容包括运动基元、启发式搜索、轨迹平滑和动态可行性。

**对当前项目的启发：** 可以在 Hybrid A* 生成参考路径后，继续考虑轨迹优化和速度分配。

## 2. EGO-Planner

**论文：** EGO-Planner: An ESDF-free Gradient-based Local Planner for Quadrotors

**研究方向：** 高效局部轨迹优化

论文利用无碰撞引导路径构造避障梯度，避免维护完整 ESDF，并通过 B-spline 优化改善轨迹平滑性、安全性和动态可行性。

**对当前项目的启发：** 为后续研究局部避障、轨迹优化及计算效率提供参考。

## 3. MINCO / GCOPTER

**论文：** Geometrically Constrained Trajectory Optimization for Multicopters

**研究方向：** 受约束轨迹优化

论文提出 MINCO 轨迹表示，实现空间轨迹形状与时间分配的联合优化，并考虑几何安全约束和系统动态约束。

**对当前项目的启发：** 为研究行驶速度、轨迹跟踪精度与车辆运动约束之间的协调关系提供理论参考。

## 4. FAST-LIO2

**论文：** FAST-LIO2: Fast Direct LiDAR-inertial Odometry

**研究方向：** 激光惯性里程计与实时建图

论文利用激光雷达和 IMU 的紧耦合状态估计、原始点云直接配准及 ikd-Tree 增量地图管理，提高定位建图效率。

**对当前项目的启发：** 为未来接入真实传感器、实现机器人定位与地图构建提供参考。

## 5. SysNav

**论文：** SysNav: Multi-Level Systematic Cooperation Enables Real-World, Cross-Embodiment Object Navigation

**研究方向：** 分层语义导航

论文将目标导航划分为高层语义推理、中层导航规划与底层运动控制，结合结构化场景表示和视觉语言模型实现复杂环境中的目标搜索。

**对当前项目的启发：** 有助于理解自主导航系统的分层模块设计，并为后续扩展语义导航任务提供思路。

## 阅读总结

以上论文分别从轨迹规划、局部优化、状态估计和系统级导航等角度，展示了机器人自主导航中的关键技术。

当前项目主要以阿克曼无人车路径规划和轨迹跟踪为研究重点，因此将优先借鉴 Fast-Planner、EGO-Planner 和 MINCO/GCOPTER 的规划优化思想，同时将 FAST-LIO2 和 SysNav 作为后续完整导航系统建设的参考。

需要注意，前三篇论文主要面向多旋翼飞行器，其具体运动模型和优化约束不能直接套用于阿克曼车辆。