# Holybro Kakute H743-Wing 

<Badge type="tip" text="PX4 v1.16" />

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://holybro.com/)。
:::

[Holybro Kakute H743 Wing](https://holybro.com/products/kakute-h743-wing) 是一款功能齐全的飞行控制器，专门针对固定翼和 VTOL 应用。它配备运行在 480 MHz 的 STM32 H743 处理器和 CAN Bus 支持，同时具备双摄像头支持和切换、ON/OFF 维修开关、5V、6V/8V、9V/12 BEC，以及即插即用的 GPS、CAN、I2C 端口。

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 购买地点

该板卡可以从以下商店购买（例如）：

- [Holybro](https://holybro.com/products/kakute-h743-wing)

## 连接器和引脚

| 引脚             | 功能                              | PX4 默认                   |
| ---------------- | --------------------------------- | -------------------------- |
| GPS 1            | USART1 和 I2C1                   | GPS1                       |
| R2, T2           | USART2 RX 和 TX                  | GPS2                       |
| R3, T3           | USART3 RX 和 TX                  | TELEM1                     |
| R5, T5           | USART5 RX 和 TX                  | TELEM2                     |
| R6, T6           | USART6 RX 和 TX                  | RC（PPM、SBUS 等）输入     |
| R7, T7, RTS, CTS | 带流量控制的 UART7 RX 和 TX      | TELEM3                     |
| R8, T8           | UART8 RX 和 TX                   | 控制台                     |
| Buz-, Buz+       | 压电蜂鸣器                        |                            |
| M1 到 M14        | 电机信号输出                      |                            |

## PX4 引导程序更新 {#bootloader}

该板卡预装了 [Betaflight](https://github.com/betaflight/betaflight/wiki)。
在安装 PX4 固件之前，必须刷写 _PX4 引导程序_。
下载 [holybro_kakuteh7-wing.hex](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/kakuteh7-wing/holybro_kakuteh7-wing_bootloader.hex) 引导程序二进制文件，并阅读[此页面](../advanced_config/bootloader_update_from_betaflight.md)获取刷写说明。

## 构建固件

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make holybro_kakuteh7-wing_default
```

## 安装 PX4 固件

::: info
KakuteH7-wing 在 PX4 v1.16 或更新版本中受支持。
在该版本之前，您需要手动构建和安装固件。
:::

固件可以通过任何常规方式手动安装：

- 构建并上传源代码：

  ```
  make holybro_kakuteh7-wing_default upload
  ```

- 使用 _QGroundControl_ [加载固件](../config/firmware.md)。
  您可以使用预构建的固件或您自己的自定义固件。

## 串行端口映射

| UART   | 设备       | 端口                  | 默认功能     |
| ------ | ---------- | --------------------- | ------------ |
| USART1 | /dev/ttyS0 | GPS 1                 | GPS1         |
| USART2 | /dev/ttyS1 | R2, T2                | GPS2         |
| USART3 | /dev/ttyS2 | R3, T3                | TELEM1       |
| UART5  | /dev/ttyS3 | R5, T5                | TELEM2       |
| USART6 | /dev/ttyS4 | R6, (T6)              | RC 输入      |
| UART7  | /dev/ttyS5 | R7, T7, RTS, CTS      | TELEM3       |
| UART8  | /dev/ttyS6 | R8, T8                | 控制台       |

## 调试端口

### 系统控制台

UART8 RX 和 TX 配置为用作[系统控制台](../debug/system_console.md)。