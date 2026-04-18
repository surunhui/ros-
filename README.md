# ROS 2 学习记录

这个仓库当前主要用来保存我和 ChatGPT/Codex 学习 ROS 2 的关键步骤与结论，方便在电脑和手机上随时查看。

## 当前学习进度

已完成 Day 1 的核心内容：

- 认识 ROS 2、node、topic、message 的最基础概念
- 在 Windows 11 上安装并配置 WSL2
- 安装 Ubuntu 24.04 LTS
- 在 Ubuntu 24.04 中安装 ROS 2 Jazzy
- 运行 ROS 2 最简单示例 `talker`
- 用命令查看 node 和 topic
- 用 `topic echo` 看到真正的 message 内容

## 最重要的一句话

`node` 通过 `topic` 传递 `message`

## 关键概念

### 1. ROS 2 是什么

最通俗地说，ROS 2 可以理解成“机器人里很多小程序一起合作时使用的规则系统”。

### 2. node 是什么

最通俗地说，`node` 就像一个独立干活的小工人。

### 3. topic 是什么

最通俗地说，`topic` 就像一个公开广播频道。

### 4. message 是什么

最通俗地说，`message` 就是频道里真正传递的内容。

## 这次安装与学习里的关键步骤

### 第 1 步：确认 Windows 路线

最终选择了：

- `WSL2 + Ubuntu 24.04`

原因：这条路线更适合后续学习 ROS 2 和机器人项目。

### 第 2 步：安装 WSL2

先解决了 `wsl --install` 的报错问题，后来使用了不依赖默认商店通道的方式完成安装，并启用了这些关键组件：

- `VirtualMachinePlatform`
- `Microsoft-Windows-Subsystem-Linux`

中间做了两次重启，让系统功能真正生效。

### 第 3 步：安装 Ubuntu 24.04

安装 `Ubuntu-24.04` 时，默认下载方式出现网络响应异常，后来改用：

```bash
wsl --install Ubuntu-24.04 --web-download
```

这样成功完成了安装。

### 第 4 步：初始化 Ubuntu

完成了以下动作：

- 创建默认 Ubuntu 用户
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

### 第 5 步：准备 ROS 2 软件源

先更新系统软件列表：

```bash
sudo apt update
```

然后安装仓库工具并启用 `universe`：

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

再安装下载与密钥工具：

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

### 第 6 步：安装 ROS 2 Jazzy

安装基础版本：

```bash
sudo apt install ros-jazzy-ros-base
```

然后在当前终端加载 ROS 2 环境：

```bash
source /opt/ros/jazzy/setup.bash
```

验证命令：

```bash
ros2 --help
```

结论：`ros2` 命令可以正常使用。

### 第 7 步：安装示例包

因为一开始运行示例时提示：

```text
Package 'demo_nodes_cpp' not found
```

所以补装了示例包：

```bash
sudo apt install ros-jazzy-demo-nodes-cpp
```

### 第 8 步：运行第一个 ROS 2 示例

运行 talker：

```bash
ros2 run demo_nodes_cpp talker
```

看到持续输出：

```text
Publishing: 'Hello World: 1'
Publishing: 'Hello World: 2'
```

这说明 `talker` 节点已经真正跑起来了。

### 第 9 步：在第二个终端观察系统状态

打开第二个 Ubuntu 终端后，需要重新加载环境：

```bash
source /opt/ros/jazzy/setup.bash
```

查看当前节点：

```bash
ros2 node list
```

结果看到：

```text
/talker
```

查看当前 topic：

```bash
ros2 topic list
```

结果看到：

```text
/chatter
/parameter_events
/rosout
```

监听 `/chatter`：

```bash
ros2 topic echo /chatter
```

结果看到：

```text
data: 'Hello World: 707'
data: 'Hello World: 708'
```

这一步把 3 个概念真正连起来了：

- `/talker` 是 `node`
- `/chatter` 是 `topic`
- `Hello World: 707` 是 `message`

## Day 1 小复盘

今天学会了：

- ROS 2 最基础概念
- WSL2 与 Ubuntu 的基础使用
- ROS 2 Jazzy 的安装
- `talker` 节点的运行
- 用命令观察 node、topic、message

今天最重要的 3 个概念：

- `node`：干活的小程序
- `topic`：传话的频道
- `message`：频道里真正传的内容

今天最容易混淆的点：

- 安装好 ROS 2，不等于新终端自动可用
- 新开终端后，通常还要重新执行：

```bash
source /opt/ros/jazzy/setup.bash
```

## 下一步计划

后续准备继续学习 Day 2：

- workspace 是什么
- package 是什么
- `src / build / install / log` 是什么
- `colcon build` 是什么
- `source` 在工作空间里又是什么意思
