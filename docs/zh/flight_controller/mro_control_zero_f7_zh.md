# mRo Control Zero F7飞行控制器

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://store.mrobotics.io/)获取硬件支持或合规问题。
:::

_mRo Control Zero F7<sup>&reg;</sup>_是mRo推出的新型飞行控制器。

![mRo Control Zero F7](../../assets/flight_controller/mro_control_zero_f7/mro_control_zero_f7.jpg)

这是一个毫不妥协的三重IMU商业级飞行控制器。
它包括8个PWM输出（支持DShot）、3个IMU、1个磁力计、1个气压传感器（高度计）、6个UART和SD卡，全部封装在32mm x 20mm的PCB中。
PWM是双向的，具有EMI保护，并且电平转换为5V逻辑电平。
全部通过前后30引脚Molex PicoClasp连接器访问。
包括耐用的塑料外壳、保形板涂层和可选的温度校准。

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 主要特性

- 微处理器：
  - 32位STM32F777 Cortex<sup>&reg;</sup> M4核心，带FPU rev. 3
  - 216 MHz/512 KB RAM/2 MB闪存
  - F-RAM Cypress MF25V02-G 256-Kbit非易失性存储器（执行速度如RAM一样快的闪存）

- 传感器：
  - [Bosch BMI088](https://www.bosch-sensortec.com/products/motion-sensors/imus/bmi088/) 3轴加速度计/陀螺仪（内部振动阻尼）
  - [Invensense ICM-20602](https://invensense.tdk.com/products/motion-tracking/6-axis/icm-20602/) 3轴加速度计/陀螺仪
  - [Invensense ICM-20948](https://invensense.tdk.com/products/motion-tracking/9-axis/icm-20948/) 3轴加速度计/陀螺仪/磁力计
  - [Infineon DPS310气压计](https://www.infineon.com/assets/row/public/documents/24/49/infineon-dps310-datasheet-en.pdf) - [已停产](https://www.infineon.com/part/DPS310)（非常平滑，不再有光敏性）

- 接口：
  - 6个UART（总串口数），3个带硬件流控制，1个FRSky遥测（D或X类型），1个控制台和1个GPS+I2C
  - 8个PWM输出（全部支持DShot）
  - 1个CAN
  - 1个I2C
  - 1个SPI
  - Spektrum DSM / DSM2 / DSM-X®卫星兼容输入和绑定
  - Futaba S.BUS®和S.BUS2®兼容输入
  - FRSky遥测端口输出
  - Graupner SUMD
  - Yuneec ST24
  - PPM和输入信号
  - 1个JTAG（TC2030连接器）
  - 1个RSSI（PWM或电压）输入
  - 三色LED

- 重量和尺寸（未装外壳）：
  - 重量：5.3g（0.19oz）
  - 宽度：20mm（0.79"）
  - 长度：32mm（1.26"）

- 电源系统：
  - 3个超低噪音LDO稳压器

## 购买地点

- [mRo Control Zero](https://store.mrobotics.io/mRo-Control-Zero-F7-p/mro-ctrl-zero-f7.htm)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make mro_ctrl-zero-f7
```

## 调试端口

### 控制台端口

[PX4系统控制台](../debug/system_console.md)在`USART7`上运行，使用下面列出的引脚。
这是一个标准串口引脚排列，设计用于连接[3.3V FTDI](https://www.digikey.com/en/products/detail/TTL-232R-3V3/768-1015-ND/1836393)线缆（5V兼容）。

| mRo control zero f7 |             | FTDI |
| ------------------- | ----------- | ---- | ---------------- |
| 17                  | USART7 Tx   | 5    | FTDI RX（黄色）  |
| 19                  | USART7 Rx   | 4    | FTDI TX（橙色）  |
| 6                   | USART21 GND | 1    | FTDI GND（黑色） |

### SWD端口

用于FMU调试的[SWD端口](../debug/swd_debug.md)（JTAG）是TC2030调试连接器，如下所示。

![mro swd端口](../../assets/flight_controller/mro_control_zero_f7/mro_control_zero_f7_swd.jpg)

您可以使用[Tag Connect](https://www.tag-connect.com/)线缆[TC2030 IDC NL](https://www.tag-connect.com/product/tc2030-idc-nl)（配有相关的[固定夹](https://www.tag-connect.com/product/tc2030-retaining-clip-board-3-pack)）连接到BlackMagic探针或ST-LINK V2调试器。

![tc2030 idc nl线缆](../../assets/flight_controller/mro_control_zero_f7/tc2030_idc_nl.jpg)

还有一个[ARM20-CTX 20引脚到TC2030-IDC适配器](https://www.tag-connect.com/product/arm20-ctx-20-pin-to-tc2030-idc-adapter-for-cortex)，可以与其他调试探针一起使用。

## 引脚图

![mRo Control Zero F7](../../assets/flight_controller/mro_control_zero_f7/mro_control_pinouts.jpg)

## 串口映射

| UART   | 设备       | 端口                                                        |
| ------ | ---------- | ----------------------------------------------------------- |
| USART2 | /dev/ttyS0 | TELEM1（流控制）                                            |
| USART3 | /dev/ttyS1 | TELEM2（流控制）                                            |
| UART4  | /dev/ttyS2 | GPS1                                                        |
| USART6 | /dev/ttyS3 | 弹性端口（可配置为带流控制的SPI或UART）                     |
| UART7  | /dev/ttyS4 | 控制台                                                      |
| UART8  | /dev/ttyS5 | 自由串口（通常用于FrSky遥测）                               |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->
<!-- https://github.com/PX4/PX4-Autopilot/blob/main/boards/mro/ctrl-zero-f7/nuttx-config/nsh/defconfig#L202-L207 -->

## 更多信息

- [介绍新的mRo Control Zero自动驾驶仪](https://mrobotics.io/introducing-the-new-mro-control-zero-autopilot/)（博客）
- [快速入门指南](https://mrobotics.io/mrocontrolzero/)
