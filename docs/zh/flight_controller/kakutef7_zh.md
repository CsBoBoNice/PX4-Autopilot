# Holybro Kakute F7（已停产）

<Badge type="info" text="已停产" />

:::warning
此机架已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://holybro.com/)获取硬件支持或合规问题。
:::

来自Holybro的_Kakute F7_是为竞速机设计的飞行控制器板。

<img src="../../assets/flight_controller/kakutef7/board.jpg" width="400px" title="Kakute F7" />

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 主要特性

- 主系统芯片：[STM32F745VGT6](https://www.st.com/en/microcontrollers-microprocessors/stm32f745vg.html)
  - CPU：216 MHz ARM Cortex M7，带单精度FPU
  - RAM：320 KB SRAM
  - 闪存：1 MB
- 标准竞速机外形：36x36 mm，标准30.5 mm孔距
- ICM20689加速度计/陀螺仪（软安装）
- BMP280气压计
- microSD（用于日志记录）
- 6个UART
- 1个I2C总线
- 6个PWM输出
- 内置OSD芯片（AB7456，通过SPI）

## 购买地点

该板可以从以下商店之一购买（例如）：

- [getfpv](https://www.getfpv.com/holybro-kakute-f7-tekko32-f3-metal-65a-4-in-1-esc-combo.html)

:::tip
_Kakute F7_设计用于与_Tekko32_ 4合1 ESC配合使用，它们可以组合购买。
:::

## 连接器和引脚

这是_Kakute F7_的丝印，显示板的顶部：

![Kakute F7丝印](../../assets/flight_controller/kakutef7/silk.png)

| 引脚     | 功能                                                    | PX4默认             |
| -------- | ------------------------------------------------------- | ------------------- |
| B+       | 电池正极电压（2S-6S）                                   |                     |
| 5V       | 5V输出（最大2A）                                        |                     |
| VO       | 视频输出到视频发射器                                    |                     |
| VI       | 来自FPV摄像头的视频输入                                 |                     |
| G 或 GND | 地线                                                    |                     |
| SDA, SCL | I2C连接（用于外设）                                     |                     |
| R1, T1   | UART1 RX和TX                                            | TELEM1              |
| R2, T2   | UART2 RX和TX                                            | TELEM2              |
| R3, T3   | UART3 RX和TX                                            | NuttX调试控制台     |
| R4, T4   | UART4 RX和TX                                            | GPS1                |
| R6, T6   | UART6 RX和TX                                            | RC端口              |
| R7, T7   | UART7 RX和TX（RX位于插头中，用于4合1 ESC）              | DShot遥测           |
| LED      | WS2182可寻址LED信号线（未测试）                         |                     |
| Buz-     | 压电蜂鸣器负极（将蜂鸣器正极连接到5V焊盘）              |                     |
| 3V3      | 3.3V输出（最大200 mA）                                  |                     |
| M1到M4   | 电机信号输出（位于插头中，用于4合1 ESC）                |                     |
| M5, M6   | 额外的电机信号输出（位于板的侧面）                      |                     |
| RSI      | 来自接收器的模拟RSSI（0-3.3V）输入                      |                     |
| Boot     | 引导加载程序按钮                                        |                     |

<a id="bootloader"></a>

## PX4引导加载程序更新

该板预装了[Betaflight](https://github.com/betaflight/betaflight/wiki)。
在安装PX4固件之前，必须刷写_PX4引导加载程序_。
下载[kakutef7_bl.hex](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/kakutef7/kakutef7_bl_0b3fbe2da0.hex)引导加载程序二进制文件，并阅读[此页面](../advanced_config/bootloader_update_from_betaflight.md)了解刷写说明。

## 构建固件

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make holybro_kakutef7_default
```

## 安装PX4固件

固件可以通过任何正常方式安装：

- 构建和上传源代码
  ```
  make holybro_kakutef7_default upload
  ```
- 使用_QGroundControl_[加载固件](../config/firmware.md)。
  您可以使用预构建的固件或您自己的自定义固件。

## 配置

如果您使用带有Betaflight/Cleanflight电机分配的4合1 ESC，您可以使用[执行器](../config/actuators.md)配置UI来适当地设置电机顺序。

除了[基本配置](../config/index.md)之外，以下参数很重要：

| 参数                                                                 | 设置                                                                        |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| [SYS_HAS_MAG](../advanced_config/parameter_reference.md#SYS_HAS_MAG) | 这应该被禁用，因为板没有内部磁力计。如果您连接外部磁力计，可以启用它。     |

## 串口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| USART1 | /dev/ttyS0 | TELEM1                |
| USART2 | /dev/ttyS1 | TELEM2                |
| USART3 | /dev/ttyS2 | 调试控制台            |
| UART4  | /dev/ttyS3 | GPS1                  |
| USART6 | /dev/ttyS4 | RC SBUS               |
| UART7  | /dev/ttyS5 | ESC遥测（DShot）      |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 调试端口

### 系统控制台

UART3 RX和TX配置为[系统控制台](../debug/system_console.md)使用。

### SWD

[SWD接口](../debug/swd_debug.md)（JTAG）引脚为：

- `SWCLK`：测试点2（CPU上的引脚72）
- `SWDIO`：测试点3（CPU上的引脚76）
- `GND`：如板上标记
- `VDD_3V3`：如板上标记

这些如下图所示。

![Kakute F7上的SWD引脚 - CLK SWO](../../assets/flight_controller/kakutef7/debug_swd_port.jpg) ![Kakute F7上的SWD引脚：GND和VDD_3V3](../../assets/flight_controller/kakutef7/debug_swd_port_gnd_vcc3_3.jpg)
