# Holybro Kakute H7 V2

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://holybro.com/)获取硬件支持或合规问题。
:::

[Holybro Kakute H7 V2](https://holybro.com/products/kakute-h7-v2)飞行控制器功能齐全，包括集成蓝牙、高清摄像头插头、双即插即用4合1 ESC端口、9V VTX开/关维修开关、气压计、OSD、6个UART、128MB闪存用于日志记录（PX4尚不支持）、5V和9V BEC，以及更大的焊接焊盘，布局简单等等。

Kakute H7v2建立在其前身[Kakute F7](../flight_controller/kakutef7.md)和[Kakute H7](../flight_controller/kakuteh7.md)的最佳特性基础上。

该板还具有板载气压计、LED和蜂鸣器焊盘，以及用于外部GPS/磁力计的I2C焊盘（SDA和SCL）。

<img src="../../assets/flight_controller/kakuteh7v2/kakuteh7v2_top.png" width="300px" title="KakuteH7V2顶部图像" /> <img src="../../assets/flight_controller/kakuteh7v2/kakuteh7v2_bottom.png" width="300px" title="KakuteH7V2底部图像" />

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 主要特性

- MCU：STM32H743 32位处理器，运行在480 MHz
- IMU：BMI270
- 气压计：BMP280
- OSD：AT7456E
- 板载蓝牙芯片：在PX4中禁用
- VTX开/关维修开关：PX4不使用
- 6个UART（1,2,3,4,6,7；UART2用于蓝牙遥测）
- 9个PWM输出（8个电机输出，1个LED）
- 2个JST-SH1.0_8pin端口（用于单个或4合1 ESC，x8/八旋翼即插即用兼容）
- 1个JST-GH1.5_6pin端口（用于高清系统，如Caddx Vista和Air Unit）
- 电池输入电压：2S-8S
- BEC 5V 2A连续
- BEC 9V 1.5A连续
- 安装：30.5 x 30.5mm/Φ4mm孔，带Φ3mm护套
- 尺寸：35x35mm
- 重量：8g

## 购买地点

该板可以从以下商店之一购买（例如）：

- [Holybro](https://holybro.com/products/kakute-h7-v2)

:::tip
_Kakute H7v2_设计用于与_Tekko32_ 4合1 ESC配合使用，它们可以组合购买。
:::

## 连接器和引脚

| 引脚     | 功能                                                    | PX4默认             |
| -------- | ------------------------------------------------------- | ------------------- |
| B+       | 电池正极电压（2S-8S）                                   |                     |
| VTX+     | 9V输出                                                  |                     |
| SDA, SCL | I2C连接（用于外设）                                     |                     |
| 5V       | 5V输出（最大2A）                                        |                     |
| 3V3      | 3.3V输出（最大0.25A）                                   |                     |
| VI       | 来自FPV摄像头的视频输入                                 |                     |
| VO       | 视频输出到视频发射器                                    |                     |
| CAM      | 到摄像头OSD控制                                         |                     |
| G 或 GND | 地线                                                    |                     |
| RSI      | 来自接收器的模拟RSSI（0-3.3V）输入                      |                     |
| R1, T1   | UART1 RX和TX                                            | TELEM1              |
| R3, T3   | UART3 RX和TX                                            | NuttX调试控制台     |
| R4, T4   | UART4 RX和TX                                            | GPS1                |
| R6, T6   | UART6 RX和TX（R6也位于GH插头中）                        | RC端口              |
| R7       | UART7 RX（RX位于插头中，用于4合1 ESC）                  | DShot遥测           |
| LED      | WS2182可寻址LED信号线（未测试）                         |                     |
| Z-       | 压电蜂鸣器负极（将蜂鸣器正极连接到5V焊盘）              |                     |
| M1到M4   | 电机信号输出（位于插头中，用于4合1 ESC）                |                     |
| M5到M8   | 电机信号输出（位于插头中，用于4合1 ESC）                |                     |
| Boot     | 引导加载程序按钮                                        |                     |

<a id="bootloader"></a>

## PX4引导加载程序更新

该板预装了[Betaflight](https://github.com/betaflight/betaflight/wiki)。
在安装PX4固件之前，必须刷写_PX4引导加载程序_。
下载[holybro_kakuteh7v2_bootloader.hex](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/kakuteh7v2/holybro_kakuteh7v2_bootloader.hex)引导加载程序二进制文件，并阅读[此页面](../advanced_config/bootloader_update_from_betaflight.md)了解刷写说明。

## 构建固件

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make holybro_kakuteh7v2_default
```

## 安装PX4固件

::: info
KakuteH7v2由PX4 master和PX4 v1.14或更新版本支持。如果您通过QGroundcontrol加载预构建固件，您必须使用QGC Daily或QGC版本新于4.1.7。
在该发布之前，您需要手动构建和安装固件。
:::

固件可以通过任何正常方式手动安装：

- 构建和上传源代码：

  ```
  make holybro_kakuteh7v2_default upload
  ```

- 使用_QGroundControl_[加载固件](../config/firmware.md)。
  您可以使用预构建的固件或您自己的自定义固件。

::: info
KakuteH7v2由PX4 main和v1.14或更新版本支持。
:::

## PX4配置

除了[基本配置](../config/index.md)之外，以下参数很重要：

| 参数                                                                 | 设置                                                                        |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| [SYS_HAS_MAG](../advanced_config/parameter_reference.md#SYS_HAS_MAG) | 这应该被禁用，因为板没有内部磁力计。如果您连接外部磁力计，可以启用它。     |

## 串口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| USART1 | /dev/ttyS0 | TELEM1                |
| USART3 | /dev/ttyS2 | 调试控制台            |
| UART4  | /dev/ttyS3 | GPS1                  |
| USART6 | /dev/ttyS4 | RC SBUS               |
| UART7  | /dev/ttyS5 | ESC遥测（DShot）      |

## 调试端口

### 系统控制台

UART3 RX和TX配置为[系统控制台](../debug/system_console.md)使用。

### SWD

[SWD接口](../debug/swd_debug.md)（JTAG）引脚为：

- `SWCLK`：测试点2（CPU上的引脚72）
- `SWDIO`：测试点3（CPU上的引脚76）
- `GND`：如板上标记
- `VDD_3V3`：如板上标记
