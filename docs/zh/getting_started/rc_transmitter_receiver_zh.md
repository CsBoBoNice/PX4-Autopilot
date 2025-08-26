# 无线电控制系统

无线电控制（RC）系统可用于从手持 RC 控制器_手动_控制您的飞行器。
本主题概述了 RC 的工作原理、如何为您的飞行器选择合适的无线电系统，以及如何将其连接到您的飞行控制器。

:::tip
PX4 也可以使用[操纵杆](../config/joystick.md)或类似游戏手柄的控制器进行手动控制：这与 RC 系统不同！
[COM_RC_IN_MODE](../advanced_config/parameter_reference.md#COM_RC_IN_MODE) 参数[可以设置](../advanced_config/parameters.md)来选择是否启用 RC（默认）、操纵杆、两者或都不启用。
:::

::: info
PX4 在自主飞行模式下不需要遥控系统。
:::

## RC 系统如何工作？

_RC 系统_有一个基于地面的_遥控单元_，操作员用它来指挥飞行器。
遥控器有物理控制装置，可用于指定飞行器运动（例如速度、方向、油门、偏航、俯仰、横滚等）并启用自动驾驶仪[飞行模式](../flight_modes/index.md)（例如起飞、着陆、返航、任务等）。
在_启用遥测_的 RC 系统上，遥控单元还可以接收和显示来自飞行器的信息，例如电池电量、飞行模式和警告。

![Taranis X9D 发射器](../../assets/hardware/transmitters/frsky_taranis_x9d_transmitter.jpg)

基于地面的 RC 控制器包含一个无线电模块，该模块与飞行器上的（兼容）无线电模块绑定并通信。
基于飞行器的单元连接到飞行控制器。
飞行控制器根据当前的自动驾驶仪飞行模式和飞行器状态确定如何解释命令，并适当地驱动飞行器电机和执行器。

<!-- image showing the different parts here would be nice -->

::: info
基于地面和飞行器的无线电模块分别称为发射器和接收器（即使它们支持双向通信），统称为_发射器/接收器对_。
RC 控制器及其包含的无线电模块通常称为"发射器"。
:::

RC 系统的一个重要品质是它支持多少"通道"。
通道数定义了遥控器上可以用于向飞行器发送命令的不同物理控制装置的数量（例如可以实际使用多少开关、旋钮、控制杆）。

飞机必须使用至少支持 4 个通道的系统（用于横滚、俯仰、偏航、推力）。
地面车辆至少需要两个通道（转向 + 油门）。8 或 16 通道发射器提供额外的通道，可用于控制其他机制或激活自动驾驶仪提供的不同[飞行模式](../flight_modes/index.md)。

## 遥控器类型

<a id="transmitter_modes"></a>

### 飞机遥控单元

下面显示了 UAV 最流行的遥控单元_形式_。
它有单独的控制杆来控制横滚/俯仰和油门/偏航，如图所示（即飞机至少需要 4 个通道）。

![RC 基本命令](../../assets/flying/rc_basic_commands.png)

控制杆、开关等有许多可能的布局。
更常见的布局被赋予了特定的"模式"编号。_模式 1_ 和_模式 2_（如下所示）仅在油门位置上有所不同。

![模式1-模式2](../../assets/concepts/mode1_mode2.png)

::: info
模式的选择很大程度上是品味问题（_模式 2_ 更受欢迎）。
:::

## 地面车辆遥控单元

无人地面车辆（UGV）/汽车最少需要 2 通道发射器才能发送转向和速度值。
通常发射器使用方向盘和扳机、两个单轴控制杆或单个双轴控制杆来设置这些值。

没有什么能阻止您使用更多通道/控制机制，这些对于接合额外的执行器和自动驾驶仪模式非常有用。

## 选择 RC 系统组件

您需要选择彼此兼容的发射器/接收器对。
此外，接收器必须[与 PX4 兼容](#compatible_receivers)和飞行控制器硬件。

兼容的无线电系统通常一起销售。
例如，[FrSky Taranis X9D 和 FrSky X8R](https://hobbyking.com/en_us/frsky-2-4ghz-accst-taranis-x9d-plus-and-x8r-combo-digital-telemetry-radio-system-mode-2.html?___store=en_us) 是一个受欢迎的组合。

### 发射器/接收器对

最受欢迎的 RC 单元之一是 _FrSky Taranis X9D_。
它有一个内部发射器模块，可以与推荐的 _FrSky X4R-SB_（S-BUS，低延迟）或 _X4R_（PPM-Sum，传统）接收器开箱即用。
它还有一个自定义无线电发射器模块插槽和可定制的开源 OpenTX 固件。

::: info
当与 [FrSky](../peripherals/frsky_telemetry.md) 或 [TBS Crossfire](../telemetry/crsf_telemetry.md) 无线电模块一起使用时，此遥控单元可以显示飞行器遥测数据。
:::

其他流行的发射器/接收器对

- Turnigy 遥控器使用，例如 FrSky 发射器/接收器模块。
- Futaba 发射器和兼容的 Futaba S-Bus 接收器。
- 长距离 ~900MHz，低延迟："Team Black Sheep Crossfire"或"Crossfire Micro"套装，配有兼容的遥控器（例如 Taranis）
- 长距离 ~433MHz：ImmersionRC EzUHF 套装，配有兼容的遥控器（例如 Taranis）

### PX4 兼容接收器 {#compatible_receivers}

除了发射器/接收器对兼容外，接收器还必须与 PX4 和飞行控制器硬件兼容。

_PX4_ 和 _Pixhawk_ 已通过以下验证：

- PPM sum 接收器
- S.BUS 和 S.BUS2 接收器来自：
  - Futaba
  - FrSky S.BUS 和 PPM 型号
  - TBS Crossfire，输出协议为 SBUS
  - Herelink

- TBS Crossfire，使用 ([CRSF 协议](../telemetry/crsf_telemetry.md))
- Express LRS，使用 ([CRSF 协议](../telemetry/crsf_telemetry.md))

- TBS Ghost，使用 (GHST 协议)
- Spektrum DSM
- Graupner HoTT

使用支持协议的其他供应商的接收器可能会工作，但尚未测试。

::: info
历史上，接收器型号之间存在差异和不兼容性，主要是由于缺乏协议的详细规范。
我们测试的接收器现在看起来都是兼容的，但其他接收器可能不兼容。
:::

## 连接接收器

作为一般指导，接收器使用适合其支持协议的端口连接到飞行控制器：

- Spektrum/DSM 接收器连接到"DSM"输入。
  Pixhawk 飞行控制器的标签各不相同：`SPKT/DSM`、`DSM`、`DSM/SBUS RC`、`DSM RC`、`DSM/SBUS/RSSI`。
- Graupner HoTT 接收器：SUMD 输出必须连接到 **SPKT/DSM** 输入（如上所述）。
- PPM-Sum 和 S.BUS 接收器必须直接连接到 **RC** 地、电源和信号引脚。
  这通常标记为：`RC IN`、`RCIN` 或 `RC`，但在某些 FC 中标记为 `PPM RC` 或 `PPM`。
- 每个通道都有单独导线的 PPM 接收器必须通过 PPM 编码器[像这样](https://www.getfpv.com/radios/radio-accessories/holybro-ppm-encoder-module.html)连接到 RCIN 通道（PPM-Sum 接收器对所有通道使用单个信号线）。
- 使用 [CRSF 遥测](../telemetry/crsf_telemetry.md)的 TBS Crossfire/Express LRS 接收器通过备用 UART 连接。

飞行控制器通常包括用于连接常见接收器类型的适当电缆。

连接到特定飞行控制器的说明在其[快速入门](../assembly/index.md)指南中给出（例如 [CUAV Pixhawk V6X 接线快速入门：无线电控制](../assembly/quick_start_cuav_pixhawk_v6x.md#radio-control)或 [Holybro Pixhawk 6X 接线快速入门：无线电控制](../assembly/quick_start_pixhawk6x.md#radio-control)）。

:::tip
有关其他信息，请参阅制造商的飞行控制器设置指南。
:::

<a id="binding"></a>

## 绑定发射器/接收器

在校准/使用无线电系统之前，您必须_绑定_接收器和发射器，以便它们仅相互通信。
绑定发射器和接收器对的过程是特定于硬件的（有关说明，请参阅您的手册）。

如果您使用 _Spektrum_ 接收器，可以使用 _QGroundControl_ 将其置于绑定模式：[无线电设置 > Spectrum 绑定](../config/radio.md#spectrum-bind)。

## 设置信号丢失行为

RC 接收器有不同的方式来指示信号丢失：

- 不输出任何信号（PX4 自动检测）
- 输出低油门值（您可以[配置 PX4 检测此情况](../config/radio.md#rc-loss-detection)）。
- 输出最后接收到的信号（PX4 无法处理这种情况！）

选择在 RC 丢失时可以不发射任何信号（首选）或低油门值的接收器。
此行为可能需要接收器的硬件配置（查看手册）。

更多信息请参见[无线电控制设置 > RC 丢失检测](../config/radio.md#rc-loss-detection)。

## 相关主题

- [无线电控制设置](../config/radio.md) - 使用 PX4 配置您的无线电。
- [多旋翼](../flying/basic_flying_mc.md)或[固定翼](../flying/basic_flying_fw.md)手动飞行 - 学习如何使用遥控器飞行。
- [TBS Crossfire (CRSF) 遥测](../telemetry/crsf_telemetry.md)
- [FrSky 遥测](../peripherals/frsky_telemetry.md)
