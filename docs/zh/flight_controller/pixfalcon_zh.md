# Pixfalcon飞行控制器（已停产）

<Badge type="info" text="已停产" px4_current="v1.15" year="2024"/>

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://holybro.com/)获取硬件支持或合规问题。
:::

Pixfalcon自动驾驶仪（由[Holybro<sup>&reg;</sup>](https://holybro.com/)设计）是[Pixhawk 1](../flight_controller/pixhawk.md)设计的二进制兼容（FMUv2）衍生产品，专为空间受限的应用（如FPV竞速机）进行了优化。它减少了IO数量以实现尺寸缩减。

![Pixfalcon主图](../../assets/hardware/hardware-pixfalcon.png)

## 快速摘要

- 主系统芯片：[STM32F427](https://www.st.com/en/microcontrollers-microprocessors/stm32f427-437.html)
  - CPU：180 MHz ARM<sup>&reg;</sup> Cortex<sup>&reg;</sup> M4，带单精度FPU
  - RAM：256 KB SRAM (L1)
- 故障安全系统芯片：STM32F100
  - CPU：24 MHz ARM Cortex M3
  - RAM：8 KB SRAM
- GPS：u-blox<sup>&reg;</sup> M8（捆绑）

### 连接性

- 1个I2C
- 2个UART（一个用于遥测/OSD，无流控制）
- 8个带手动覆盖的PWM
- S.BUS / PPM输入

## 可用性：

不再可用。

可选硬件：

- 光流：来自制造商[Holybro](https://holybro.com/products/px4flow)的PX4 Flow单元
- 来自制造商[Holybro](https://holybro.com/products/digital-air-speed-sensor-ms4525do)的数字空速传感器
- 带集成遥测的屏幕显示：
  - 带屏幕显示（OSD）单元的Micro HKPilot遥测无线电模块 - 433MHz。（已停产）
- 纯遥测选项：
  - [SIK无线电](../telemetry/sik_radio.md)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v2_default
```

## 调试端口

此板没有调试端口（即它没有用于访问[系统控制台](../debug/system_console.md)或[SWD接口](../debug/swd_debug.md)（JTAG）的端口）。

开发人员需要将导线焊接到板的测试焊盘上用于SWD，以及焊接到STM32F4（IC）的TX和RX来获取控制台。

## 串口映射

| UART   | 设备       | 端口                     |
| ------ | ---------- | ------------------------ |
| UART1  | /dev/ttyS0 | IO调试                   |
| USART2 | /dev/ttyS1 | TELEM1（无流控制）       |
| UART4  | /dev/ttyS2 | GPS                      |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->
