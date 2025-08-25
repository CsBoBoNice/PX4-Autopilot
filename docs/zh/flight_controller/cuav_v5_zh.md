# CUAV v5（已停产）

<Badge type="info" text="已停产" /> <!-- 202507 / PX4v1.16 -->

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再商业化销售。
:::

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://store.cuav.net/)。
:::

_CUAV v5_<sup>&reg;</sup>（以前称为"Pixhack v5"）是由 CUAV<sup>&reg;</sup> 设计和制造的先进自驾仪。
该板基于 [Pixhawk 项目](https://pixhawk.org/) **FMUv5** 开源硬件设计。
它在 [NuttX](https://nuttx.apache.org/) 操作系统上运行 PX4，完全兼容 PX4 固件。
主要面向学术和商业开发者。

![CUAV v5](../../assets/flight_controller/cuav_v5/pixhack_v5.jpg)

## 快速总结

- 主 FMU 处理器：STM32F765
  - 32 位 Arm® Cortex®-M7，216MHz，2MB 内存，512KB RAM
- IO 处理器：STM32F100
  - 32 位 Arm® Cortex®-M3，24MHz，8KB SRAM
- 板载传感器：
  - 加速度计/陀螺仪：ICM-20689
  - 加速度计/陀螺仪：BMI055
  - 磁力计：IST8310
  - 气压计：MS5611

- 接口：
  - 8-14 个 PWM 输出（6 个来自 IO，8 个来自 FMU）
  - FMU 上 3 个专用 PWM/捕获输入
  - CPPM 专用 R/C 输入
  - PPM 和 S.Bus 专用 R/C 输入
  - 模拟/PWM RSSI 输入
  - S.Bus 舵机输出
  - 5 个通用串行端口
  - 4 个 I2C 端口
  - 4 个 SPI 总线
  - 2 个带串行 ESC 的 CAN 总线
  - 2 个电池的电压/电流模拟输入
- 电源系统：
  - 电源：4.3~5.4V
  - USB 输入：4.75~5.25V
  - 舵机导轨输入：0~36V
- 重量和尺寸：
  - 重量：90g
  - 尺寸：44x84x12mm
- 其他特征：
  - 工作温度：-20 ~ 80°C（测量值）

## 购买地点

从 [CUAV](https://cuav.taobao.com/index.htm?spm=2013.1.w5002-16371268426.2.411f26d9E18eAz) 订购。

## 连接

![CUAV v5](../../assets/flight_controller/cuav_v5/pixhack_v5_connector.jpg)

:::warning
RCIN 接口仅限于为 RC 接收器供电，不能连接任何电源/负载。
:::

## 电压额定值

如果提供三个电源，_CUAV v5_ 可以在电源上实现三重冗余。三个电源导轨是：**POWER1**、**POWER2** 和 **USB**。

::: info
输出电源导轨 **FMU PWM OUT** 和 **I/O PWM OUT**（0V 至 36V）不为飞行控制器板供电（也不由其供电）。
您必须向 **POWER1**、**POWER2** 或 **USB** 之一供电，否则板卡将无电源。
:::

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER1** 和 **POWER2** 输入（4.3V 至 5.4V）
1. **USB** 输入（4.75V 至 5.25V）

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v5_default
```

## 调试端口

[PX4 系统控制台](../debug/system_console.md) 和 [SWD 接口](../debug/swd_debug.md) 在 **FMU 调试** 端口上运行。
只需将 FTDI 线缆连接到 Debug & F7 SWD 连接器。
要访问 I/O 调试端口，用户必须拆除 CUAV v5 外壳。
两个端口都有标准串行引脚，可以连接到标准 FTDI 线缆（3.3V，但 5V 耐受）。

引脚分布如图所示。

![CUAV v5 debug](../../assets/flight_controller/cuav_v5/pixhack_v5_debug.jpg)

| 引脚 | CUAV v5 调试 |
| ---- | ------------ |
| 1    | GND          |
| 2    | FMU-SWCLK    |
| 3    | FMU-SWDIO    |
| 4    | UART7_RX     |
| 5    | UART7_TX     |
| 6    | VCC          |

## 串行端口映射

| UART   | 设备       | 端口                              |
| ------ | ---------- | --------------------------------- |
| UART1  | /dev/ttyS0 | GPS                               |
| USART2 | /dev/ttyS1 | TELEM1（流量控制）                |
| USART3 | /dev/ttyS2 | TELEM2（流量控制）                |
| UART4  | /dev/ttyS3 | TELEM4                            |
| USART6 | /dev/ttyS4 | TX 是来自 SBUS_RC 连接器的 RC 输入|
| UART7  | /dev/ttyS5 | 调试控制台                        |
| UART8  | /dev/ttyS6 | PX4IO                             |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 外设

- [数字空速传感器](https://item.taobao.com/item.htm?spm=a1z10.3-c-s.w4002-16371268452.37.6d9f48afsFgGZI&id=9512463037)
- [遥测无线电模块](https://cuav.taobao.com/category-158480951.htm?spm=2013.1.w5002-16371268426.4.410b7a821qYbBq&search=y&catName=%CA%FD%B4%AB%B5%E7%CC%A8)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/固定翼/地面车辆或船只。
完整的支持配置可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [FMUv5 参考设计引脚分布](https://docs.google.com/spreadsheets/d/1-n0__BYDedQrc_2NHqBenG1DNepAgnHpSGglke-QQwY/edit#gid=912976165)。
- [CUAV Github](https://github.com/cuav)
