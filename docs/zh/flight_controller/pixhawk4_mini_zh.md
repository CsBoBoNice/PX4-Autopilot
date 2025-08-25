# Holybro Pixhawk 4 Mini（已停产）

<Badge type="info" text="已停产" px4_current="v1.15" year="2024"/>

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://holybro.com/)获取硬件支持或合规问题。
:::

_Pixhawk<sup>&reg;</sup> 4 Mini_自动驾驶仪专为希望利用_Pixhawk 4_强大功能但使用较小无人机的工程师和爱好者设计。
_Pixhawk 4 Mini_采用_Pixhawk 4_的FMU处理器和内存资源，同时去除通常不使用的接口。
这使得_Pixhawk 4 Mini_足够小，可以安装在250mm竞速无人机中。

_Pixhawk 4 Mini_与Holybro<sup>&reg;</sup>和Auterion<sup>&reg;</sup>合作设计和开发。
它基于[Pixhawk](https://pixhawk.org/) **FMUv5**设计标准，并经过优化以运行PX4飞行控制软件。

![Pixhawk4 mini](../../assets/flight_controller/pixhawk4mini/pixhawk4mini_iso_1.png)

:::tip
此自动驾驶仪由PX4维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 快速摘要

- 主FMU处理器：STM32F765
  - 32位Arm® Cortex®-M7，216MHz，2MB内存，512KB RAM
- 板载传感器：
  - 加速度计/陀螺仪：ICM-20689
  - 加速度计/陀螺仪：BMI055或ICM20602
  - 磁力计：IST8310
  - 气压计：MS5611
- GPS：u-blox Neo-M8N GPS/GLONASS接收器；集成磁力计IST8310
- 接口：
  - 8个PWM输出
  - FMU上4个专用PWM/捕获输入
  - CPPM专用R/C输入
  - Spektrum/DSM和S.Bus专用R/C输入，带模拟/PWM RSSI输入
  - 3个通用串口
  - 2个I2C端口
  - 3个SPI总线
  - 1个CANBus用于CAN ESC
  - 电池的电压/电流模拟输入
  - 2个额外的模拟输入
- 电源系统：
  - 电源砖输入：4.75~5.5V
  - USB电源输入：4.75~5.25V
  - 舵机轨输入：0~24V
  - 最大电流检测：120A
- 重量和尺寸：
  - 重量：37.2g
  - 尺寸：38x55x15.5mm
- 其他特性：
  - 工作温度：-40 ~ 85°C

其他信息可以在[_Pixhawk 4 Mini_技术数据表](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/pixhawk4mini/pixhawk4mini_technical_data_sheet.pdf)中找到。

## 购买地点

不再可用。

## 接口

![Pixhawk 4 Mini接口](../../assets/flight_controller/pixhawk4mini/pixhawk4mini_interfaces.png)

:::warning
**RC IN**和**PPM**端口仅用于RC接收器。这些是有电源的！永远不要连接任何舵机、电源或电池（或任何连接的接收器）。
:::

## 引脚图

从[这里](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/pixhawk4mini/pixhawk4mini_pinouts.pdf)下载_Pixhawk 4 Mini_引脚图。

## 尺寸

![Pixhawk 4 Mini尺寸](../../assets/flight_controller/pixhawk4mini/pixhawk4mini_dimensions.png)

## 电压额定值

如果提供两个电源，_Pixhawk 4 Mini_可以实现电源冗余。电源轨是：**POWER**和**USB**。

::: info
**MAIN OUT**的输出电源轨不为飞行控制器板供电（也不由其供电）。
您必须向**POWER**或**USB**中的一个[供电](../assembly/quick_start_pixhawk4_mini.md#power)，否则板子将无电源。
:::

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER**（4.75V到5.5V）
1. **USB**输入（4.75V到5.25V）

**绝对最大额定值**

在这些条件下，系统将保持完整。

1. **POWER**输入（0V到6V不受损）
1. **USB**输入（0V到6V不受损）
1. 舵机输入：**MAIN OUT**的VDD_SERVO引脚（0V到24V不受损）

## 组装/设置

[_Pixhawk 4 Mini_接线快速入门](../assembly/quick_start_pixhawk4_mini.md)提供了如何组装所需/重要外设（包括GPS、电源管理板等）的说明。

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v5_default
```

## 调试端口

[PX4系统控制台](../debug/system_console.md)和[SWD接口](../debug/swd_debug.md)在**FMU调试**端口上运行。
要访问这些端口，用户必须拆除_Pixhawk 4 Mini_外壳。

![Pixhawk 4 Mini FMU调试](../../assets/flight_controller/pixhawk4mini/pixhawk4mini_fmu_debug.png)

该端口具有标准串口引脚排列，可以连接到标准FTDI线缆（3.3V，但5V兼容）或[Zubax BugFace BF1](https://github.com/Zubax/bugface_bf1)。
引脚排列使用标准[Pixhawk调试连接器](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)引脚排列。有关如何连接此端口的详细信息，请参考[接线](../debug/system_console.md)页面。

## 串口映射

|  UART  |   设备     | QGC参数描述           |      FC上的端口标签      |
| :----: | :--------: | :-------------------: | :----------------------: |
| UART1  | /dev/ttyS0 |         GPS1          |        GPS模块           |
| USART2 | /dev/ttyS1 |        TELEM1         |          TELEM1          |
| USART3 | /dev/ttyS2 |        TELEM2         |           N/A            |
| UART4  | /dev/ttyS3 |     TELEM/SERIAL4     |        UART/l2C B        |
| USART6 | /dev/ttyS4 |          N/A          |          RC IN           |
| UART7  | /dev/ttyS5 |          N/A          |          调试            |
| UART8  | /dev/ttyS6 |          N/A          | 未连接（无PX4IO）        |

## 外设

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [遥测无线电模块](../telemetry/index.md)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台

电机和舵机按照[机架参考](../airframes/airframe_reference.md)中为您的飞行器指定的顺序连接到**MAIN OUT**端口。
此参考列出了所有支持的空中和地面机架的输出端口到电机/舵机映射（如果您的机架没有在参考中列出，则使用正确类型的"通用"机架）。

:::warning
_Pixhawk 4 Mini_没有AUX端口。
该板不能用于需要超过8个端口或将AUX端口用于电机或控制面的机架。
它可以用于将AUX用于非必要外设的机架（例如"RC AUX1通道的馈通"）。
:::

## 更多信息

- [_Pixhawk 4 Mini_技术数据表](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/pixhawk4mini/pixhawk4mini_technical_data_sheet.pdf)
- [FMUv5参考设计引脚图](https://docs.google.com/spreadsheets/d/1-n0__BYDedQrc_2NHqBenG1DNepAgnHpSGglke-QQwY/edit#gid=912976165)
