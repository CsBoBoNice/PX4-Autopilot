# Pixhawk 系列

[Pixhawk<sup>&reg;</sup>](https://pixhawk.org/) 是一个独立的开源硬件项目，为学术、爱好者和工业社区提供现成可用、低成本且高端的_自动驾驶仪硬件设计_。

Pixhawk 是 PX4 的参考硬件平台，在 [NuttX](https://nuttx.apache.org/) 操作系统上运行 PX4。

制造商基于开源设计创建了许多不同的板子，这些板子的外形因素针对从货物运输到第一人称视角 (FPV) 竞速器等应用进行了优化。

:::tip
对于计算密集型任务（例如计算机视觉），您需要一个单独的伴飞计算机（例如 [Raspberry Pi 2/3 Navio2](../flight_controller/raspberry_pi_navio2.md)）或具有集成伴飞解决方案的平台。
:::

## 主要优势

使用 _Pixhawk 系列_ 控制器的主要优势包括：

- 软件支持 - 作为 PX4 参考硬件，这些是我们维护得最好的板子。
- 在可连接的硬件外设方面具有灵活性。
- 高质量。
- 在外形因素方面高度可定制。
- 使用广泛，因此经过充分测试/稳定。
- 通过 _QGroundControl_ 自动更新最新固件（用户友好）。

## 支持的板子

PX4 项目使用 [Pixhawk 标准自动驾驶仪](../flight_controller/autopilot_pixhawk_standard.md) 作为参考硬件。
这些是完全兼容 Pixhawk 标准（包括使用商标）且仍在制造的控制器。

::: info
PX4 维护和测试团队维护并支持这些标准板子。
:::

不完全符合规范的类 Pixhawk 板子可能是[制造商支持的](../flight_controller/autopilot_manufacturer_supported.md)、[实验性/停产的](../flight_controller/autopilot_experimental.md)或不受支持的。

本主题的其余部分对 Pixhawk 系列进行了更多解释，但不是必读内容。

## 背景

[Pixhawk 项目](https://pixhawk.org/) 以原理图的形式创建开源硬件设计，这些原理图定义了一组组件（CPU、传感器等）及其连接/引脚映射。

鼓励制造商采用[开源设计](https://github.com/pixhawk/Hardware)并创建最适合特定市场或用例的产品（物理布局/外形因素不属于开源规范的一部分）。基于相同设计的板子是二进制兼容的。

::: info
虽然不强制要求物理连接器标准，但较新的产品通常遵循 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
:::

该项目还基于开源设计创建参考自动驾驶仪板子，并在相同的[许可证](#licensing-and-trademarks)下共享它们。

<a id="fmu_versions"></a>

### FMU 版本

Pixhawk 项目创建了许多不同的开源设计/原理图。
基于同一设计的所有板子应该是二进制兼容的（运行相同的固件）。

每个设计都使用以下命名：FMUvX（例如：FMUv1、FMUv2、FMUv3、FMUv4 等）。
更高的 FMU 数字表示板子更新，但可能不表示能力增强（版本可能几乎相同 - 仅在连接器接线上有所不同）。

PX4 _用户_ 通常不需要对 FMU 版本了解太多：

- _QGroundControl_ 自动为连接的自动驾驶仪下载正确的固件（基于其"幕后"的 FMU 版本）。
- 选择控制器通常基于物理约束/外形因素而非 FMU 版本。

::: info
例外情况是，如果您使用 FMUv2 固件，它[限制为 1MB 闪存](../flight_controller/silicon_errata.md#fmuv2-pixhawk-silicon-errata)。
为了将 PX4 装入这个有限的空间，许多模块默认被禁用。
您可能会发现一些[参数缺失](../advanced_config/parameters.md#missing)，以及一些硬件无法"开箱即用"。
:::

PX4 _开发者_ 需要知道其板子的 FMU 版本，因为构建自定义硬件时需要这个信息。

从很高的层面来看，主要差异是：

- **FMUv2：** 带有 STM32427VI 处理器的单板（[Pixhawk 1（已停产）](../flight_controller/pixhawk.md)、[pix32](../flight_controller/holybro_pix32.md)、[Pixfalcon](../flight_controller/pixfalcon.md)、[Drotek DroPix](../flight_controller/dropix.md)）
- **FMUv3：** 与 FMUv2 相同，但可用闪存翻倍至 2MB（[Hex Cube Black](../flight_controller/pixhawk-2.md)、[CUAV Pixhack v3](../flight_controller/pixhack_v3.md)、[mRo Pixhawk](../flight_controller/mro_pixhawk.md)、[Pixhawk Mini（已停产）](../flight_controller/pixhawk_mini.md)）
- **FMUv4：** 增加了 RAM。更快的 CPU。更多串口。没有 IO 处理器（[Pixracer](../flight_controller/pixracer.md)）
- **FMUv4-PRO：** 稍微增加了 RAM。更多串口。有 IO 处理器（[Pixhawk 3 Pro](../flight_controller/pixhawk3_pro.md)）
- **FMUv5：** 新处理器 (F7)。
  快得多。
  更多 RAM。
  更多 CAN 总线。
  更加可配置。
  （[Pixhawk 4](../flight_controller/pixhawk4.md)、[CUAV v5](../flight_controller/cuav_v5.md)、[CUAV V5+](../flight_controller/cuav_v5_plus.md)、[CUAV V5 nano](../flight_controller/cuav_v5_nano.md)）
- **FMUv5X：** 新处理器 (F7)。
  快得多，模块化设计。
  更可靠。
  更多冗余。
  更多 RAM (1MB)。
  更多 CAN 总线。
  更加可配置和可定制。
  （[Pixhawk 5X](../flight_controller/pixhawk5x.md)、Skynode）
- **FMUv6C：**
  （[Holybro Pixhawk 6C Mini](../flight_controller/pixhawk6c_mini.md)、[Holybro Pixhawk 6C](../flight_controller/pixhawk6c.md)）
- **FMUv6X：**
  （[CUAV Pixhawk V6X](../flight_controller/cuav_pixhawk_v6x.md)、[Holybro Pixhawk 6X](../flight_controller/pixhawk6x.md)）
- **FMUv6X-RT：** 更快的 MCU 核心（1GHz）（相比 6X 上的 480Mhz）。
  更多 RAM (2Mb)。
  更多闪存 (64Mb)（v6X/v5X 上为 2Mb）。
  （[Holybro Pixhawk 6X-RT](../flight_controller/pixhawk6x-rt.md)）

<a id="licensing-and-trademarks"></a>

### 许可证和商标

Pixhawk 项目原理图和参考设计在 [CC BY-SA 3](https://creativecommons.org/licenses/by-sa/3.0/legalcode) 许可证下获得许可。

该许可证允许您以几乎任何方式使用、销售、共享、修改和构建文件 - 只要您给予信用/归属，并且您在相同的开源许可证下共享您所做的任何更改（请参阅[许可证的人类可读版本](https://creativecommons.org/licenses/by-sa/3.0/)了解权利和义务的简明摘要）。

::: info
_直接衍生_ 自 Pixhawk 项目原理图文件（或参考板）的板子必须开源。
它们不能作为专有产品进行商业许可。
:::

制造商可以通过首先生成具有与 FMU 设计相同引脚映射/组件的全新原理图文件来创建（兼容的）_完全独立的产品_。
基于独立创建的原理图的产品被视为原创作品，可以根据需要获得许可。

产品名称/品牌也可以注册商标。
未经所有者许可，不得使用商标名称。

:::tip
_Pixhawk_ 是一个商标，未经许可不得在产品名称中使用。
:::

## 附加信息

### LED

所有 _Pixhawk 系列_ 飞控都支持：

- 一个面向用户的 RGB _UI LED_，用于指示载具当前的_准备飞行_状态。这通常是一个超亮的 I2C 外设，可能安装在板上，也可能不安装（即 FMUv4 板上没有，通常使用安装在 GPS 上的 LED）。
- 三个*状态 LED*，提供较低级别的电源状态、引导加载程序模式和活动以及错误信息。

要解释 LED 含义，请参阅：[LED 含义](../getting_started/led_meanings.md)。
