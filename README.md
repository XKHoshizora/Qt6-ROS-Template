# Qt6 ROS Template

[中文](README.md) | [English](README_en.md)

## 目录

- [项目简介](#项目简介)
- [功能特性](#功能特性)
- [系统要求](#系统要求)
- [安装指南](#安装指南)
- [项目设置](#项目设置)
- [运行项目](#运行项目)
- [项目结构](#项目结构)
- [自定义和扩展](#自定义和扩展)
- [常见问题](#常见问题)
- [贡献指南](#贡献指南)
- [版本历史](#版本历史)
- [许可证](#许可证)
- [联系方式](#联系方式)

## 项目简介

**Qt6 ROS Template** 是一个基于 Qt6 构建的 ROS Noetic 人机交互界面模板。本项目旨在为开发者提供一个快速入门的框架，方便用户在此基础上进行 ROS 人机交互界面的开发。它融合了 Qt6 的现代化 UI 设计能力和 ROS 的强大机器人开发生态，为机器人应用的图形界面开发提供了一个理想的起点。

本项目的开发灵感来自于 Qt5 版本的 [ros_qt_demo](https://github.com/XKHoshizora/ros_qt_demo) 项目。然而，与 Qt5 版本相比，本项目进行了重大改进：

1. **双重编译支持**：本模板不仅支持在 ROS 环境下使用 `catkin_make` 进行编译，还可以直接在 Qt Creator 中打开和编译，无需复杂的配置步骤。

2. **简化开发流程**：相比 Qt5 版本需要各种配置才能在 Qt Creator 中进行开发，本项目实现了"开箱即用"的体验，大大简化了开发流程。

3. **增强的灵活性**：开发者可以根据自己的偏好选择使用 ROS 工具链或 Qt Creator 进行开发，提供了更大的灵活性。

## 功能特性

- 集成 Qt6 和 ROS Noetic，提供现代化的 UI 设计和强大的机器人开发能力
- 双重编译支持：兼容 ROS 的 `catkin_make` 和 Qt Creator 的构建系统
  - 可以在只有 ROS 的环境下使用 `catkin_make` 进行编译
  - 可以在只有 Qt6 的环境下使用 Qt Creator 编译并打开项目
  - 可以在 ROS 和 Qt6 环境下同时使用 `catkin_make` 或 Qt Creator 对项目进行编译
- 无需复杂配置，可直接在 Qt Creator 中打开项目进行开发
- 预配置的 CMakeLists.txt，简化了 Qt 和 ROS 的集成过程
- 包含基本的 ROS 节点和 Qt 主窗口实现，可作为开发起点
- 提供了 ROS launch 文件，方便启动和管理节点
- 支持在 ROS 和非 ROS 环境下编译运行，增强了项目的灵活性
- 相比 Qt5 版本，大大简化了开发流程，提高了开发效率

## 系统要求

- 操作系统：Ubuntu 20.04 LTS
- ROS 版本：Noetic
- Qt 版本：6.x
- CMake 版本：3.16 或更高

## 安装指南

### 安装 ROS Noetic

有两种方法可以安装 ROS Noetic：

1. 根据[官方指南](https://wiki.ros.org/noetic/Installation/Ubuntu)进行安装

2. 使用 Auto ROS Installer（推荐）：
   ```bash
   git clone https://github.com/XKHoshizora/auto-ros-installer.git
   cd auto-ros-installer
   ```
   详细安装方法请查看[项目主页](https://github.com/XKHoshizora/auto-ros-installer)的说明。

### 安装 Qt6

推荐使用 Qt 官方安装器安装 Qt6：

1. 下载 Qt Installer：
   访问 [Qt 官方下载页面](https://www.qt.io/download-qt-installer)，下载适用于 Linux 的在线安装程序。

2. 授予执行权限：

   ```bash
   chmod +x qt-online-installer-linux-<x64/arm64>-<version>.run
   ```

3. 运行安装程序：

   ```bash
   ./qt-online-installer-linux-<x64/arm64>-<version>.run
   ```

4. 配置 Qt Creator 快捷方式：
   使用以下命令创建并打开 `qtcreator` 文件

   ```bash
   sudo nano /usr/bin/qtcreator
   ```

   向 `qtcreator` 文件中添加以下内容：

   ```shell
   #!/bin/sh

   export QT_HOME=/home/<user>/Qt/Tools/QtCreator/bin
   $QT_HOME/qtcreator $*
   ```

5. 为 `qtcreator` 文件添加可执行权限：

   ```bash
   sudo chmod a+x /usr/bin/
   ```

6. 启动 Qt Creator：

   ```bash
   qtcreator
   ```

7. 安装其他依赖

   如果在运行 Qt Creator 时遇到问题，请安装以下依赖：

   ```bash
   sudo apt install libxcb-xinerama0 libxcb-xinerama0-dev libxcb-cursor0
   ```

## 项目设置

### 创建工作空间

```bash
mkdir -p ~/qt6_ws/src
cd ~/qt6_ws/src
```

### 克隆项目

```bash
git clone https://github.com/XKHoshizora/qt6_ros_template.git
```

### 构建项目

#### 单独的 ROS 环境中

在你的工作空间内执行以下命令即可编译该功能包：

```bash
cd ~/qt6_ws
catkin_make
```

#### 在单独的 Qt6 环境中

1. 打开 Qt Creator
2. 选择 "File" > "Open File or Project"
3. 导航到 `~/qt6_ws/src/qt6_ros_template` 目录中，选择 `CMakeLists.txt` 文件并打开
4. 配置并打开项目，左侧可以正常显示项目文件，即说明编译成功。若编译失败，则只会显示一个 `CMakeLists.txt` 文件。

#### 在 ROS 和 Qt6 共存的环境中

1. 在你的工作空间内执行以下命令即可编译该功能包：

   ```bash
   cd ~/qt6_ws
   catkin_make
   ```

2. 需要在 Qt Creator 中打开项目进行开发时，首先要通过第一步的编译。接着按照以下步骤进行操作：
   1. 打开 Qt Creator
   2. 选择 "File" > "Open File or Project"
   3. 导航到 `~/qt6_ws/src` 并选择 `CMakeLists.txt` 文件(**注意，是选择工作空间下的 `CMakeLists.txt` 文件，而不是功能包内的文件**)
   4. 进入到配置页面后，点击 `Import Build From...` 选项右侧的 `Details` 按钮。点击 `Browse...` 按钮找到 `qt_ws/build` 目录并点击右上角的 `Open` 按钮打开。点击 `Import` 按钮完成导入。
   5. 勾选 `Imported Kit` 和 `Build` 选项，并去掉除此之外的所有选项。
   6. 点击右下角的 `Configure Project` 按钮完成配置并开始编项目。
   7. 左侧可以正常显示项目文件，即说明编译成功。若编译失败，则只会显示一个 `CMakeLists.txt` 文件。

## 项目测试

### 运行项目

#### 单独的 ROS 环境中

首先确保已经根据上面的步骤完成了编译。然后在工作空间下执行以下命令：

```bash
source ~/qt6_ws/devel/setup.bash
roslaunch qt6_ros_template demo.launch

# 如果您想指定不同的 ROS_HOSTNAME 或 ROS_IP，可以这样使用：
roslaunch qt6_ros_template demo.launch ros_hostname:=your_hostname ros_ip:=your_ip
```

#### 在单独的 Qt6 环境中

通过 Qt Creator 编译并打开项目后，点击左侧绿色的 `Run` 按钮，或使用 `Ctrl + R` 快捷键运行。

#### 在 ROS 和 Qt6 共存的环境中

首先确保已经根据上面的步骤完成了编译。然后在工作空间下执行以下命令：

```bash
source ~/qt6_ws/devel/setup.bash
roslaunch qt6_ros_template demo.launch

# 如果您想指定不同的 ROS_HOSTNAME 或 ROS_IP，可以这样使用：
roslaunch qt6_ros_template demo.launch ros_hostname:=your_hostname ros_ip:=your_ip
```

或通过 Qt Creator 编译并打开项目后，点击左侧绿色的 `Run` 按钮，或使用 `Ctrl + R` 快捷键运行。

### 功能测试

测试时推荐使用 `rosrun` 命令进行测试，此时需要提前在新的终端使用 `roscore` 命令运行 `ros master`，然后在另一个新的终端输入以下命令来启动 ROS 节点：

```bash
rosrun qt6_ros_template qt6_ros_template_node
```

节点成功运行之后，按照以下步骤测试应用程序的各项功能：

1. **连接到 ROS**

   - 点击应用程序中的"Connect"按钮。
   - 验证"ROS Status"标签是否变为绿色并显示"Connected"。

2. **更改话题**

   - 在"Change Topic"输入框中输入新的话题名称（例如"/test_topic"）。
   - 点击"Change Topic"按钮。

3. **发布消息**

   - 在"Publish"输入框中输入一条消息。
   - 点击"Publish"按钮。
   - 在新终端中使用以下命令验证已发布的消息：
     ```
     rostopic echo /test_topic
     ```

4. **订阅消息**

   - 在新终端中，向已订阅的话题发布一条消息：
     ```
     rostopic pub /test_topic std_msgs/String "data: '来自命令行的问候'" -1
     ```
   - 验证消息是否出现在应用程序的日志视图中。

5. **测试断开连接**

   - 点击"Disconnect"按钮。
   - 验证"ROS 状态"标签是否变为红色并显示"Disconnected"。
   - 尝试发布消息并验证是否失败。

6. **测试 ROS Master 故障**

   - 使用应用程序连接到 ROS。
   - 在运行 roscore 的终端中，使用 Ctrl+C 停止它。
   - 观察应用程序的日志视图和控制台输出是否有断开连接的消息。

7. **环境变量使用**

   - 勾选"Use environment variables"复选框。
   - 验证主 URL 和 ROS IP 字段是否从环境变量中填充。

8. **设置的保存和加载**
   - 在应用程序中更改一些设置。
   - 关闭应用程序并重新打开。
   - 验证设置是否正确恢复。

### 故障排除

如果遇到任何问题：

1. 确保在启动应用程序之前运行 `roscore`。
2. 检查您的 ROS 环境变量（`ROS_MASTER_URI` 和 `ROS_IP`）是否正确设置。
3. 如果在多台机器上运行 ROS，请验证网络连接。
4. 检查控制台输出和应用程序日志中是否有任何错误消息。

## 项目结构

本项目使用了标准的 CMake 构建系统，并遵循了 Qt 项目的目录结构。

```
qt6_ros_template/
├── CMakeLists.txt
├── package.xml
├── include/
│   ├── qt6_ros_template/
│   └── mainwindow.h
├── msg/
├── resources/
│   ├── images/
│   │   └── icon.png
│   └── resource.qrc
├── scripts/
├── src/
│   ├── main.cpp
│   ├── mainwindow.cpp
│   └── qt6_ros_template_node.cpp
├── srv/
├── ui/
│   └── mainwindow.ui
└── launch/
    └── demo.launch
```

## 自定义和扩展

1. 修改 `src/mainwindow.cpp` 和 `ui/mainwindow.ui` 以自定义 UI。
2. 在 `src/qt6_ros_template_node.cpp` 中添加 ROS 功能。
3. 更新 `CMakeLists.txt` 以包含新的源文件或依赖项。

## 常见问题

1. **问题**：编译时出现 "Qt6 not found" 错误。
   **解决方案**：确保 Qt6 正确安装，并且 CMAKE_PREFIX_PATH 包含 Qt6 安装路径。

2. **问题**：ROS 相关的函数未定义。
   **解决方案**：确保已 source devel/setup.bash，并且 package.xml 中包含所有必要的依赖。

3. **问题**：在 Qt Creator 中无法找到 ROS 头文件。
   **解决方案**：在 Qt Creator 的项目设置中，添加 ROS 的 include 路径（通常在 /opt/ros/noetic/include）。

## 贡献指南

我们欢迎并感谢任何形式的贡献！如果您想为项目做出贡献，请遵循以下步骤：

1. Fork 本仓库
2. 创建您的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交您的更改 (`git commit -m 'Add some AmazingFeature'`)
4. 将您的更改推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建一个新的 Pull Request

## 版本历史

- 0.1.0
  - 初始版本
  - 基本的 Qt6 和 ROS Noetic 集成
  - 实现了双重编译支持（ROS 环境和 Qt Creator）

## 许可证

本项目基于 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 联系方式

项目维护者：XKHoshizora - hoshizoranihon@gmail.com

项目链接：[https://github.com/XKHoshizora/qt6_ros_template](https://github.com/XKHoshizora/qt6_ros_template)

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=XKHoshizora/qt6_ros_template&type=Date)](https://star-history.com/#XKHoshizora/qt6_ros_template&Date)
