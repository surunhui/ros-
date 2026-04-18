# Day 1 学习记录

## 今天的目标

认识 ROS 2 最基础的世界：

- ROS 2 是什么
- node 是什么
- topic 是什么
- message 是什么
- 跑通最简单的 ROS 2 示例

## 最重要的一句话

`node` 通过 `topic` 传递 `message`

## 通俗理解

### ROS 2 是什么

最通俗地说，ROS 2 就像“机器人里很多小程序一起协作时使用的规则系统”。

### node 是什么

最通俗地说，`node` 就像一个独立干活的小工人。

### topic 是什么

最通俗地说，`topic` 就像一个公开广播频道。

### message 是什么

最通俗地说，`message` 就是频道里真正传递的内容。

## 这次走过的关键步骤

### 1. 选择环境路线

最终选择：

- `WSL2 + Ubuntu 24.04`

原因：更适合后续 ROS 2 和机器人项目学习。

### 2. 安装 WSL2

解决了 `wsl --install` 的报错问题，最终启用了关键组件：

- `VirtualMachinePlatform`
- `Microsoft-Windows-Subsystem-Linux`

中间进行了两次重启，让系统功能生效。

### 3. 安装 Ubuntu 24.04

默认安装发行版时，网络响应异常，后来改用：

```bash
wsl --install Ubuntu-24.04 --web-download
```

成功安装 Ubuntu 24.04。

### 4. 初始化 Ubuntu

完成了这些动作：

- 创建 Ubuntu 默认用户
- 设置密码
- 进入 Ubuntu 终端
- 从 Windows 映射目录切回 Ubuntu 家目录

常用命令：

```bash
pwd
cd ~
lsb_release -a
```

确认结果：

- Ubuntu 版本：`24.04.4 LTS`
- 代号：`noble`

### 5. 准备 ROS 2 软件源

更新软件列表：

```bash
sudo apt update
```

安装仓库工具并启用 `universe`：

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

安装下载和密钥工具：

```bash
sudo apt install curl gnupg2
```

导入 ROS 官方密钥：

```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

添加 ROS 2 官方软件源：

```bash
echo "deb [signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu noble main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

再次刷新软件列表，确认系统已经识别 `packages.ros.org`：

```bash
sudo apt update
```

### 6. 安装 ROS 2 Jazzy

安装基础版本：

```bash
sudo apt install ros-jazzy-ros-base
```

加载环境：

```bash
source /opt/ros/jazzy/setup.bash
```

验证命令：

```bash
ros2 --help
```

结论：`ros2` 可以正常使用。

### 7. 安装示例包

一开始运行示例时提示：

```text
Package 'demo_nodes_cpp' not found
```

所以补装：

```bash
sudo apt install ros-jazzy-demo-nodes-cpp
```

### 8. 运行第一个 ROS 2 示例

运行：

```bash
ros2 run demo_nodes_cpp talker
```

看到持续输出：

```text
Publishing: 'Hello World: 1'
Publishing: 'Hello World: 2'
```

说明 `talker` 节点已经跑起来了。

### 9. 在第二个终端里观察系统

打开第二个 Ubuntu 终端后，要重新加载环境：

```bash
source /opt/ros/jazzy/setup.bash
```

查看节点：

```bash
ros2 node list
```

结果：

```text
/talker
```

查看 topic：

```bash
ros2 topic list
```

结果：

```text
/chatter
/parameter_events
/rosout
```

监听 `/chatter`：

```bash
ros2 topic echo /chatter
```

结果：

```text
data: 'Hello World: 707'
data: 'Hello World: 708'
```

这一步把三个概念连起来了：

- `/talker` 是 `node`
- `/chatter` 是 `topic`
- `Hello World: 707` 是 `message`

## Day 1 小复盘

今天学了什么：

- ROS 2 最基础概念
- WSL2 与 Ubuntu 的基础使用
- ROS 2 Jazzy 的安装
- `talker` 节点的运行
- 用命令观察 node、topic、message

今天最重要的 3 个概念：

- `node`：干活的小程序
- `topic`：传话的频道
- `message`：频道里真正传递的内容

今天最容易混淆的点：

- 安装好 ROS 2，不等于新终端自动可用
- 新开终端后，通常还要重新执行：

```bash
source /opt/ros/jazzy/setup.bash
```

## 下一步计划

准备继续学习 Day 2：

- workspace 是什么
- package 是什么
- `src / build / install / log` 是什么
- `colcon build` 是什么
- `source` 在工作空间里又是什么意思
