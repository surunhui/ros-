# Day 2 学习记录

## 今天的目标

认识 ROS 2 工作空间和 package 的基本结构：

- workspace 是什么
- package 是什么
- `src / build / install / log` 是什么
- `colcon build` 是什么
- `source install/setup.bash` 是什么

## 最重要的一句话

`先把 package 放进 src，再用 colcon build 生成 build / install / log，最后 source install/setup.bash。`

## 通俗理解

### workspace 是什么

最通俗地说，`workspace` 就像一个 ROS 2 总工地。

### package 是什么

最通俗地说，`package` 就像工地里的一个小功能盒子。

### src 是什么

最通俗地说，`src` 是放源码和 package 的地方。

### build 是什么

最通俗地说，`build` 是施工中的中间结果区。

### install 是什么

最通俗地说，`install` 是施工完成后可以使用的成品区。

### log 是什么

最通俗地说，`log` 是施工记录本。

## 这次走过的关键步骤

### 1. 创建工作空间目录

创建工作空间和源码目录：

```bash
mkdir -p ~/ros2_ws/src
```

然后进入工作空间：

```bash
cd ~/ros2_ws
```

一开始工作空间里只有：

```bash
src
```

这很正常，因为还没有 build。

### 2. 进入 src 并创建 package

进入源码目录：

```bash
cd ~/ros2_ws/src
```

创建第一个 Python 包：

```bash
ros2 pkg create --build-type ament_python my_first_pkg
```

中间第一次遇到报错：

```text
ros2: command not found
```

原因：当前终端没有重新加载 ROS 2 环境。

修复动作：

```bash
source /opt/ros/jazzy/setup.bash
```

然后重新执行创建 package 的命令，成功生成 `my_first_pkg`。

### 3. 回到工作空间根目录准备 build

切回工作空间根目录：

```bash
cd ~/ros2_ws
```

### 4. 第一次执行 colcon build

第一次运行：

```bash
colcon build
```

出现报错：

```text
Command 'colcon' not found
```

原因：构建工具还没有安装。

修复动作：

```bash
sudo apt install python3-colcon-common-extensions
```

安装完成后重新执行：

```bash
colcon build
```

成功输出：

```text
Starting >>> my_first_pkg
Finished <<< my_first_pkg
Summary: 1 package finished
```

### 5. 查看 build 后的工作空间结构

构建完成后，在 `~/ros2_ws` 里看到：

```bash
build  install  log  src
```

这说明：

- `src` 是源码区
- `build / install / log` 是 build 后自动生成的

### 6. 加载工作空间自己的环境

在工作空间根目录执行：

```bash
source install/setup.bash
```

这一步不是加载系统 ROS 2，而是加载“你这个工作空间 build 出来的结果”。

### 7. 用环境变量确认工作空间已加载

执行：

```bash
echo $AMENT_PREFIX_PATH
```

看到：

```text
/home/surunhui/ros2_ws/install/my_first_pkg:/opt/ros/jazzy
```

这说明当前终端已经同时认识：

- 系统里的 ROS 2：`/opt/ros/jazzy`
- 工作空间自己的结果：`/home/surunhui/ros2_ws/install/my_first_pkg`

## Day 2 小复盘

今天学了什么：

- `workspace` 是总工作目录
- `package` 是一个独立的小功能包
- `src` 用来放源码和 package
- `colcon build` 会根据 `src` 里的包开始构建
- 构建后通常会生成 `build / install / log`
- `source install/setup.bash` 是加载工作空间自己的环境

今天最重要的 3 个概念：

- `workspace`：总工地
- `package`：小功能盒子
- `colcon build`：开始施工的动作

今天最容易混淆的点：

- `src` 是手动先建的源码区
- `build / install / log` 往往是 `colcon build` 后自动生成的
- `source /opt/ros/jazzy/setup.bash` 和 `source install/setup.bash` 不是一回事

## 下一步计划

准备继续学习 Day 3：

- publisher 是什么
- subscriber 是什么
- topic 名字为什么重要
- 一个最小的 Python ROS 2 包怎么运行
- 第一次真正写自己的 ROS 2 Python 节点
