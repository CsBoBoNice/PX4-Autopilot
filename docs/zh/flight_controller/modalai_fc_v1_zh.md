# ModalAI Flight Core v1

<Badge type="info" text="已停产" /> <Badge type="tip" text="PX4 v1.11" />

:::warning
此机架已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://forum.modalai.com/)获取硬件支持或合规问题。
:::

ModalAI _Flight Core v1_（[数据表](https://docs.modalai.com/flight-core-datasheet)）是美国制造的PX4飞行控制器。
Flight Core可以与ModalAI VOXL配对用于避障和GPS拒止导航，或作为独立飞行控制器单独使用。

![FlightCoreV1](../../assets/flight_controller/modalai/fc_v1/main.jpg)

Flight Core与[VOXL Flight](https://www.modalai.com/voxl-flight)（[数据表](https://docs.modalai.com/voxl-flight-datasheet/)）的PX4飞行控制器部分相同，VOXL Flight将VOXL伴随计算机和Flight Core集成到单个PCB上。

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 规格

| 特性             | 详细信息                                                      |
| :--------------- | :----------------------------------------------------------- |
| 重量             | 6g                                                           |
| MCU              | 216MHz, 32位ARM M7 [STM32F765II][stm32f765ii]               |
| 内存             | 256Kb FRAM                                                   |
|                  | 2Mbit闪存                                                    |
|                  | 512Kbit SRAM                                                 |
| 固件             | [PX4][px4]                                                   |
| IMU              | [ICM-20602][icm-20602] (SPI1)                                |
|                  | ICM-42688 (SPI2)                                             |
|                  | [BMI088][bmi088] (SPI6)                                      |
| 气压计           | [BMP388][bmp388] (I2C4)                                      |
| 安全元件         | [A71CH][a71ch] (I2C4)                                        |
| microSD卡        | [支持的卡信息](../dev_log/logging.md#sd-cards)              |
| 输入             | GPS/磁力计                                                   |
|                  | Spektrum                                                     |
|                  | 遥测                                                         |
|                  | CAN总线                                                      |
|                  | PPM                                                          |
| 输出             | 6个LED（2个RGB）                                            |
|                  | 8个PWM通道                                                   |
| 额外接口         | 3个串口                                                      |
|                  | I2C                                                          |
|                  | GPIO                                                         |

::: info
更详细的硬件文档可以在[这里](https://docs.modalai.com/flight-core-datasheet/)找到。
:::

<!-- reference links for table above (improve layout) -->

[stm32f765ii]: https://www.st.com/en/microcontrollers-microprocessors/stm32f765ii.html
[bmp388]: https://www.adafruit.com/product/3966
[icm-20602]: https://invensense.tdk.com/products/motion-tracking/6-axis/icm-20602/
[bmi088]: https://www.bosch-sensortec.com/products/motion-sensors/imus/bmi088/
[px4]: https://github.com/PX4/PX4-Autopilot/tree/main/boards/modalai/fc-v1
[a71ch]: https://www.nxp.com/products/security-and-authentication/authentication/plug-and-trust-the-fast-easy-way-to-deploy-secure-iot-connections:A71CH

## 尺寸

![FlightCoreV1Dimensions](../../assets/flight_controller/modalai/fc_v1/dimensions.png)

## PX4固件兼容性

_Flight Core v1_与PX4 v1.11的官方PX4固件完全兼容。

ModalAI维护了PX4 v1.11的[分支PX4版本](https://github.com/modalai/px4-firmware/tree/modalai-1.11)。
这包括UART ESC支持以及计划上游的VIO和VOA改进。

有关固件的更多信息可以在[这里](https://docs.modalai.com/flight-core-firmware/)找到。

## QGroundControl支持

此板在QGroundControl 4.0及更高版本中受支持。

## 可用性

- 不再可用

## 快速入门

### 方向

下图显示了推荐的方向，对应于从PX4 v1.11开始的`ROTATION_NONE`。

![FlightCoreV1Orientation](../../assets/flight_controller/modalai/fc_v1/orientation.png)

### 连接器

有关引脚排列的详细信息可以在[这里](https://docs.modalai.com/flight-core-datasheet-connectors)找到。

![FlightCoreV1Top](../../assets/flight_controller/modalai/fc_v1/top.png)

| 连接器 | 摘要                                  |
| ------ | ------------------------------------ |
| J1     | VOXL通信接口连接器（TELEM2）         |
| J2     | 编程和调试连接器                     |
| J3     | USB连接器                            |
| J4     | UART2，UART ESC（TELEM3）            |
| J5     | 遥测连接器（TELEM1）                 |
| J6     | VOXL-电源管理输入/扩展               |
| J7     | 8通道PWM输出连接器                   |
| J8     | CAN总线连接器                        |
| J9     | PPM RC输入                           |
| J10    | 外部GPS和磁力计连接器                |
| J12    | RC输入，Spektrum/SBus/UART连接器     |
| J13    | I2C显示（备用传感器连接器）/安全按钮输入 |

![FlightCoreV1Bottom](../../assets/flight_controller/modalai/fc_v1/bottom.png)

### 用户指南

完整的用户指南可在[这里](https://docs.modalai.com/flight-core-manual/)获取。

### 如何构建

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make modalai_fc-v1
```

## 串口映射

| UART   | 设备       | 端口                                     |
| ------ | ---------- | ---------------------------------------- |
| USART1 | /dev/ttyS0 | GPS1 (J10)                               |
| USART2 | /dev/ttyS1 | TELEM3 (J4)                              |
| USART3 | /dev/ttyS2 | 调试控制台 (J2)                          |
| UART4  | /dev/ttyS3 | 扩展UART (J6)                            |
| UART5  | /dev/ttyS4 | TELEM2，主VOXL通信 (J1)                  |
| USART6 | /dev/ttyS5 | RC (J12)                                 |
| UART7  | /dev/ttyS6 | TELEM1 (J5)                              |
| UART8  | /dev/ttyS7 | N/A                                      |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 支持

请访问[ModalAI论坛](https://forum.modalai.com/category/10/flight-core)获取更多信息。
