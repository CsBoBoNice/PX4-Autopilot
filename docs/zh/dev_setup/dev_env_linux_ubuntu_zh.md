# Ubuntu 开发环境

以下说明使用一个 bash 脚本来在 PX4 支持的 [Ubuntu Linux LTS](https://wiki.ubuntu.com/LTS) 版本上设置 PX4 开发环境：Ubuntu 24.04 (Nimble Numbat) 和 Ubuntu 22.04 (Jammy Jellyfish)。

该环境包括：

- [Gazebo 模拟器](../sim_gazebo_gz/index.md) ("Harmonic")
- [用于 Pixhawk（和其他基于 NuttX 的硬件）的构建工具链](../dev_setup/building_px4.md#nuttx-pixhawk-based-boards)。

在 Ubuntu 22.04 上：

- 可以使用 [Gazebo Classic 模拟器](../sim_gazebo_classic/index.md) 替代 Gazebo。
  Gazebo 在 PX4 上正接近与 Gazebo-Classic 的功能对等，并将很快取代它用于所有用例。

其他飞控、模拟器以及与 ROS 协作的构建工具链在下面的 [其他目标](#other-targets) 部分中讨论。

::: details 我可以使用旧版本的 Ubuntu 吗？
PX4 在可能的情况下支持当前和上一个 Ubuntu LTS 版本。
不支持旧版本（因此您不能针对它们提出缺陷），但可能仍然有效。
例如，Gazebo Classic 设置包含在我们针对 macOS、Ubuntu 18.04 和 20.04 以及基于 WSL2 的 Windows 的标准构建说明中。
:::

## 模拟和 NuttX (Pixhawk) 目标

使用 [ubuntu.sh](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/setup/ubuntu.sh) 脚本来设置一个开发环境，允许您为模拟器和/或 [NuttX/Pixhawk](../dev_setup/building_px4.md#nuttx-pixhawk-based-boards) 工具链进行构建。

:::tip
该脚本旨在在 _干净_ 的 Ubuntu LTS 安装上运行，如果在现有系统"之上"运行或在不同的 Ubuntu 版本上运行，可能无法工作。
:::

安装工具链：

1. [下载 PX4 源代码](../dev_setup/building_px4.md)：

   ```sh
   git clone https://github.com/PX4/PX4-Autopilot.git --recursive
   ```

   ::: info
   源代码中的环境设置脚本通常适用于最近的 PX4 版本。
   如果使用旧版本的 PX4，您可能需要 [获取特定于您版本的源代码](../contribute/git_examples.md#get-a-specific-release)。
   :::

2. 运行 **ubuntu.sh** 脚本（在 bash shell 中）不带任何参数以安装所有内容：

   ```sh
   bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
   ```

   - 在脚本进行过程中确认任何提示。
   - 您可以使用 `--no-nuttx` 和 `--no-sim-tools` 选项来省略 NuttX 和/或模拟工具。

3. 如果您需要 Gazebo Classic（仅限 Ubuntu 22.04），则可以手动移除 Gazebo 并通过遵循 [Gazebo Classic > 安装](../sim_gazebo_classic/index.md#installation) 中的说明来安装它。

4. 完成后重启计算机。

:::details 附加说明
这些说明仅"供参考"：

- 此设置由 PX4 开发团队支持。
  这些说明也可能适用于其他基于 Debian Linux 的系统。
- 您可以通过确认 `gcc` 版本来验证 NuttX 安装，如下所示：

  ```sh
  $arm-none-eabi-gcc --version

  arm-none-eabi-gcc (15:13.2.rel1-2) 13.2.1 20231009
  Copyright (C) 2023 Free Software Foundation, Inc.
  This is free software; see the source for copying conditions.  There is NO
  warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
  ```

- 您无论如何都需要 PX4 源代码。
  但如果您只想设置开发环境而不获取所有源代码，您可以改为下载 [ubuntu.sh](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/setup/ubuntu.sh) 和 [requirements.txt](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/setup/requirements.txt)，然后运行 **ubuntu.sh**：

  ```sh
  wget https://raw.githubusercontent.com/PX4/PX4-Autopilot/main/Tools/setup/ubuntu.sh
  wget https://raw.githubusercontent.com/PX4/PX4-Autopilot/main/Tools/setup/requirements.txt
  bash ubuntu.sh
  ```

  :::

## 其他目标

Ubuntu 开发环境用于 ROS、其他模拟器和其他硬件目标的内容在其各自的文档中有所涵盖。
下面链接了相关主题的一个子集。

树莓派

- [树莓派 2/3 Navio2 自动驾驶仪 > PX4 开发环境](../flight_controller/raspberry_pi_navio2.md#px4-development-environment)
- [树莓派 2/3/4 PilotPi 盾](../flight_controller/raspberry_pi_pilotpi.md)。

ROS

- ROS 2: [ROS 2 用户指南 > 安装与设置](../ros2/user_guide.md#installation-setup)。
- ROS (1): [ROS (1) 安装指南](../ros/mavros_installation.md)

## 下一步

完成命令行工具链设置后：

- 安装 [VSCode](../dev_setup/vscode.md)（如果您更喜欢使用 IDE 而不是命令行）。
- 安装 [QGroundControl 每日构建版](../dev_setup/qgc_daily_build.md)

  :::tip
  _每日构建版_ 包含在发布构建中隐藏的开发工具。
  它也可能提供对尚未在发布构建中支持的新 PX4 功能的访问。
  :::

- 继续阅读 [构建说明](../dev_setup/building_px4.md)。