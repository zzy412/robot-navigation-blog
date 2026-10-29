
# 移动机器人运动规划课程学习

> Motion Planning for Mobile Robots

本栏目记录我学习《Motion Planning for Mobile Robots》课程的过程，主要围绕路径搜索、采样式规划与考虑运动学约束的路径规划方法展开。

目前已经学习了课程前四讲，并将部分理论应用于自己的 C++ 阿克曼无人车运动规划项目。

---

## Lecture 1：Motion Planning for Mobile Robots

### 移动机器人运动规划概述

第一讲主要介绍机器人自主导航系统的整体架构，以及运动规划在完整导航系统中的作用。

主要学习内容：

- 机器人自主导航系统的基本组成
- 环境感知、定位、建图、规划与控制之间的关系
- 前端路径搜索与后端轨迹优化
- 栅格地图、OctoMap、TSDF、ESDF 等地图表示方法
- 运动规划的主要算法分类

**学习收获：**

理解了运动规划并不是单一的路径搜索问题，而是需要与环境建模、机器人运动约束以及控制模块相互配合。

---

## Lecture 2：Search-based Path Finding

### 基于搜索的路径规划

第二讲重点介绍了图搜索算法与启发式搜索方法。

主要学习算法：

| 算法 | 核心思想 |
|---|---|
| DFS | 深度优先搜索 |
| BFS | 广度优先搜索 |
| Dijkstra | 根据累计路径代价扩展节点 |
| A* | 结合累计代价与启发式估计 |
| Weighted A* | 对启发式函数进行加权 |
| JPS | 利用规则栅格中的路径对称性减少搜索节点 |

其中，A* 算法的评价函数为：

$$
f(n)=g(n)+h(n)
$$

- `g(n)`：从起点到当前节点的累计代价。
- `h(n)`：从当前节点到目标的估计代价。
- `f(n)`：估计的总代价。

### 相关实践

我已经使用 C++ 实现 A* 路径规划，并将其作为 Hybrid A* 实验的基础对照算法。

相关资源：

- [A* 与 Hybrid A* 路径规划实验](../algorithms/hybrid-a-star.md)
- [PathFinding.js 在线算法可视化](https://qiao.github.io/PathFinding.js/visual/)

---

## Lecture 3：Sample-based Path Finding

### 基于采样的路径规划

第三讲主要介绍通过随机采样探索配置空间的路径规划方法。

重点学习：

- PRM（Probabilistic Roadmap）
- RRT（Rapidly-exploring Random Tree）
- RRT-Connect
- RRT*
- Informed RRT*
- Kinodynamic RRT*

### 主要理解

PRM 通过采样构建路线图，适合在同一环境中处理多次路径查询。

RRT 从起点逐步扩展搜索树，通过随机采样探索状态空间。

RRT* 在 RRT 的基础上引入父节点优化和邻域重连接机制，在适当条件下具有渐近最优性。

### 后续实践方向

目前这部分以理论学习为主。

后续计划使用 PythonRobotics 和 OMPL 学习 RRT*，并考虑将采样式规划方法作为 Hybrid A* 的对照算法。

参考项目：

- [PythonRobotics](https://github.com/AtsushiSakai/PythonRobotics)
- [OMPL](https://github.com/ompl/ompl)

---

## Lecture 4：Kinodynamic Path Finding

### 考虑运动约束的路径规划

第四讲重点研究机器人运动学与动力学约束对规划问题的影响。

主要学习：

- State Lattice
- 运动基元（Motion Primitives）
- 控制空间采样
- 状态空间搜索
- 边界值问题（BVP）
- Kinodynamic RRT*
- Hybrid A*

### 阿克曼车辆运动学

对于阿克曼转向无人车，可以使用简化的运动学自行车模型：

$$
\begin{aligned}
\dot{x} &= v\cos\theta \\
\dot{y} &= v\sin\theta \\
\dot{\theta} &= \frac{v}{L}\tan\delta
\end{aligned}
$$

其中：

- `x, y`：车辆位置
- `theta`：车辆航向角
- `v`：车辆速度
- `L`：车辆轴距
- `delta`：前轮转向角

### 相关实践

在 C++ 项目中，我已经实现基于车辆运动学模型的 Hybrid A* 算法，通过离散转向输入生成运动基元，并在路径搜索过程中进行碰撞检测。

[查看 Hybrid A* C++ 实现](../algorithms/hybrid-a-star.md)

---

## 课程学习总结

通过前四讲课程，我逐步建立了以下知识体系：

**机器人导航系统 → 地图表示 → 图搜索 → 随机采样 → 运动约束规划 → 轨迹跟踪**

其中，A*、Hybrid A* 和车辆运动学模型已经应用于当前 C++ 仿真实验。

下一阶段，我将继续学习轨迹优化和控制算法，并结合 ROS 2 平台开展系统级实验。

---

## 相关学习资源

- [PythonRobotics](https://github.com/AtsushiSakai/PythonRobotics)
- [PathFinding.js](https://github.com/qiao/PathFinding.js)
- [OMPL](https://github.com/ompl/ompl)
- [Hybrid A* Path Planner](https://github.com/karlkurzer/path_planner)
- [我的 GitHub 项目](https://github.com/zzy412/Robot-Motion-Planning)
