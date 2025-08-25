# PX4 参考飞行控制器设计

PX4 参考设计是 [Pixhawk 系列](../flight_controller/pixhawk_series.md)飞行控制器。首次发布于 2011 年，该设计现在已是第 5 [代](#reference_design_generations)（第 6 代板载设计正在进行中）。

## 二进制兼容性

按照特定设计制造的所有板载预期二进制兼容（即可以运行相同的固件）。从 2018 年开始，我们将提供二进制兼容性测试套件，允许我们验证和认证这种兼容性。

FMU 第 1-3 代被设计为开放硬件，而 FMU 第 4 代和第 5 代仅提供引脚和电源规格（原理图由各个制造商创建）。为了更好地确保兼容性，FMUv6 及以后将回到完整的参考设计模型。

<a id="reference_design_generations"></a>

## 参考设计代次

- FMUv1：开发板（STM32F407，128 KB RAM，1MB 闪存，[原理图](https://github.com/pixhawk/Hardware/tree/master/FMUv1)）（PX4 不再支持）
- FMUv2：Pixhawk（STM32F427，168 MHz，192 KB RAM，1MB 闪存，[原理图](https://github.com/pixhawk/Hardware/tree/master/FMUv2)）
- FMUv3：具有 2MB 闪存的 Pixhawk 变体（3DR Pixhawk 2（Solo），Hex Pixhawk 2.1，Holybro Pixfalcon，3DR Pixhawk Mini，STM32F427，168 MHz，256 KB RAM，2 MB 闪存，[原理图](https://github.com/pixhawk/Hardware/tree/master/FMUv3_REV_D)）
- FMUv4：Pixracer（STM32F427，168 MHz，256 KB RAM，2 MB 闪存，[引脚图](https://docs.google.com/spreadsheets/d/1raRRouNsveQz8cj-EneWG6iW0dqGfRAifI91I2Sr5E0/edit#gid=1585075739)）
- FMUv4 PRO：Drotek Pixhawk 3 PRO（STM32F469，180 MHz，384 KB RAM，2 MB 闪存，[引脚图](https://docs.google.com/spreadsheets/d/1raRRouNsveQz8cj-EneWG6iW0dqGfRAifI91I2Sr5E0/edit#gid=1585075739)）
- FMUv5：Holybro Pixhawk 4（STM32F765，216 MHz，512 KB RAM，2 MB 闪存，[引脚图](https://docs.google.com/spreadsheets/d/1-n0__BYDedQrc_2NHqBenG1DNepAgnHpSGglke-QQwY/edit#gid=912976165)）
- FMUv5X：（多种产品）（STM32F765，400 MHz，512KB RAM，2 MB 闪存）（[标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-011%20Pixhawk%20Autopilot%20v5X%20Standard.pdf)）
- FMUv6X：（多种产品）（STM32H753，480 MHz，1 MB RAM，2 MB 闪存）和变体 6i（i.MX RT1050，600 MHz，512 KB RAM，外部闪存）（[标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)）
- FMUv6C：（多种产品）（STM32H743V，480 MHz，1 MB RAM，2 MB 闪存）（[标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-018%20Pixhawk%20Autopilot%20v6C%20Standard.pdf)）
- FMUv6U：（多种产品）（STM32H753，400 MHz，1 MB RAM，2 MB 闪存）（[标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-016%20Pixhawk%20Autopilot%20v6U%20Standard.pdf)）
- FMUv6X-RT：（多种产品）（NXP i.MX RT1176，32 位 Arm® Cortex®-M7，1GHz 32 位 Arm® Cortex®-M4，400MHz 辅助核心，2 MB RAM，64 MB 闪存）和变体 6i（i.MX RT1050，600 MHz，512 KB RAM，外部闪存）（[标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-020%20Pixhawk%20Autopilot%20v6X-RT%20Standard.pdf)）

从 FMUv5X 开始，所有新标准都在 GitHub 上的 [Pixhawk/Pixhawk-Standards](https://github.com/pixhawk/Pixhawk-Standards) 下发布。更多信息请参见 [Pixhawk.org](https://pixhawk.org)。

## Main/IO 功能分解

下图显示了 Pixhawk 系列飞行控制器中 FMU 和 I/O 板载之间的总线和功能责任划分（板载合并到单个物理模块中）。

![PX4 Main/IO Functional Breakdown](../../assets/diagrams/px4_fmu_io_functions.png)

<!-- Draw.io version of file can be found here: https://drive.google.com/file/d/1H0nK7Ufo979BE9EBjJ_ccVx3fcsilPS3/view?usp=sharing -->

一些 Pixhawk 系列控制器没有 I/O 板载构建，以减少空间或复杂性，或更好地满足某些板载用例。
在这种情况下，I/O 驱动程序不会启动。

::: info
没有 I/O 板载的制造商飞行控制器变体通常被命名为包含 I/O 板载版本的"缩小版"：例如 _Pixhawk 4_ **Mini**，_CUAV v5_ **nano**。
:::

必须在具有 I/O 板载的飞行控制器上运行的构建目标将 FMU 输出映射到 `AUX`，将 I/O 输出映射到 `MAIN`（见上图）。
如果目标在不存在 I/O 板载或已禁用的硬件上运行，PWM MAIN 输出将不存在。
例如，您可以通过在 [Pixhawk 4](../flight_controller/pixhawk4.md)（有 IO）和 [Pixhawk 4 Mini](../flight_controller/pixhawk4_mini.md)（无 I/O）上运行 `px4_fmu-v5_default` 看到这一点。

:::warning
在 [Pixhawk 4 Mini](../flight_controller/pixhawk4_mini.md) 上，这会导致飞行控制器上丝印的 `MAIN` 标签与[执行器配置](../config/actuators.md)期间显示的 `AUX` 总线之间的不匹配。
:::

::: info
如果构建目标仅用于在没有 I/O 板载的飞行控制器上运行，则 FMU 输出映射到 `MAIN`（例如，[Pixracer](../flight_controller/pixracer.md) 的 `px4_fmu-v4_default` 目标）。
:::

PX4 PWM 输出在[执行器配置](../config/actuators.md)中映射到 `MAIN` 或 `AUX` 端口。
