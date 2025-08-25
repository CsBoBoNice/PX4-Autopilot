# CUAV X25-EVO

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://store.cuav.net/)。
:::

_X25-EVO_ 是由 CUAV<sup>&reg;</sup> 制造的先进自驾仪。

该自驾仪推荐用于商业系统集成，但也适合学术研究和任何其他应用。

![X25-EVO AutoPilot - hero image](../../assets/flight_controller/cuav_x25-evo/X25-EVO.jpg)

X25-EVO 在各个方面都为您带来终极性能、稳定性和可靠性。

::: info
这些飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

### 特点

- Arm® Cortex-M7® 处理器（STM32H743XI）带浮点单元（FPU），运行频率 480MHz，具有 2MB Flash 内存。使开发者能够提高生产力和效率，允许更复杂的算法和模型。
- 车规级 RM3100 指南针。专为更好的稳定性和抗干扰能力而设计。
- 位于独立总线上的三重冗余 IMU 和双重冗余气压计。如果 PX4 自驾仪检测到传感器故障，系统会无缝切换到另一个传感器以保持飞行控制可靠性。
- 独立的 LDO 电源控制为每个传感器组供电。减振系统过滤高频振动并降低噪音以确保准确读数，为飞行器提供更好的整体飞行性能。
- 集成 Microchip 以太网 PHY，通过以太网与任务计算机等机载设备进行高速通信。
- 双重温度补偿系统，分别位于 IMU 板和 FMU 板上。温度由机载加热电阻器控制，以达到 IMU 的最佳工作温度。
- PWM 舵机输出电压可在 3.3V 或 5V 之间切换。
- 模块化设计，适用于 DIY 载板。

### 处理器和传感器

- 主处理器：STM32H743XI
  - 32 位 Arm® Cortex®-M7，480MHz，2MB Flash，1MB RAM
- 板载传感器：
  - 加速度计/陀螺仪：IIM42652\*2
  - 加速度计/陀螺仪：IIM42653
  - 磁力计：RM3100
  - 气压计：BMP581
  - 气压计：ICP-20100

### 电气数据

- 额定电压：
  - 输入电压：10~18V
  - USB 电源输入：4.75~5.25V
  - 舵机导轨输入：0~9.9V
- 额定电流：
  - 总输出最大电流：10A
  - TELEM1 和 TELEM2 输出电流限制器：4A
  - CAN1 和 CAN2 输出电流限制器：2.4A
  - 其他端口输出电流限制器：1.5A

### 接口

- 16x PWM 舵机输出
- 1x Spektrum / DSM 和 S.Bus 专用 R/C 输入
- 1x 模拟/PWM RSSI 输入
- 2x TELEM 端口（带完整流量控制）
- 1x UART4 端口
- 2x GPS 端口
  - 1x 完整 GPS 加安全开关端口（GPS1）
  - 1x 基本 GPS 端口（带 I2C，GPS2）
- 1x USB 端口（TYPE-C）
- 1x 以太网端口
  - 无变压器应用
  - 100Mbps
- 3x I2C 总线端口
- 1x SPI 总线
  - 1x 片选线
  - 1x 数据就绪线
  - 1x SPI 复位线
- 5x CAN 端口用于 CAN 外设
  - 3x CAN1 总线复用端口
  - 2x CAN2 总线复用端口
- 2x 电源输入端口
  - DroneCAN/UAVCAN 电源输入
- 2x AD 端口
  - 模拟输入（3.3V）
  - 模拟输入（6.6V - PX4 不支持）
- 1x 专用调试端口
  - FMU 调试

### 机械数据

 - 未提供。

## 购买渠道

从 [CUAV](https://store.cuav.net/) 订购。

## 组装/设置

 - 未提供。

## 引脚定义

 - 未提供。

## 串行端口映射

| UART   | 设备       | 端口          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS1          |
| USART2 | /dev/ttyS1 | GPS2          |
| USART3 | /dev/ttyS2 | 调试控制台    |
| UART4  | /dev/ttyS3 | UART4         |
| UART5  | /dev/ttyS4 | TELEM2        |
| USART6 | /dev/ttyS5 | RC            |
| UART7  | /dev/ttyS6 | TELEM1        |

## 电压额定值

如果提供三个电源，_X25-EVO_ 可在电源上实现三重冗余。三个电源导轨是 POWERC1、POWERC2 和 USB。
- **POWER C1** 和 **POWER C2** 是 DroneCAN/UAVCAN 电池接口。

**正常操作最大额定值**

在这些条件下，所有电源将按以下顺序用于为系统供电：
1. **POWER C1** 和 **POWER C2** 输入（10V 至 18V）
2. USB 输入（4.75V 至 5.25V）

**电压监控**

默认启用数字 DroneCAN/UAVCAN 电池监控。

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)，执行：

```
make cuav_x25-evo_default
```

<a id="debug_port"></a>

## 调试端口

[PX4 系统控制台](../debug/system_console.md) 和 [SWD 接口](../debug/swd_debug.md) 在 **FMU 调试** 端口上运行。

| 引脚      | 信号             | 电压  |
| --------- | ---------------- | ----- |
| 1 (红色)  | 5V+              | +5V   |
| 2 (黑色)  | DEBUG TX (OUT)   | +3.3V |
| 3 (黑色)  | DEBUG RX (IN)    | +3.3V |
| 4 (黑色)  | FMU_SWDIO        | +3.3V |
| 5 (黑色)  | FMU_SWCLK        | +3.3V |
| 6 (黑色)  | GND              | GND   |

## 支持的平台/机架

任何可以使用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/固定翼/地面车辆或船只。完整的支持配置可以在[机架参考](../airframes/airframe_reference.md)中找到。

## 更多信息

- [CUAV 文档](https://doc.cuav.net/)
