# Holybro Pixhawk 4

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://holybro.com/)获取硬件支持或合规问题。
:::

_Pixhawk 4_<sup>&reg;</sup>是与Holybro<sup>&reg;</sup>和PX4团队合作设计和制造的高级自动驾驶仪。
它经过优化以运行PX4 v1.7及更高版本，适合学术和商业开发者。

它基于[Pixhawk项目](https://pixhawk.org/) **FMUv5**开源硬件设计，在[NuttX](https://nuttx.apache.org/) OS上运行PX4。

<img src="../../assets/flight_controller/pixhawk4/pixhawk4_hero_upright.jpg" width="200px" title="Pixhawk4直立图像" /> <img src="../../assets/flight_controller/pixhawk4/pixhawk4_logo_view.jpg" width="420px" title="Pixhawk4图像" />

:::tip
此自动驾驶仪由PX4维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 快速摘要

- 主FMU处理器：STM32F765
  - 32位Arm® Cortex®-M7，216MHz，2MB内存，512KB RAM
- IO处理器：STM32F100
  - 32位Arm® Cortex®-M3，24MHz，8KB SRAM
- 板载传感器：
  - 加速度计/陀螺仪：ICM-20689
  - 加速度计/陀螺仪：BMI055或ICM20602
  - 磁力计：IST8310
  - 气压计：MS5611
- GPS：u-blox Neo-M8N GPS/GLONASS接收器；集成磁力计IST8310
- 接口：
  - 8-16个PWM输出（IO输出8个，FMU输出8个）
  - FMU上3个专用PWM/捕获输入
  - CPPM专用R/C输入
  - Spektrum/DSM和S.Bus专用R/C输入，带模拟/PWM RSSI输入
  - 专用S.Bus舵机输出
  - 5个通用串口
  - 3个I2C端口
  - 4个SPI总线
  - 最多2个CANBus用于双CAN串行ESC
  - 2个电池的电压/电流模拟输入
- 电源系统：
  - 电源模块输出：4.9~5.5V
  - USB电源输入：4.75~5.25V
  - 舵机轨输入：0~36V
- 重量和尺寸：
  - 重量：15.8g
  - 尺寸：44x84x12mm
- 其他特性：
  - 工作温度：-40 ~ 85°C

其他信息可以在[Pixhawk 4技术数据表](https://github.com/PX4/PX4-Autopilot/blob/main/docs/assets/flight_controller/pixhawk4/pixhawk4_technical_data_sheet.pdf)中找到。

## 购买地点

从[Holybro](https://holybro.com/products/pixhawk-4)订购。

## 连接器

![Pixhawk 4连接器](../../assets/flight_controller/pixhawk4/pixhawk4-connectors.jpg)

:::warning
**DSM/SBUS RC**和**PPM RC**端口仅用于RC接收器。
这些是有电源的！永远不要连接任何舵机、电源或电池（或任何连接的接收器）。
:::

## 引脚图

从[这里](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Pixhawk4-Pinouts.pdf)下载_Pixhawk 4_引脚图。

::: info
连接器引脚分配是从左到右（即引脚1是最左边的引脚）。
例外是[调试端口](#debug_port)（引脚1是最右边的，如下所示）。
:::

## 串口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | GPS                   |
| USART2 | /dev/ttyS1 | TELEM1（流控制）      |
| USART3 | /dev/ttyS2 | TELEM2（流控制）      |
| UART4  | /dev/ttyS3 | TELEM4                |
| USART6 | /dev/ttyS4 | RC SBUS               |
| UART7  | /dev/ttyS5 | 调试控制台            |
| UART8  | /dev/ttyS6 | PX4IO                 |

## 尺寸

![Pixhawk 4尺寸](../../assets/flight_controller/pixhawk4/pixhawk4_dimensions.jpg)

## 电压额定值

如果提供三个电源，_Pixhawk 4_可以实现电源三重冗余。三个电源轨是：**POWER1**、**POWER2**和**USB**。

::: info
输出电源轨**FMU PWM OUT**和**I/O PWM OUT**（0V到36V）不为飞行控制器板供电（也不由其供电）。
您必须向**POWER1**、**POWER2**或**USB**中的一个供电，否则板子将无电源。
:::

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER1**和**POWER2**输入（4.9V到5.5V）
1. **USB**输入（4.75V到5.25V）

**绝对最大额定值**

在这些条件下，系统将不消耗任何电力（将不可操作），但将保持完整。

1. **POWER1**和**POWER2**输入（操作范围4.1V到5.7V，0V到10V不受损）
1. **USB**输入（操作范围4.1V到5.7V，0V到6V不受损）
1. 舵机输入：**FMU PWM OUT**和**I/O PWM OUT**的VDD_SERVO引脚（0V到42V不受损）

## 组装/设置

[Pixhawk 4接线快速入门](../assembly/quick_start_pixhawk4.md)提供了如何组装所需/重要外设（包括GPS、电源管理板等）的说明。

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v5_default
```

<a id="debug_port"></a>

## 调试端口

[PX4系统控制台](../debug/system_console.md)和[SWD接口](../debug/swd_debug.md)在**FMU调试**端口上运行，而I/O控制台和SWD接口可以通过**I/O调试**端口访问。
要访问这些端口，用户必须拆除_Pixhawk 4_外壳。

![Pixhawk 4调试端口](../../assets/flight_controller/pixhawk4/pixhawk4_debug_port.jpg)

引脚排列使用标准[Pixhawk调试连接器引脚排列](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
有关接线信息，请参见：

- [系统控制台 > Pixhawk调试端口](../debug/system_console.md#pixhawk_debug_port)

## 外设

- [数字空速传感器](https://store-drotek.com/793-digital-differential-airspeed-sensor-kit-.html)
- [遥测无线电模块](../telemetry/index.md)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通RC舵机或Futaba S-Bus舵机控制的多旋翼/飞机/漫游车或船只。
完整的支持配置集可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [Pixhawk 4技术数据表](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/pixhawk4/pixhawk4_technical_data_sheet.pdf)
- [FMUv5参考设计引脚图](https://docs.google.com/spreadsheets/d/1-n0__BYDedQrc_2NHqBenG1DNepAgnHpSGglke-QQwY/edit#gid=912976165)
- [Pixhawk 4接线快速入门](../assembly/quick_start_pixhawk4.md)
- [Pixhawk 4引脚图](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Pixhawk4-Pinouts.pdf)（Holybro）
- [Pixhawk 4快速入门指南](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Pixhawk4-quickstartguide.pdf)（Holybro）
