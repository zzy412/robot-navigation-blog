
# 机器人运动规划与导航论文精读

本栏目记录我在机器人自主导航、路径规划、轨迹优化、SLAM 和语义导航方向阅读的科研论文。

目前重点学习了五篇论文，分别涉及运动规划、轨迹优化、激光惯性里程计和分层语义导航。

需要说明的是，这些论文的研究对象并不完全相同。其中 Fast-Planner、EGO-Planner 和 GCOPTER 主要面向多旋翼机器人，相关思想需要根据阿克曼车辆的运动约束进行适配。

---

## 1. Fast-Planner

**论文名称：**

Robust and Efficient Quadrotor Trajectory Generation for Fast Autonomous Flight

**研究方向：** 动力学约束路径搜索与轨迹优化

### 主要研究内容

Fast-Planner 将考虑动力学约束的路径搜索与轨迹优化结合起来，为四旋翼机器人生成可执行的飞行轨迹。

主要技术包括：

- Kinodynamic Path Searching
- 运动基元生成
- B-spline 轨迹优化
- 轨迹时间分配
- 运动可行性约束

### 对当前项目的启发

目前我的 C++ 项目主要通过 Hybrid A* 生成车辆运动学可行路径。

Fast-Planner 为后续研究规划路径的平滑处理、速度规划与轨迹可执行性提供了参考。

**GitHub：**

[HKUST-Aerial-Robotics/Fast-Planner](https://github.com/HKUST-Aerial-Robotics/Fast-Planner)

---

## 2. EGO-Planner

**论文名称：**

EGO-Planner: An ESDF-free Gradient-based Local Planner for Quadrotors

**研究方向：** 高效局部轨迹优化

### 主要研究内容

EGO-Planner 研究如何在复杂障碍物环境中高效优化飞行轨迹。

其重要特点是不需要持续构建完整的 ESDF 地图，而是根据碰撞区域和引导路径构造优化信息。

主要技术包括：

- ESDF-free 轨迹优化
- B-spline 轨迹表示
- 碰撞代价与平滑代价
- 梯度优化
- 轨迹动态可行性调整

### 对当前项目的启发

EGO-Planner 展示了如何在避障约束与计算效率之间进行权衡。

未来可以借鉴其优化思想，对 Hybrid A* 输出的参考路径开展进一步研究，但不能直接使用四旋翼运动模型代替阿克曼车辆模型。

**GitHub：**

[ZJU-FAST-Lab/ego-planner](https://github.com/ZJU-FAST-Lab/ego-planner)

---

## 3. MINCO / GCOPTER

**论文名称：**

Geometrically Constrained Trajectory Optimization for Multicopters

**研究方向：** 几何约束与轨迹优化

### 主要研究内容

该论文提出高效的轨迹优化方法，利用 MINCO 轨迹表示和相关优化技术处理轨迹几何约束与动态约束。

主要学习内容：

- MINCO 轨迹表示
- 多项式轨迹优化
- 时间分配
- 几何安全约束
- 动态可行性约束

### 对当前项目的启发

该论文帮助我理解轨迹生成并不仅仅是寻找一条无碰撞路径，还需要进一步考虑运动系统的约束以及优化目标。

对于阿克曼无人车，后续可进一步探索参考路径、行驶速度和轨迹跟踪性能之间的协同优化问题。

**GitHub：**

[ZJU-FAST-Lab/GCOPTER](https://github.com/ZJU-FAST-Lab/GCOPTER)

---

## 4. FAST-LIO2

**论文名称：**

FAST-LIO2: Fast Direct LiDAR-inertial Odometry

**研究方向：** 激光惯性里程计与实时定位建图

### 主要研究内容

FAST-LIO2 研究如何将激光雷达和 IMU 信息紧耦合，用于高效估计机器人运动状态。

重点技术包括：

- LiDAR 与 IMU 融合
- 迭代扩展卡尔曼滤波
- 原始点云直接配准
- ikd-Tree 地图管理
- 实时状态估计

### 对当前项目的启发

当前项目主要使用预设二维地图和仿真车辆位姿，没有完成真实传感器定位建图。

FAST-LIO2 为未来接入激光雷达与 IMU、构建真实机器人导航系统提供了学习参考。

**GitHub：**

[hku-mars/FAST_LIO](https://github.com/hku-mars/FAST_LIO)

---

## 5. SysNav

**论文名称：**

SysNav: Multi-Level Systematic Cooperation Enables Real-World, Cross-Embodiment Object Navigation

**研究方向：** 分层语义目标导航

### 主要研究内容

SysNav 通过不同层次的模块合作实现目标导航任务，将高层语义决策与较低层次的导航规划、运动控制连接起来。

主要学习内容：

- 多层次导航架构
- 视觉语言模型辅助语义推理
- 结构化场景表示
- 房间级导航决策
- 不同机器人平台之间的任务协作

### 对当前项目的启发

SysNav 帮助我理解机器人导航系统中的语义决策、路径规划与运动控制之间的层次关系。

当前项目主要聚焦底层运动规划与轨迹跟踪，SysNav 则为未来拓展语义导航任务提供系统级研究思路。

---

## 论文阅读总结

通过以上五篇论文，我对机器人导航领域的不同技术模块有了更完整的认识。

| 论文 | 主要研究领域 | 对当前项目的帮助 |
|---|---|---|
| Fast-Planner | 动力学约束规划 | 运动基元与轨迹优化 |
| EGO-Planner | 局部轨迹优化 | 避障与优化效率 |
| GCOPTER | 受约束轨迹优化 | 轨迹表示与时间分配 |
| FAST-LIO2 | 定位与建图 | 未来真实传感器接入 |
| SysNav | 语义导航 | 分层导航系统设计 |

我目前的研究重点仍是**阿克曼无人车的运动规划与轨迹跟踪**。

因此，下一阶段将优先深入学习与车辆运动学约束、Hybrid A*、速度规划和轨迹跟踪相关的研究工作。

---

## 我的相关项目

- [C++ Hybrid A* 路径规划实验](../algorithms/hybrid-a-star.md)
- [Pure Pursuit 轨迹跟踪实验](../tracking/pure-pursuit-experiments.md)
- [ROS 2 系统集成](../ros2/ackermann-ros2-simulation.md)
- [GitHub 源码仓库](https://github.com/zzy412/Robot-Motion-Planning)
