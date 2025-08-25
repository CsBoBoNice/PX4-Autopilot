# CUAV X7 飞行控制器（已停产）

<Badge type="info" text="已停产" /> <!-- 202507 / PX4v1.16 -->

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再商业化销售。
已被 [CUAV X7+](https://doc.cuav.net/controller/x7/en/) 取代。
:::

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://www.cuav.net)。
:::

[X7](https://doc.cuav.net/controller/x7/en/)<sup>&reg;</sup> 飞行控制器是一款高性能自驾仪。
它是工业无人机和大型重载无人机的理想选择。
主要供应给商业制造商。

![CUAV x7](../../assets/flight_controller/cuav_x7/x7.jpg)

该飞行控制器采用模块化设计，可与不同基板匹配。
您可以为您的无人机设计专用载板，以提高商业系统的集成度，减少接线，提高系统可靠性，增强您的无人机竞争力（例如，在载板中集成空速传感器、遥测甚至伴随计算机）。
CUAV 还提供了多种载板供您选择。

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 特点

- 内部减震
- 模块化设计，可 DIY 载板
- 支持 USB_HS，下载日志更快（PX4 尚未支持）
- 支持更多 DShot 输出
- 支持 IMU 加热，使传感器工作更好
- 专用 CAN 电池端口
- 3 组 IMU 传感器
- 车规级 RM3100 指南针
- 高性能处理器

:::tip
制造商 [CUAV 文档](https://doc.cuav.net/flight-controller/x7/en/) 是 X7 的权威参考。
应优先使用它们，因为它们包含最完整和最新的信息。
:::

## 快速总结

- 主 FMU 处理器：STM32H743
- 板载传感器：
  - 加速度计/陀螺仪：ICM-20689
  - 加速度计/陀螺仪：ICM-20649
  - 加速度计/陀螺仪：BMI088
  - 磁力计：RM3100
  - 气压计：MS5611\*2

- 接口：
  - 14 个 PWM 输出（12 个支持 Dshot）
  - 支持多种 RC 输入（SBUs / CPPM / DSM）
  - 模拟/PWM RSSI 输入
  - 2 个 GPS 端口（GPS 和 UART4 端口）
  - 4 个 i2c 总线（两个 i2c 专用端口）
  - 2 个 CAN 总线端口
  - 2 个电源端口（Power A 是通用 adc 接口，Power C 是 DroneCAN 电池接口）
  - 2 个 ADC 输入
  - 1 个 USB 端口
- 电源系统：
  - 电源：4.3~5.4V
  - USB 输入：4.75~5.25V
  - 舵机导轨输入：0~36V
- 重量和尺寸：
  - 重量：101 g
- 其他特征：
  - 工作温度：-20 ~ 80°c（测量值）
  - 三个 IMU
  - 支持温度补偿
  - 内部减震

::: info
当运行 PX4 固件时，只有 8 个 PWM 工作，其余 6 个 PWM 仍在适配中，因此现在与 VOLT 不兼容。
:::

## 购买地点

[CUAV 商店](https://store.cuav.net)

[CUAV aliexpress](https://www.aliexpress.com/item/4001042683738.html?spm=a2g0o.detail.1000060.2.1ebb2a9d3WDryi&gps-id=pcDetailBottomMoreThisSeller&scm=1007.13339.169870.0&scm_id=1007.13339.169870.0&scm-url=1007.13339.169870.0&pvid=f0df2481-1c0a-44eb-92a4-9c11c6cb3d06&_t=gps-id:pcDetailBottomMoreThisSeller,scm-url:1007.13339.169870.0,pvid:f0df2481-1c0a-44eb-92a4-9c11c6cb3d06,tpp_buckets:668%230%23131923%2320_668%23808%234094%23518_668%23888%233325%2319_668%234328%2319934%23630_668%232846%238115%23807_668%232717%237566%23827_668%231000022185%231000066058%230_668%233468%2315607%2376)

## 连接（接线）

[CUAV X7 接线快速入门](https://doc.cuav.net/controller/x7/en/quick-start/quick-start-x7-plus.html)

## 尺寸和引脚分布

![CUAV x7](../../assets/flight_controller/cuav_x7/x7-size.jpg)

![X7 pinouts](../../assets/flight_controller/cuav_x7/x7-pinouts.jpg)

:::warning
`RCIN` 端口仅限于为 RC 接收器供电，不能连接任何电源/负载。
:::

## 电压额定值

如果提供三个电源，_X7 自驾仪_ 可在电源上实现三重冗余。
电源导轨是：**POWERA**、**POWERC** 和 **USB**。

::: info
输出电源导轨 **PWM OUT**（0V 至 36V）不为飞行控制器板供电（也不由其供电）。
您必须向 **POWERA**、**POWERC** 或 **USB** 之一供电，否则板卡将无电源。
:::

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWERA** 和 **POWERC** 输入（4.3V 至 5.4V）
2. **USB** 输入（4.75V 至 5.25V）

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make cuav_x7pro_default
```

## 过电流保护

_X7_ 在 5 伏外设和 5 伏高功率上具有过电流保护，将电流限制为 2.5A。
_X7_ 具有短路保护。

:::warning
最多可向列为引脚 1 的连接器提供 2.5 A（尽管这些连接器额定值仅为 1 A）。
:::

## 调试端口

系统的串行控制台和 SWD 接口在 **DSU7** 端口上运行。
只需将 FTDI 线缆连接到 DSU7 连接器（产品列表包含 CUAV FTDI 线缆）。

![Debug port (DSU7)](../../assets/flight_controller/cuav_v5_plus/debug_port_dsu7.jpg)

[PX4 系统控制台](../debug/system_console.md) 和 [SWD 接口](../debug/swd_debug.md) 在 **FMU 调试** 端口（`DSU7`）上运行。

调试端口（`DSU7`）使用 [JST BM06B](https://www.digikey.com.au/en/products/detail/jst-sales-america-inc/BM06B-GHS-TBT-LF-SN-N/807850) 连接器，具有以下引脚分布：

| 引脚      | 信号           | 电压  |
| --------- | -------------- | ----- |
| 1 (红色)  | 5V+            | +5V   |
| 2 (黑色)  | DEBUG TX (OUT) | +3.3V |
| 3 (黑色)  | DEBUG RX (IN)  | +3.3V |
| 4 (黑色)  | FMU_SWDIO      | +3.3V |
| 5 (黑色)  | FMU_SWCLK      | +3.3V |
| 6 (黑色)  | GND            | GND   |

CUAV 提供专用调试线缆，可连接到 `DSU7` 端口。
这分出一根 FTDI 线缆用于将 [PX4 系统控制台](../debug/system_console.md) 连接到计算机 USB 端口，以及用于 SWD/JTAG 调试的 SWD 引脚。
提供的调试线缆不连接到 SWD 端口 `Vref` 引脚（1）。

![CUAV Debug cable](../../assets/flight_controller/cuav_v5_plus/cuav_v5_debug_cable.jpg)

:::warning
SWD Vref 引脚（1）使用 5V 作为 Vref，但 CPU 运行在 3.3V！

一些 JTAG 适配器（SEGGER J-Link）将使用 Vref 电压来设置 SWD 线路上的电压。
对于直接连接到 _Segger Jlink_，我们建议您使用标记为 `DSM`/`SBUS`/`RSSI` 的连接器引脚 4 的 3.3 伏为 JTAG 提供 `Vtref`（即提供 3.3V 而_不是_ 5V）。
:::

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/固定翼/地面车辆或船只。
完整的支持配置可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [CUAV 文档](https://doc.cuav.net/)
- [x7 原理图](https://github.com/cuav/hardware/tree/master/X7_Autopilot)
