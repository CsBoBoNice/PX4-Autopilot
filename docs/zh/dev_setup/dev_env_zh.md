# 设置开发环境（工具链）

PX4 开发的 _支持平台_ 有：

- [Ubuntu Linux (22.04/20.04/18.04)](../dev_setup/dev_env_linux_ubuntu.md) — 推荐
- [Windows (10/11)](../dev_setup/dev_env_windows_wsl.md) — 通过 WSL2
- [Mac OS](../dev_setup/dev_env_mac.md)

## 支持的目标

下表显示了您可以在每个操作系统上构建的 PX4 目标。

| 目标                                                                                                                                 | Linux (Ubuntu) | Mac | Windows |
| -------------------------------------------------------------------------------------------------------------------------------------- | :------------: | :-: | :-----: |
| **基于 NuttX 的硬件:** [Pixhawk 系列](../flight_controller/pixhawk_series.md), [Crazyflie](../complete_vehicles_mc/crazyflie2.md) |       ✓        |  ✓  |    ✓    |
| **基于 Linux 的硬件:** [树莓派 2/3](../flight_controller/raspberry_pi_navio2.md)                                              |       ✓        |     |         |
| **模拟:** [Gazebo SITL](../sim_gazebo_gz/index.md)                                                                               |       ✓        |  ✓  |    ✓    |
| **模拟:** [Gazebo Classic SITL](../sim_gazebo_classic/index.md)                                                                  |       ✓        |  ✓  |    ✓    |
| **模拟:** [带 Gazebo Classic 的 ROS](../simulation/ros_interface.md)                                                              |       ✓        |     |    ✓    |
| **模拟:** 带 Gazebo 的 ROS 2                                                                                                      |       ✓        |     |    ✓    |

有经验的 Docker 用户也可以使用我们的持续集成系统使用的容器进行构建：[Docker 容器](../test_and_ci/docker.md)

## 下一步

完成上述命令行工具链之一的设置后：

- 安装 [VSCode](../dev_setup/vscode.md)（如果您更喜欢使用 IDE 而不是命令行）。
- 安装 [QGroundControl 每日构建版](../dev_setup/qgc_daily_build.md)
- 继续阅读 [构建 PX4 软件](../dev_setup/building_px4.md)。