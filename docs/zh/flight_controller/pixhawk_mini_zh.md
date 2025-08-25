# Holybro Pixhawk Mini (已停产)

:::warning
PX4 不制造此（或任何）自动驾驶仪。
如有硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

Holybro _Pixhawk<sup>&reg;</sup> Mini_ 自动驾驶仪是 Pixhawk 的下一代演进产品。
它的尺寸约为原始 Pixhawk 的 1/3，并拥有更强大的处理器和传感器。

Pixhawk Mini 基于 PX4 开源硬件项目，并已针对 PX4 飞行堆栈进行了优化。

![Pixhawk Mini](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_hero.jpg)

接线信息见[下文](#wiring)。

::: info
此飞控是由 3DR 与 HobbyKing<sup>&reg;</sup> 合作设计的。
它之前被称为 3DR Pixhawk Mini。
:::

:::tip
此自动驾驶仪[受到](../flight_controller/autopilot_pixhawk_standard.md) PX4 维护和测试团队的支持。
:::

## 规格参数

**处理器：**

- **主处理器：** STM32F427 Rev 3
- **IO 处理器：** STM32F103

**传感器：**

- **加速度计/陀螺仪/磁力计：** MPU9250
  - PX4 固件[已弃用](https://github.com/PX4/PX4-Autopilot/pull/7618)
- **加速度计/陀螺仪：** ICM20608
- **气压计：** MS5611

**电压规格：**

- **电源模块输出：** 4.1~5.5V
- **最大输入电压：** 45V (10S LiPo)
- **最大电流检测：** 90A
- **USB 电源输入：** 4.1~5.5V
- **舵机导轨输入：** 0~10V

**接口：**

- 1x UART 串口（用于 GPS）
- Spektrum DSM/DSM2/DSM-X® 卫星兼容的遥控输入
- Futaba S BUS® 兼容的遥控输入
- PPM Sum 信号遥控输入
- I2C（用于数字传感器）
- CAN（用于兼容控制器的数字电机控制）
- ADC（用于模拟传感器）
- Micro USB 端口

**重量和尺寸：**

- **尺寸：** 38x43x12mm
- **重量：** 15.8g

**GPS 模块（套件提供）：**

- **GNSS 接收器：** u-blox<sup>&reg;</sup> Neo-M8N；罗盘 HMC5983
- **重量：** 22.4g
- **尺寸：** 37x37x12mm

## 购买渠道

已停产。

## 连接器分配

`<待添加>`

## 功能特点

Pixhawk Mini 的主要特点包括：

- 先进的 32 位 ARM Cortex® M4 处理器，运行 NuttX RTOS
- 8 个 PWM/舵机输出
- 多种连接选项用于附加外设（UART、I2C、CAN）
- 冗余电源输入和自动故障转移
- 集成安全开关和可选外部安全按钮，便于电机激活
- 多色 LED 指示器
- 集成多音调压电音频指示器
- microSD 卡用于长时间高速日志记录
- 易于使用的 Micro JST 连接器

Pixhawk Mini 配备了新的 **GPS 模块**：

- 基于 u-blox M8N
- 同时接收多达 3 个 GNSS（GPS、Galileo、GLONASS、北斗）
- 行业领先的 -167 dBm 导航灵敏度
- 安全和完整性保护
- 支持所有卫星增强系统
- 高级干扰和欺骗检测
- 产品变体满足性能和成本要求

## 套件包装

_Pixhawk Mini_ 配送时包含以下内容：

| 组件                                                          | 图片                                                                                                                                |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| Pixhawk Mini 自动驾驶仪                                             | ![Pixhawk Mini](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_drawing.png)                                                |
| GPS 模块                                                         | ![罗盘+GPS 模块](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_compass_drawing.png)                                  |
| 四轴电源分配板                                      | ![四轴电源分配板](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_quad_power_distribution_board_drawing.png) |
| 8 通道 PWM 分线板                                       | ![8 通道 PWM 分线板](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_8_channel_pwm_breakout_board_drawing.png)   |
| 4 芯线缆（用于 I2C）                                              | ![4 芯线缆（用于 I2C）](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_4_pin_cable_drawing.png)                           |
| PPM/SBUS 遥控输入线缆                                           | ![PPM/SBUS 遥控输入线缆](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_rc_in_cable_drawing.png)                        |
| 6 转 6/4 'Y' 型适配器（用于 GPS 和额外的 I2C 设备）            | ![6 转 6/4 'Y' 型适配器](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_6_to_6_and_4_pin_Y_cable_drawing.png)               |
| 6 芯线缆 (2) （用于电源分配板和罗盘/GPS） | ![6 芯线缆](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_6_pin_cable_drawing.png)                                     |
| 6 芯 JST 转 DF13（用于传统数传电台）                       | ![6 芯 JST 转 DF13](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_6pin_JST_to_DF13_cable_drawing.png)                    |
| 安全开关                                                      | ![安全开关](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_safety_switch_drawing.png)                                 |
| 8 通道 PWM 分线线缆                                       | ![8 通道 PWM 分线线缆](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_8channel_pwm_breakout_cable_drawing.png)    |
| 安装海绵                                                      | ![安装海绵](../../assets/hardware/mounting/3dr_anti_vibration_mounting_foam.png)                                                |
| I2C 分线板 ? - 手册中未列出的零件                 | -                                                                                                                                    |

## 可选配件

- 数传电台套装：915 MHz（美国）、433 MHz（欧洲）
  ::: info
  安装 3DR 数传电台时，请使用 Pixhawk Mini 附带的连接器，而不是电台附带的连接器。
  :::

- 3DR 10S 电源模块
- WiFi 数传电台
- 数字空速传感器

## 兼容性

### 遥控器

- PPM 输出遥控接收器
- Spektrum DSM 遥控接收器
- Futaba S BUS 遥控接收器

### 电调

- 所有标准 PWM 输入电调

## 连接器引脚分配（引脚图）

![Pixhawk Mini - 连接器引脚图](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_pinout.png)

## 产品比较

### Pixhawk Mini vs Pixhawk（原版）

- 尺寸减小三分之一 - 从 50x81.5x15.5mm 到 38x43x12mm。
- Rev 3 处理器，充分利用 2MB 闪存。
- 传感器改进，主要和辅助 IMU 分别为 MPU9250 和 ICM20608。
  结果是更稳定、更可靠的飞行和导航。
- 包含 GPS+罗盘模块。采用支持 GLONASS 的 Neo M8N；罗盘 HMC5983。
  期待更快更强的 GPS 锁定。
- 使用 Micro JST 连接器而非 DF-13。
  这些更容易使用。
- 集成压电扬声器和安全开关。
- 通过包含的 PDB 原生支持 4S 电池。

### Pixhawk Mini vs Pixfalcon

- 传感器改进，主要和辅助 IMU 分别为 MPU9250 和 ICM20608。
  期待更好的振动处理和可靠性。
- CAN 接口支持 UAVCAN。
- 包含 8 通道分线舵机导轨，适用于需要有源 PWM 输出的飞机和其他载具。
- 包含 I2C 分线板，总共 5 个 I2C 连接。
- 尺寸相似。

Pixhawk Mini 采用来自 ST Microelectronics® 的先进处理器和传感器技术以及 NuttX 实时操作系统，为控制任何自主载具提供卓越的性能、灵活性和可靠性。

## 已知问题

- 一些 Pixhawk Mini 有[硬件缺陷](https://github.com/PX4/PX4-Autopilot/issues/7327#issuecomment-317132917)，使内部 MPU9250 IMU 不可靠。
  - 此问题仅存在于较旧的硬件版本中，因为[制造商在某个时候修复了它](https://github.com/PX4/PX4-Autopilot/issues/7327#issuecomment-372393609)。
  - 要检查特定板子是否受影响，将板子断开连接一段时间，然后上电并尝试从 PX4 命令行启动 mpu9250 驱动程序。如果板子受影响，驱动程序将无法启动。
  - MPU9250 在 PX4 固件中[默认禁用](https://github.com/PX4/PX4-Autopilot/pull/7618)。
  - 有缺陷的 Pixhawk Mini 在没有外部磁力计或连接的 GPS 的情况下无法校准，即使在室内也是如此。
  - 使用外部 GPS 时，[这不是问题](https://github.com/PX4/PX4-Autopilot/pull/7618#issuecomment-320270082)，因为辅助 ICM20608 提供加速度计和陀螺仪，而外部 GPS 提供磁力计。

<a id="wiring"></a>

## 接线快速入门

:::warning
_Pixhawk Mini_ 不再由 3DR 制造或提供。
:::

本快速入门指南展示如何为 [Pixhawk Mini](../flight_controller/pixhawk_mini.md) 供电并连接其最重要的外设。

### 标准接线图

下图显示了使用 _Pixhawk Mini 套件_ 和 3DR 数传电台的标准_四轴飞行器_接线（连同电调、电机、电池和在手机上运行的地面控制站）。
我们将在以下部分中讨论每个主要部分。

![QAV250 的 Pixhawk Mini 电子设备接线（机架外）](../../assets/airframes/multicopter/lumenier_qav250_pixhawk_mini/qav250_wiring_image_pixhawk_mini.jpg)

::: info
其他类型载具的输出接线/供电略有不同。下面对 VTOL、飞机、多轴更详细地涵盖了这一点。
:::

### 安装和定向控制器

_Pixhawk Mini_ 应使用减振海绵垫（套件中包含）安装在机架上。它应尽可能靠近载具的重心定位，顶面朝上，箭头指向载具前方。

![Pixhawk Mini 推荐方向](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_mounting_arrow.jpg)

![安装海绵](../../assets/hardware/mounting/3dr_anti_vibration_mounting_foam.png)

::: info
如果控制器无法以推荐/默认方向安装（例如由于空间限制），您需要为自动驾驶仪软件配置您实际使用的方向：[飞控方向](../config/flight_controller_orientation.md)。
:::

### GPS + 罗盘

使用提供的 6 芯线缆将 3DR GPS + 罗盘连接到 Pixhawk Mini 的 **GPS&I2C** 端口（右上角）。
GPS/罗盘应安装在机架上，尽可能远离其他电子设备，面向载具前方（将罗盘与其他电子设备分离将减少干扰）。

![将罗盘/GPS 连接到 Pixhawk Mini](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_with_compass.jpg)

注意 - 插入显示两个端口的图片？或者 GPS&I2C 的正面图

首次使用前必须校准罗盘：[罗盘校准](../config/compass.md)

### 电源

下图显示了在四轴飞行器中使用 _Pixhawk Mini_ 时的典型电源供应接线。
这使用套件中的 _四轴电源分配板_ 从电池为 Pixhawk Mini 和 电调/电机供电（也可以为其他配件供电）。

::: info
_四轴电源分配板_ 包含适用于 <= 4S 电池的电源模块 (PM)。
如果您需要更多功率，推荐使用 _3DR 10S 电源模块_（已停产）。
:::

![Pixhawk Mini - 供电](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_powering_quad_board.jpg)

_Pixhawk Mini_ 通过 **PM** 端口供电。
使用电源模块时（如本例），端口还将读取模拟电压和电流测量值。

最多 4 个电调可以从电源分配板单独供电（尽管在本例中我们只连接了一个）。

控制信号来自 MAIN OUT。在本例中只有一个控制通道，通过 _8 通道 PWM 分线板_ 连接到电调。

Pixhawk Mini 输出导轨（MAIN OUT）无法为连接的设备供电（在所示电路中也不需要）。
对于 MAIN OUT 连接到需要电源的设备的载具（例如飞机中使用的舵机），您需要使用 BEC（电池消除电路）为导轨供电。
包含的分线板允许一个通道为其他输出提供电源。

### 遥控器

Pixhawk Mini 支持许多不同的无线电接收器型号：

- Spektrum 和 DSM 接收器连接到 **SPKT/DSM** 输入。

  <img src="../../assets/flight_controller/pixhawk_mini/pixhawk_mini_port_spkt_dsm.png" width="350px" title="Pixhawk Mini - Spektrum 接收器的无线电端口" />

- PPM-SUM 和 S.BUS 接收器连接到 **RCIN** 端口。

  <img src="../../assets/flight_controller/pixhawk_mini/pixhawk_mini_port_rcin.png" width="350px" title="Pixhawk Mini - PPM 接收器的无线电端口" />

- _每个通道都有单独线路_的 PPM 和 PWM 接收器必须通过 PPM 编码器连接到 **RCIN** 端口，[如这个](https://www.getfpv.com/radios/radio-accessories/holybro-ppm-encoder-module.html)（PPM-Sum 接收器对所有通道使用单根信号线）。

有关选择无线电系统、接收器兼容性和绑定发射器/接收器对的更多信息，请参阅：[遥控发射器和接收器](../getting_started/rc_transmitter_receiver.md)。

### 安全开关（可选）

控制器有一个集成的安全开关，一旦自动驾驶仪准备好起飞，您可以使用它激活电机。
如果在特定载具上这个开关难以接近，您可以连接（可选的）外部安全按钮，如下所示。

![Pixhawk Mini - 可选开关](../../assets/flight_controller/pixhawk_mini/pixhawk_mini_safety_switch_wiring.jpg)

### 数传电台

### 电机

所有支持的空中和地面机架的 MAIN/AUX 输出端口与电机/舵机之间的映射列在[机架参考](../airframes/airframe_reference.md)中。

:::warning
映射在不同机架之间不一致（例如，您不能依赖油门在所有飞机机架的相同输出上）。
确保为您的载具使用正确的映射。
:::

:::tip
如果您的机架未在参考中列出，则使用正确类型的"通用"机架。
:::

:::info
- 输出导轨必须单独供电，如上面[电源](#power)部分所讨论的。
- Pixhawk Mini 不能用于 QuadPlane VTOL 机架。这是因为 QuadPlane 需要 9 个输出（4 个主要，5 个辅助），而 Pixhawk Mini 只有 8 个输出（8 个主要）。
:::

<img src="../../assets/flight_controller/pixhawk_mini/pixhawk_mini_port_main_out.png" width="350px" title="Pixhawk Mini - 电机/舵机端口" />

### 其他外设

其他组件的接线和配置在各个[外设](../peripherals/index.md)主题中介绍。

### 配置

一般配置信息在：[自动驾驶仪配置](../config/index.md)中介绍。

QuadPlane 特定配置在这里介绍：[QuadPlane VTOL 配置](../config_vtol/vtol_quad_configuration.md)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v3_default
```

## 调试端口

此板没有调试端口（即它没有用于访问[系统控制台](../debug/system_console.md)或 [SWD 接口](../debug/swd_debug.md)的端口）。

开发人员需要焊接线路到板子测试焊盘进行 SWD，以及焊接到 STM32F4 (IC) TX 和 RX 以获得控制台。
