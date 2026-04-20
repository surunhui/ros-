# ROS 2 学习记录

这个仓库用来保存我和 ChatGPT/Codex 学习 ROS 2 的关键步骤、通俗解释和每天的学习记录，方便在电脑和手机上随时查看。

## 学习约定

从现在开始，默认执行下面这条规则：

- 每天学习结束后，都要把当天的重要步骤、关键概念、复盘内容同步更新到 GitHub

同步时默认会做这两件事：

- 更新 `README.md` 里的学习进度
- 新增或更新当天的学习记录文件，比如 `Day1.md`、`Day2.md`、`Day3.md`

## 当前学习进度

已完成：

- Day 1：认识 ROS 2、node、topic、message
- Day 2：认识 workspace、package、src / build / install / log、colcon build、source
- Windows 11 上安装并配置 WSL2
- 安装 Ubuntu 24.04 LTS
- 安装 ROS 2 Jazzy
- 跑通第一个 ROS 2 示例 `talker`
- 创建第一个 ROS 2 Python package `my_first_pkg`
- 完成第一次 `colcon build`

## 最重要的两句话

- `node` 通过 `topic` 传递 `message`
- `先把 package 放进 src，再用 colcon build 生成 build / install / log，最后 source install/setup.bash。`

## 当前文件结构

- [Day1.md](https://github.com/surunhui/ros-/blob/main/Day1.md): Day 1 详细学习记录
- [Day2.md](https://github.com/surunhui/ros-/blob/main/Day2.md): Day 2 详细学习记录

## 当前环境结论

已经完成：

- `WSL2 + Ubuntu 24.04`
- `ROS 2 Jazzy`
- `ros2` 命令可正常使用
- `talker` 示例可正常运行
- `ros2_ws` 工作空间已创建
- `my_first_pkg` package 已创建并成功 build

## 下一步计划

准备继续学习 Day 3：

- publisher 是什么
- subscriber 是什么
- topic 名字为什么重要
- 一个最小的 Python ROS 2 包怎么运行
- 第一次真正写自己的 ROS 2 Python 节点
