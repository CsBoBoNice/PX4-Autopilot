# MindPX硬件

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](http://mindpx.net)获取硬件支持或合规问题。
:::

AirMind<sup>&reg;</sup> [MindPX](http://mindpx.net)系列是从Pixhawk<sup>&reg;</sup>分支出来的新一代自动驾驶仪系统。

![MindPX控制器](../../assets/hardware/hardware-mindpx.png)

::: info
这些飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 快速摘要

::: info
主要的硬件文档在[这里](http://mindpx.net/assets/accessories/Specification9.18_3_pdf.pdf)。
:::

MindPX是从Pixhawk<sup>&reg;</sup>分支出来的新一代自动驾驶仪系统，在原理图和结构方面进行了修订，并通过新功能进一步增强，使无人驾驶飞行器更智能、更友好。

MindPX将总PWM输出通道增加到16个（8个主输出 + 8个辅助输出）。
这意味着MindPX可以支持更复杂的VTOL配置和更精细的控制。
这对基于FMU-V4的飞行控制器尤其有意义，因为MindPX在单个FMU中实现了主输出和辅助输出。

![](../../assets/hardware/hardware-mindpx-specs.png)

- 主系统芯片：STM32F427
  - CPU：32位，168 MHz ARM Cortex<sup>&reg;</sup> M4，带FPU
  - RAM：256 KB SRAM
  - 2MB闪存
  - ST Micro LSM303D 14位加速度计/磁力计
  - MEAS MS5611气压计
  - InvenSense<sup>&reg;</sup> MPU6500集成6轴传感器

- 亮点特性：
  - CNC加工铝合金外壳，轻巧坚固
  - 内置隔离IMU冗余
  - 总共16个PWM输出通道（8个主 + 8个辅助）
  - 1个额外的I2C端口用于光流连接
  - 1个额外的USB端口用于伴随计算机连接（内置UART转USB转换器）
  - 暴露的调试端口用于开发

## 快速入门

### 安装

![MindPX安装](../../assets/hardware/hardware-mindpx-mounting.png)

### 接线

![MindPX接线1](../../assets/hardware/hardware-mindpx-wiring1.png)

![MindPX接线2](../../assets/hardware/hardware-mindpx-wiring2.png)

### 引脚

![MindPX引脚图](../../assets/hardware/hardware-mindpx-pin.png)

| 编号 |           描述            | 编号 |        描述         |
| :--: | :-----------------------: | :--: | :-----------------: |
|  1   |           电源            |  9   |   I2C2 (MindFLow)   |
|  2   | 调试（刷新引导加载程序）  |  10  | USB2（串口2转USB）  |
|  3   |   USB1（刷新固件）        |  11  |      UART4,5        |
|  4   |           复位            |  12  |  UART1（遥测）      |
|  5   |       UART3（GPS）        |  13  |        CAN          |
|  6   |  I2C1（外部指南针）       |  14  |        ADC          |
|  7   |        TF卡插槽           |  15  |      三色指示灯     |
|  8   | NRF/SPI（遥控）           |  16  |       环路器        |

### 无线电接收器

MindPX支持多种无线电接收器（从V2.6开始），包括：PPM/SBUS/DSM/DSM2/DSMX。
MindPX还支持FrSky<sup>&reg;</sup>双向遥测D和S.Port。

有关详细的引脚图，请参考[用户指南](http://mindpx.net/assets/accessories/UserGuide9.18_2_pdf.pdf)。

### 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make airmind_mindpx-v2_default
```

### 伴随PC连接

MindPX板上有一个USB转UART桥接IC。
使用micro-USB到USB Type A线缆进行连接。
将micro-USB端连接到MindPX的"OBC"端口，将USB Type A端连接到伴随计算机。

最大波特率与px4系列相同，最高可达921600。

## 用户指南

::: info
用户指南在[这里](http://mindpx.net/assets/accessories/UserGuide9.18_2_pdf.pdf)。
:::

## 购买地点

MindRacer可在[AirMind商店](https://airmind.mindpx.net/catalog)购买。
您也可以在Amazon<sup>&reg;</sup>或eBay<sup>&reg;</sup>上找到MindRacer。

## 串口映射

| UART   | 设备       | 端口          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | RC            |
| USART2 | /dev/ttyS1 | TELEM1        |
| USART3 | /dev/ttyS2 | TELEM2        |
| UART4  | /dev/ttyS3 | GPS1          |
| USART6 | /dev/ttyS4 | ?             |
| UART7  | /dev/ttyS5 | 调试控制台    |
| UART8  | /dev/ttyS6 | ?             |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 支持

请访问http://www.mindpx.org获取更多信息。
或者您可以发送电子邮件至[support@mindpx.net](mailto:support@mindpx.net)进行任何咨询或寻求帮助。
