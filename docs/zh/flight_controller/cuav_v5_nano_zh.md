# CUAV V5 nano 自驾仪

:::warning
PX4 不制造此（或任何）自驾仪。
如需硬件支持或合规问题，请联系[制造商](https://store.cuav.net/)。
:::

**V5 nano**<sup>&reg;</sup> 是由 CUAV<sup>&reg;</sup> 与 PX4 团队合作设计的用于空间受限应用的自驾仪。

该自驾仪足够小，可用于 220mm 竞速无人机，但仍然足够强大以满足大多数无人机用途。

![V5 nano - 主图](../../assets/flight_controller/cuav_v5_nano/v5_nano_01.png)

::: info
V5 nano 类似于 [CUAV V5+](../flight_controller/cuav_v5_plus.md)，但采用一体化外形，PWM 端口较少（不能用于使用 AUX 端口的[机架](../airframes/airframe_reference.md)），并且没有内部阻尼。
:::

其一些主要特性包括：

- 与 [Pixhawk 项目](https://pixhawk.org/) **FMUv5** 设计标准完全兼容，并对所有外部接口使用 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
- 比 FMU v3 更先进的处理器、RAM 和闪存，以及更稳定可靠的传感器。
- 与 PX4 固件兼容。
- I/O 引脚宽敞的 2.6mm 间距，使所有接口更易于使用。

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

### 快速摘要

主 FMU 处理器：STM32F765◦32 位 Arm® Cortex®-M7，216MHz，2MB 内存，512KB RAM

- 板载传感器：
  - 加速度计/陀螺仪：ICM-20689
  - 加速度计/陀螺仪：ICM-20602
  - 加速度计/陀螺仪：BMI055
  - 磁力计：IST8310
  - 气压计：MS5611

- 接口：8 个 PWM 输出
  - FMU 上 3 个专用 PWM/捕获输入
  - CPPM 专用 R/C 输入
  - Spektrum / DSM 和 S.Bus 专用 R/C 输入
  - 模拟 / PWM RSSI 输入
  - 4 个通用串行端口
  - 3 个 I2C 端口
  - 4 个 SPI 总线
  - 2 个 CAN 总线
  - 电池电压/电流模拟输入
  - 2 个额外的模拟输入
  - 支持 nARMED

- 电源系统：Power Brick 输入：4.75~5.5V
- USB 电源输入：4.75~5.25V

- 重量和尺寸：
  - 尺寸：60\*40\*14mm
- 其他特性：
  - 工作温度：-20 ~ 85°C（测量值）

## 购买渠道

[CUAV 商店](https://store.cuav.net/shop/v5-nano/)

[CUAV Aliexpress](https://www.aliexpress.com/item/33050770314.html?storeId=3257035&spm=2114.12010612.8148356.9.dbe6790bjW2hpH)（国际用户）

[CUAV 淘宝](https://item.taobao.com/item.htm?spm=a230r.1.14.8.26ab5258veQJRu&id=569404317857&ns=1&abbucket=13#detail)（中国大陆用户）

::: info
自驾仪可能会配备 Neo GPS 模块一起购买
:::

<a id="connection"></a>

## 连接（接线）

[V5 nano 接线快速入门](../assembly/quick_start_cuav_v5_nano.md)

## 引脚分布

从[这里](http://manual.cuav.net/V5-Plus.pdf)下载 **V5 nano** 引脚分布图。

## 构建固件

:::tip
大多数用户不需要构建此固件！
当连接适当的硬件时，它会由 _QGroundControl_ 预构建并自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v5_default
```

<a id="debug_port"></a>

## 调试端口

[PX4 系统控制台](../debug/system_console.md) 和 [SWD 接口](../debug/swd_debug.md) 在 **FMU Debug** 端口 (`DSU7`) 上运行。
该板没有 I/O 调试接口。

![调试端口 (DSU7)](../../assets/flight_controller/cuav_v5_nano/debug_port_dsu7.jpg)

调试端口 (`DSU7`) 使用 [JST BM06B](https://www.digikey.com.au/en/products/detail/jst-sales-america-inc/BM06B-GHS-TBT-LF-SN-N/807850) 连接器，具有以下引脚分布：

| 引脚    | 信号           | 电压  |
| ------- | -------------- | ----- |
| 1 (红)  | 5V+            | +5V   |
| 2 (黑)  | DEBUG TX (OUT) | +3.3V |
| 3 (黑)  | DEBUG RX (IN)  | +3.3V |
| 4 (黑)  | FMU_SWDIO      | +3.3V |
| 5 (黑)  | FMU_SWCLK      | +3.3V |
| 6 (黑)  | GND            | GND   |

产品包装包含一根便于使用的调试电缆，可以连接到 `DSU7` 端口。
这将分出一根 FTDI 电缆用于将 [PX4 系统控制台](../debug/system_console.md) 连接到计算机 USB 端口，以及用于 SWD/JTAG 调试的 SWD 引脚。
提供的调试电缆不连接到 SWD 端口 `Vref` 引脚 (1)。

![CUAV 调试电缆](../../assets/flight_controller/cuav_v5_nano/cuav_nano_debug_cable.jpg)

:::warning
SWD Vref 引脚 (1) 使用 5V 作为 Vref，但 CPU 运行在 3.3V！

一些 JTAG 适配器（SEGGER J-Link）将使用 Vref 电压来设置 SWD 线上的电压。
对于直接连接到 _Segger Jlink_，我们建议您使用标记为 `DSM`/`SBUS`/`RSSI` 的连接器引脚 4 的 3.3 伏来为 JTAG 提供 `Vtref`（即提供 3.3V 而_不是_ 5V）。

有关更多信息，请参见[使用 JTAG 进行硬件调试](#using-jtag-for-hardware-debugging)。
:::

## 串口映射

| UART   | 设备       | 端口                                      |
| ------ | ---------- | ----------------------------------------- |
| UART1  | /dev/ttyS0 | GPS                                       |
| USART2 | /dev/ttyS1 | TELEM1（流量控制）                        |
| USART3 | /dev/ttyS2 | TELEM2（流量控制）                        |
| UART4  | /dev/ttyS3 | TELEM4                                    |
| USART6 | /dev/ttyS4 | TX 是来自 SBUS_RC 连接器的 RC 输入        |
| UART7  | /dev/ttyS5 | 调试控制台                                |
| UART8  | /dev/ttyS6 | 未连接（无 PX4IO）                       |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 电压额定值

_V5 nano_ 在飞行期间必须从 `Power` 连接器供电，也可以/或者从 `USB` 供电用于台架测试。

::: info
`PM2` 连接器不能用于为 _V5 nano_ 供电（参见[这个问题](#compatibility_pm2)）。
:::

::: info
舵机电源轨既不由 FMU 供电，也不向 FMU 提供电源。
但是，标记为 **+** 的引脚都是公共的，BEC 可以连接到任何舵机引脚组来为舵机电源轨供电。
:::

## 过流保护

_V5 nano_ 没有过流保护。

<a id="Optional-hardware"></a>

## 外设

- [数字空速传感器](https://item.taobao.com/item.htm?spm=a1z10.3-c-s.w4002-16371268452.37.6d9f48afsFgGZI&id=9512463037)
- [遥测无线电模块](https://cuav.taobao.com/category-158480951.htm?spm=2013.1.w5002-16371268426.4.410b7a821qYbBq&search=y&catName=%CA%FD%B4%AB%B5%E7%CC%A8)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/飞机/漫游车或船只。
完整的支持配置集可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 兼容性

CUAV 采用了一些差异化设计，与某些硬件不兼容，将在下面描述。

<a id="compatibility_gps"></a>

#### Neo v2.0 GPS 与其他设备不兼容

推荐与 _CUAV V5+_ 和 _CUAV V5 nano_ 一起使用的 _Neo v2.0 GPS_ 与其他 Pixhawk 飞行控制器不完全兼容（具体来说，蜂鸣器部分不兼容，安全开关可能有问题）。

也可以使用 UAVCAN [NEO V2 PRO GNSS 接收器](https://doc.cuav.net/gps/neo-series-gnss/en/neo-v2-pro.html)，它与其他飞行控制器兼容。

<a id="compatibility_jtag"></a>

#### 使用 JTAG 进行硬件调试

`DSU7` FMU 调试引脚 1 是 5 伏 - 不是 CPU 的 3.3 伏。

一些 JTAG 探针使用此电压来设置与目标通信时的 IO 电平。

对于直接连接到 _Segger Jlink_，我们建议您使用 DSM/SBUS/RSSI 引脚 4 的 3.3 伏作为调试连接器上的引脚 1（`Vtref`）。

<a id="compatibility_pm2"></a>

#### PM2 无法为飞行控制器供电

`PM2` 只能测量电池电压和电流，但**不能**为飞行控制器供电。

:::warning
PX4 不支持此接口。
:::

## 已知问题

下面的问题指的是它们首次出现的_批次号_。
批次号是 V01 后面的四位生产日期，显示在飞行控制器侧面的贴纸上。
例如，序列号批次 V011904（V01 是 V5 的编号，1904 是生产日期，即批次号）。

<a id="pin1_unfused"></a>

#### SBUS / DSM / RSSI 接口引脚1未熔断

:::warning
这是一个安全问题。
:::

请勿在 SBUS / DSM / RSSI 接口上连接其他设备（除了 RC 接收器）- 这可能导致设备损坏！

- _发现：_ 批次 V01190904xxxx
- _修复：_ 批次晚于 V01190904xxxx

## 更多信息

- [V5 nano 手册](http://manual.cuav.net/V5-nano.pdf) (CUAV)
- [FMUv5 参考设计引脚分布](https://docs.google.com/spreadsheets/d/1-n0__BYDedQrc_2NHqBenG1DNepAgnHpSGglke-QQwY/edit#gid=912976165) (CUAV)
- [CUAV Github](https://github.com/cuav) (CUAV)
- [使用 CUAV v5 nano 在 DJI FlameWheel450 上构建机架的日志](../frames_multicopter/dji_f450_cuav_5nano.md)
