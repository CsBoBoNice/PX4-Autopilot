# 飞行控制器移植指南

本主题适用于想要将 PX4 移植到新飞行控制器硬件上的开发者。

## PX4 架构

PX4 由两个主要层组成：主机操作系统（NuttX、Linux 或任何其他 POSIX 平台如 Mac OS）之上的[板载支持和中间件层](../middleware/index.md)，以及应用程序（[src/modules](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules) 中的飞行栈）。请参考 [PX4 架构概述](../concept/architecture.md) 了解更多信息。

本指南仅专注于主机操作系统和中间件，因为应用程序/飞行栈将在任何板载目标上运行。

## 飞行控制器配置文件布局

板载启动和配置文件位于 [/boards](https://github.com/PX4/PX4-Autopilot/tree/main/boards/) 下的每个板载的供应商特定目录中（即 **boards/_VENDOR_/_MODEL_/**）。

例如，对于 FMUv5：

- （所有）板载特定文件：[/boards/px4/fmu-v5](https://github.com/PX4/PX4-Autopilot/tree/main/boards/px4/fmu-v5)。<!-- NEED px4_version -->
- 构建配置：[/boards/px4/fmu-v5/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/default.px4board)。<!-- NEED px4_version -->
- 板载特定初始化文件：[/boards/px4/fmu-v5/init/rc.board_defaults](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/init/rc.board_defaults) <!-- NEED px4_version -->
  - 如果在 boards 目录下的 **init/rc.board** 处找到板载特定初始化文件，它会自动包含在启动脚本中。
  - 该文件用于启动仅存在于特定板载上的传感器（和其他组件）。
    它也可以用于设置板载的默认参数、UART 映射和任何其他特殊情况。
  - 对于 FMUv5，您可以看到所有 Pixhawk 4 传感器都在启动，它还设置了更大的 LOGGER_BUF。

## 主机操作系统配置

本节描述了将每个受支持的主机操作系统移植到新飞行控制器硬件所需的配置文件的目的和位置。

### NuttX

请参见 [NuttX 板载移植指南](porting_guide_nuttx.md)。

### Linux

Linux 板载不包括操作系统和内核配置。
这些已经由板载可用的 Linux 镜像提供（需要开箱即用地支持惯性传感器）。

- [boards/px4/raspberrypi/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/raspberrypi/default.px4board) - RPi 交叉编译。<!-- NEED px4_version -->

## 中间件组件和配置

本节描述了各种中间件组件，以及将它们移植到新飞行控制器硬件所需的配置文件更新。

### QuRT / Hexagon

- 启动脚本位于 [posix-configs/](https://github.com/PX4/PX4-Autopilot/tree/main/posix-configs)。<!-- NEED px4_version -->
- 操作系统配置是默认 Linux 镜像的一部分（TODO：提供 LINUX IMAGE 的位置和烧录说明）。
- PX4 中间件配置位于 [src/boards](https://github.com/PX4/PX4-Autopilot/tree/main/boards)。<!-- NEED px4_version --> TODO: ADD BUS CONFIG

## RC UART 线路连接建议

通常建议通过单独的 RX 和 TX 引脚将 RC 连接到微控制器。
但是，如果 RX 和 TX 连接在一起，则必须将 UART 置于单线模式以防止任何争用。
这通过板载配置和清单文件完成。
一个例子是 [px4fmu-v5](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/src/manifest.c)。<!-- NEED px4_version -->

## 官方支持的硬件

PX4 项目支持并维护 [FMU 标准参考硬件](../hardware/reference_design.md) 以及与标准兼容的任何板载。
这包括 [Pixhawk 系列](../flight_controller/pixhawk_series.md)（参见用户指南了解[官方支持硬件的完整列表](../flight_controller/index.md)）。

每个官方支持的板载都受益于：

- PX4 存储库中可用的 PX4 端口
- 可从 _QGroundControl_ 访问的自动固件构建
- 与生态系统其余部分的兼容性
- 通过 CI 的自动检查 - 安全对于这个社区来说仍然是至关重要的
- [飞行测试](../test_and_ci/test_flights.md)

我们鼓励板载制造商争取与 [FMU 规范](https://pixhawk.org/) 完全兼容。
通过完全兼容，您可以受益于 PX4 正在进行的日常开发，但没有来自支持规范偏差的维护成本。

:::tip
制造商在偏离规范之前应仔细考虑维护成本（制造商的成本与偏差程度成正比）。
:::

我们欢迎任何个人或公司提交他们的端口以包含在我们支持的硬件中，前提是他们愿意遵循我们的[行为准则](https://github.com/PX4/PX4-Autopilot/blob/main/CODE_OF_CONDUCT.md)并与开发团队合作为他们的客户提供安全和令人满意的 PX4 体验。

同样重要的是要注意，PX4 开发团队有责任发布安全软件，因此我们要求任何板载制造商承诺必要的资源来保持其端口最新并处于工作状态。

如果您希望在 PX4 中获得官方支持：

- 您的硬件必须在市场上可用（即任何开发者都可以无限制地购买）。
- 硬件必须提供给 PX4 开发团队，以便他们可以验证端口（联系 [lorenz@px4.io](mailto:lorenz@px4.io) 获取有关将硬件运送到何处进行测试的指导）。
- 板载必须通过完整的[测试套件](../test_and_ci/index.md)和[飞行测试](../test_and_ci/test_flights.md)。

**PX4 项目保留拒绝接受新端口（或删除当前端口）的权利，原因是未能满足项目设定的要求。**

您可以通过[官方支持渠道](../contribute/support.md)联系核心开发团队和社区。

## 相关信息

- [设备驱动程序](../middleware/drivers.md) - 如何支持新的外设硬件（设备驱动程序）
- [构建代码](../dev_setup/building_px4.md) - 如何构建源代码和上传固件
- 支持的飞行控制器：
  - [自动驾驶仪硬件](../flight_controller/index.md)
  - [支持的板载列表](https://github.com/PX4/PX4-Autopilot/#supported-hardware)（Github）- PX4-Autopilot 具有特定代码的板载
- [支持的外设](../peripherals/index.md)
