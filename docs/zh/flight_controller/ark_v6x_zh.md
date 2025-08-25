# ARK Electronics ARKV6X

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://arkelectron.com/contact-us/)获取硬件支持或合规问题。
:::

美国制造的[ARKV6X](<(https://arkelectron.gitbook.io/ark-documentation/flight-controllers/arkv6x)>)飞行控制器基于[FMUV6X和Pixhawk自动驾驶仪总线开源标准](https://github.com/pixhawk/Pixhawk-Standards)。

通过三重同步IMU，可以实现数据平均、投票和过滤。
Pixhawk自动驾驶仪总线（PAB）外形使ARKV6X能够在任何[PAB兼容载板](../flight_controller/pixhawk_autopilot_bus.md)上使用，例如[ARK Pixhawk自动驾驶仪总线载板](../flight_controller/ark_pab.md)。

![ARKV6X主要图片](../../assets/flight_controller/arkv6x/ark_v6x_front.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 购买地点

从[Ark Electronics](https://arkelectron.com/product/arkv6x/)订购（美国）

## 传感器

- [双Invensense ICM-42688-P IMU](https://invensense.tdk.com/products/motion-tracking/6-axis/icm-42688-p/)
- [Invensense IIM-42652工业级IMU](https://invensense.tdk.com/products/smartindustrial/iim-42652/)
- [Bosch BMP390气压计](https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp390/)
- [Bosch BMM150磁力计](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bmm150-ds001.pdf)

## 微处理器

- [STM32H743IIK6 MCU](https://www.st.com/en/microcontrollers-microprocessors/stm32h743ii.html)
  - 480MHz
  - 2MB闪存
  - 1MB内存

## 其他特性

- FRAM
- [Pixhawk自动驾驶仪总线（PAB）外形尺寸](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)
- LED指示灯
- MicroSD插槽
- 美国制造
- 设计有1W加热器。在极端条件下保持传感器温暖

## 电源要求

- 5V
- 500mA
  - 主系统300mA
  - 加热器200mA

## 其他信息

- 重量：5.0克
- 尺寸：3.6 x 2.9 x 0.5厘米

## 引脚图

有关ARKV6X的引脚图，请参见[DS-10 Pixhawk自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)

## 串口映射

| UART   | 设备       | 端口          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS           |
| USART2 | /dev/ttyS1 | TELEM3        |
| USART3 | /dev/ttyS2 | 调试控制台     |
| UART4  | /dev/ttyS3 | UART4 & I2C   |
| UART5  | /dev/ttyS4 | TELEM2        |
| USART6 | /dev/ttyS5 | PX4IO/RC      |
| UART7  | /dev/ttyS6 | TELEM1        |
| UART8  | /dev/ttyS7 | GPS2          |

## 构建固件

```sh
make ark_fmu-v6x_default
```

## 另请参阅

- [ARK Electronics ARKV6X](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/arkv6x) (ARK文档)
