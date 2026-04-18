# ROS 2 学习记录

这个仓库用来保存我和 ChatGPT/Codex 学习 ROS 2 的关键步骤、通俗解释和每天的学习记录，方便在电脑和手机上随时查看。

## 当前学习进度

已完成：

- Day 1：认识 ROS 2、node、topic、message
- Windows 11 上安装并配置 WSL2
- 安装 Ubuntu 24.04 LTS
- 安装 ROS 2 Jazzy
- 跑通第一个 ROS 2 示例 `talker`
- 用 `node list`、`topic list`、`topic echo` 观察系统

## 最重要的一句话

`node` 通过 `topic` 传递 `message`

## 当前文件结构

- [Day1.md](https://github.com/surunhui/ros-/blob/main/Day1.md): Day 1 详细学习记录

## Day 1 你应该记住什么

- `ROS 2`：机器人里很多小程序协作时用的规则系统
- `node`：一个独立干活的小程序
- `topic`：传递消息的频道
- `message`：频道里真正传递的内容

## 当前环境结论

已经完成：

- `WSL2 + Ubuntu 24.04`
- `ROS 2 Jazzy`
- `ros2` 命令可正常使用
- `talker` 示例可正常运行

## 下一步计划

准备继续学习 Day 2：

- workspace 是什么
- package 是什么
- `src / build / install / log` 是什么
- `colcon build` 是什么
- `source` 在工作空间里又是什么意思
