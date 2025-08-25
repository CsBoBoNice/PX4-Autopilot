# ModalAI VOXL Flight

<Badge type="info" text="已停产" /> <Badge type="tip" text="PX4 v1.11" />

:::warning
此机架已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://forum.modalai.com/)获取硬件支持或合规问题。
:::

ModalAI VOXL Flight是首批将Snapdragon的强大功能和复杂性与STM32F7上PX4的灵活性和易用性相结合的计算平台之一。
VOXL Flight在美国制造，在单个PCB上支持避障和GPS拒止（室内）导航融合PX4飞行控制器。

![VOXL-Flight](../../assets/flight_controller/modalai/voxl_flight/voxl-flight-dk.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 规格

### 系统

| 特性   | 详细信息 |
| :----- | :------- |
| 重量   | 26g      |

### 伴随计算机

| 特性                   | 详细信息                                                                                                                                                                                                                                                           |
| :--------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 基础操作系统           | Linux Yocto Jethro，3.18内核。可以通过在VOXL上运行Docker使用其他Linux操作系统，详情[这里](https://docs.modalai.com/docker-on-voxl/)                                                                                                                               |
| 计算                   | Qualcomm Snapdragon 821，4GB LPDDR4 1866MHz，Snapdragon 821 [数据表](https://developer.qualcomm.com/download/sd820e/qualcomm-snapdragon-820e-processor-apq8096sge-device-specification.pdf)，[文档](https://developer.qualcomm.com/hardware/apq-8096sg/tools) |
| CPU                    | 四核CPU，最高2.15GHz                                                                                                                                                                                                                                               |
| GPU                    | Adreno 530 GPU，624MHz                                                                                                                                                                                                                                             |
| 计算DSP                | Hexagon计算DSP（cDSP）825MHz                                                                                                                                                                                                                                       |
| 传感器DSP              | Hexagon传感器DSP（sDSP）700MHz                                                                                                                                                                                                                                      |
| 视频                   | 4k30视频捕获h.264/5，720p FPV                                                                                                                                                                                                                                      |
| 摄像头接口             | 支持MIPI-CSI2、USB UVC、HDMI                                                                                                                                                                                                                                       |
| Wi-Fi                  | 预认证Wi-Fi模块[QCNFA324 FCC ID:PPD-QCNFA324](https://fccid.io/PPD-QCNFA324)，QCA6174A调制解调器，802.11ac 2x2双频，蓝牙4.2（双模式）                                                                                                                            |
| 4G LTE                 | [可选附加模块](https://www.modalai.com/collections/voxl-add-ons/products/voxl-lte)                                                                                                                                                                                 |
| Microhard pDDL         | [可选附加模块](https://www.modalai.com/collections/voxl-add-ons/products/voxl-microhard-modem-usb-hub)                                                                                                                                                             |
| GNSS                   | WGR7640 10Hz                                                                                                                                                                                                                                                       |
| I/O                    | 1个USB3.0 OTG（ADB端口），1个USB2.0（扩展端口），2个UART，3个I2C，可配置额外的GPIO和SPI                                                                                                                                                                           |
| 存储                   | 32GB（UFS 2.0），Micro SD卡                                                                                                                                                                                                                                       |
| 软件                   | Docker、OpenCV 2.4.11、3.4.6、4.2、ROS Indigo、Qualcomm机器视觉SDK，参见[GitLab](https://gitlab.com/voxl-public)获取大量开源示例！                                                                                                                               |
| IMU                    | ICM-42688（SPI10），ICM-20948（SPI1）                                                                                                                                                                                                                              |
| 气压计                 | BMP280                                                                                                                                                                                                                                                             |

### 飞行控制器

| 特性             | 详细信息                                                      |
| :--------------- | :------------------------------------------------------------ |
| MCU              | 216MHz，32位ARM M7 [STM32F765II][stm32f765ii]                |
| 内存             | 256Kb FRAM                                                    |
|                  | 2Mbit闪存                                                     |
|                  | 512Kbit SRAM                                                  |
| 固件             | [PX4][px4]                                                    |
| IMU              | [ICM-20602][icm-20602]（SPI1）                                |
|                  | ICM-42688（SPI2）                                             |
|                  | [BMI088][bmi088]（SPI6）                                      |
| 气压计           | [BMP388][bmp388]（I2C4）                                      |
| 安全元件         | [A71CH][a71ch]（I2C4）                                        |
| microSD卡        | [支持的卡信息](../dev_log/logging.md#sd-cards)               |
| 输入             | GPS/磁力计                                                    |
|                  | Spektrum                                                      |
|                  | 遥测                                                          |
|                  | CAN总线                                                       |
|                  | PPM                                                           |
| 输出             | 6个LED（2个RGB）                                             |
|                  | 8个PWM通道                                                    |
| 额外接口         | 3个串口                                                       |
|                  | I2C                                                           |
|                  | GPIO                                                          |

<!-- reference links for above table (improve layout) -->

[stm32f765ii]: https://www.st.com/en/microcontrollers-microprocessors/stm32f765ii.html
[px4]: https://github.com/PX4/PX4-Autopilot/tree/main/boards/modalai/fc-v1
[icm-20602]: https://invensense.tdk.com/products/motion-tracking/6-axis/icm-20602/
[bmi088]: https://www.bosch-sensortec.com/products/motion-sensors/imus/bmi088/
[bmp388]: https://www.adafruit.com/product/3966
[a71ch]: https://www.nxp.com/products/security-and-authentication/authentication/plug-and-trust-the-fast-easy-way-to-deploy-secure-iot-connections:A71CH

::: info
更详细的硬件文档可以在[这里](https://docs.modalai.com/voxl-flight-datasheet/)找到。
:::

## 尺寸

![FlightCoreV1Dimensions](../../assets/flight_controller/modalai/voxl_flight/voxl-flight-dimensions.jpg)

[3D STEP文件](https://storage.googleapis.com/modalai_public/modal_drawings/M0019_VOXL-Flight.zip)

## PX4固件兼容性

_VOXL Flight_与PX4 v1.11的官方PX4固件完全兼容。

ModalAI维护PX4 v1.11的[分支PX4版本](https://github.com/modalai/px4-firmware/tree/modalai-1.11)。
这包括UART ESC支持以及计划上游的VIO和VOA改进。

有关固件的更多信息可以在[这里](https://docs.modalai.com/flight-core-firmware/)找到。

## QGroundControl支持

此板在QGroundControl 4.0及更高版本中受支持。

## 可用性

不再可用。

## 快速入门

供应商的快速入门指南位于[这里](https://docs.modalai.com/voxl-flight-quickstart/)。

### voxl-vision-px4

VOXL Flight在硬件的伴随计算机部分运行[voxl-vision-px4](https://gitlab.com/voxl-public/modal-pipe-architecture/voxl-vision-px4)，作为一种MAVLink代理。
有关详细信息，源代码可在[这里](https://gitlab.com/voxl-public/modal-pipe-architecture/voxl-vision-px4)获得

### 连接器

有关引脚排列的详细信息可以在[这里](https://docs.modalai.com/voxl-flight-datasheet-connectors/)找到。

#### 顶部

![VOXLFlightTop](../../assets/flight_controller/modalai/voxl_flight/voxl-flight-top.jpg)

_注意：1000系列连接器可从STM32/PX4访问_

| 连接器 | 摘要                                   | 使用者                            |
| ------ | -------------------------------------- | --------------------------------- |
| J2     | 高分辨率4k图像传感器（CSI0）           | Snapdragon - Linux                |
| J3     | 立体图像传感器（CSI1）                 | Snapdragon - Linux                |
| J6     | 冷却风扇连接器                         | Snapdragon - Linux                |
| J7     | BLSP6（GPIO）和BLSP9（UART）           | Snapdragon - Linux                |
| J13    | 扩展B2B                                | Snapdragon - Linux                |
| J14    | 集成GNSS天线连接                       | Snapdragon - Linux                |
| J1001  | 编程和调试/UART3                       | STM32 - PX4                       |
| J1002  | UART ESC，UART2/TELEM3                 | STM32 - PX4                       |
| J1003  | PPM RC输入                             | STM32 - PX4                       |
| J1004  | RC输入，Spektrum/SBus/UART6            | STM32 - PX4                       |
| J1006  | USB 2.0连接器（PX4/QGroundControl）    | STM32 - PX4                       |
| J1007  | 8通道PWM/DShot输出                     | STM32 - PX4                       |
| J1008  | CAN总线                                | STM32 - PX4                       |
| J1009  | I2C3，UART4                            | STM32 - PX4                       |
| J1010  | 遥测（TELEM1）                         | STM32 - PX4                       |
| J1011  | I2C2，安全按钮输入                     | STM32 - PX4                       |
| J1012  | 外部GPS和磁力计，UART1，I2C1           | STM32 - PX4                       |
| J1013  | 电源输入，I2C3                         | STM32 - PX4（为整个系统供电）     |

#### 底部

![VOXLFlightBottom](../../assets/flight_controller/modalai/voxl_flight/voxl-flight-bottom.jpg)

_注意：1000系列连接器可从STM32/PX4访问_

| 连接器         | 摘要                                    | 使用者                      |
| -------------- | --------------------------------------- | --------------------------- |
| J4             | 跟踪/光流图像传感器（CSI2）             | Snapdragon - Linux          |
| J8             | USB 3.0 OTG                             | Snapdragon - Linux，**adb** |
| J10            | BLSP7 UART和I2C板外                     | Snapdragon - Linux          |
| J11            | BLSP12 UART和I2C板外                    | Snapdragon - Linux          |
| VOXL microSD   |                                         | Snapdragon - Linux          |
| PX4 microSD    | 最大32Gb                                | STM32 - PX4                 |
| Wi-Fi天线      | 包含                                    | Snapdragon - Linux          |

### 用户指南

完整的用户指南可在[这里](https://docs.modalai.com/voxl-flight-quickstart)获取。

### 如何构建

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make modalai_fc-v1
```

## 串口映射

_注意：显示的映射仅适用于PX4控制的接口_

| UART   | 设备       | 端口                                    |
| ------ | ---------- | --------------------------------------- |
| USART1 | /dev/ttyS0 | GPS1（J1012）                           |
| USART2 | /dev/ttyS1 | TELEM3（J1002）                         |
| USART3 | /dev/ttyS2 | 调试控制台（J1001）                     |
| UART4  | /dev/ttyS3 | 扩展UART（J6）                          |
| UART5  | /dev/ttyS4 | PX4和伴随计算机之间的UART               |
| USART6 | /dev/ttyS5 | RC（J1004）                             |
| UART7  | /dev/ttyS6 | TELEM1（J1010）                         |
| UART8  | /dev/ttyS7 | N/A                                     |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 支持

请访问[ModalAI论坛](https://forum.modalai.com/category/8/voxl-flight)获取更多信息。
