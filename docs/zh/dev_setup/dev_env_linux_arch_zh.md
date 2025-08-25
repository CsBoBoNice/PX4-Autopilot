# Arch Linux 开发环境

:::warning
此开发环境是 [社区支持和维护的](../advanced/community_supported_dev_env)。
它可能适用于也可能不适用于当前版本的 PX4。

有关核心开发团队支持的环境和工具的信息，请参见 [工具链安装](../dev_setup/dev_env.md)。
:::

PX4-Autopilot 仓库提供了一个方便的脚本来设置您的 Arch 安装以进行 PX4 开发：[Tools/setup/arch.sh](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/setup/arch.sh)。 <!-- NEED px4_version -->

该脚本默认安装所有用于为 NuttX 目标构建 PX4 和使用 [JMAVSim](../sim_jmavsim/index.md) 运行模拟的工具。
您可以通过指定命令行参数 `--gazebo` 来额外安装 [Gazebo Classic](../sim_gazebo_classic/index.md) 模拟器。

![Gazebo on Arch](../../assets/simulation/gazebo_classic/arch-gazebo.png)

::: info
这些说明已在 [Manjaro](https://manjaro.org/)（基于 Arch 的发行版）上进行了测试，因为它比 Arch Linux 更容易设置。
:::

要获取并运行脚本，请执行以下任一操作：

- [下载 PX4 源代码](../dev_setup/building_px4.md) 并在原地运行脚本：

  ```sh
  git clone https://github.com/PX4/PX4-Autopilot.git
  bash PX4-Autopilot/Tools/setup/arch.sh
  ```

- 仅下载所需的脚本，然后运行它们：

  ```sh
  wget https://raw.githubusercontent.com/PX4/PX4-Autopilot/main/Tools/setup/arch.sh
  wget https://raw.githubusercontent.com/PX4/PX4-Autopilot/main/Tools/setup/requirements.txt
  bash arch.sh
  ```

该脚本接受以下可选参数：

- `--gazebo`：添加此参数以从 [AUR](https://aur.archlinux.org/packages/gazebo/) 安装 Gazebo。

  ::: info
  Gazebo 从源代码编译。
  安装需要一些时间，并且需要多次输入 `sudo` 密码（用于依赖项）。
  :::

- `--no-nuttx`：不安装 NuttX/Pixhawk 工具链（即，如果仅使用模拟）。
- `--no-sim-tools`：不安装 jMAVSim/Gazebo（即，如果仅针对 Pixhawk/NuttX 目标）