# mRo Pixracer

:::warning
PX4不制造此飞控（或任何其他自动驾驶仪）。
如需硬件支持或合规问题，请联系[制造商](https://store.mrobotics.io/)。
:::

Pixhawk<sup>&reg;</sup> XRacer 板系列针对小型竞速四轴飞行器和飞机进行了优化。与 [Pixfalcon](../flight_controller/pixfalcon.md) 和 [Pixhawk](../flight_controller/pixhawk.md) 相比，它内置 WiFi、新传感器、便捷的完整伺服接头、CAN 并支持 2M 闪存。

<img src="../../assets/flight_controller/pixracer/pixracer_hero_grey.jpg" width="300px" title="pixracer + 8266 grey" />

:::tip
此自动驾驶仪得到 PX4 维护和测试团队的[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 主要特性

- 主系统级芯片：[STM32F427VIT6 rev.3](https://www.st.com/en/microcontrollers-microprocessors/stm32f427-437.html)
  - CPU：180 MHz ARM Cortex<sup>&reg;</sup> M4 单精度 FPU
  - RAM：256 KB SRAM (L1)
- 标准 FPV 外形：36x36 mm，标准 30.5 mm 孔间距
- Invensense<sup>&reg;</sup> ICM-20608 加速度计/陀螺仪 (4 KHz) / MPU9250 加速度计/陀螺仪/磁力计 (4 KHz)
- HMC5983 带温度补偿的磁力计
- Measurement Specialties MS5611 气压计
- JST GH 连接器
- microSD（记录）
- Futaba S.BUS 和 S.BUS2 / Spektrum DSM2 和 DSMX / Graupner SUMD / PPM 输入 / Yuneec ST24
- FrSky<sup>&reg;</sup> 遥测端口
- OneShot PWM 输出（可配置）
- 可选：安全开关和蜂鸣器

## 购买地址

Pixracer Pro 可从 [store.3dr.com](https://store.3dr.com/pixracer-pro/) 购买。

配件包括：

- [数字空速传感器](https://hobbyking.com/en_us/hkpilot-32-digital-air-speed-sensor-and-pitot-tube-set.html)
- Hobbyking<sup>&reg;</sup> OSD + EU 遥测 (433 MHz)（已停产）

## 套件

Pixracer 设计为使用独立的航电电源。这是为了避免来自电机或 ESC 的电流浪涌流回飞控并干扰其精密传感器所必需的。

- 电源模块（具有电压和电流检测）
- I2C 分离器（支持 AUAV、Hobbyking 和 3DR<sup>&reg;</sup> 外设）
- 所有常见外设的电缆套件

## Wifi（无需 USB）

该板的主要特性之一是能够使用 Wifi 刷新新固件、系统设置和飞行中遥测。这使其无需任何桌面系统。

- [ESP8266 Wifi](../telemetry/esp8266_wifi_module.md)
- [自定义 ESP8266 MAVLink 固件](https://github.com/BeyondRobotix/mavesp8266)

::: info
尚未启用通过 WiFi 的固件升级（默认引导加载程序支持但尚未启用）。支持设置和遥测。
:::

## 组装

请参阅 [Pixracer 接线快速入门](../assembly/quick_start_pixracer.md)

## 接线图

![Grau setup pixracer top](../../assets/flight_controller/pixracer/grau_setup_pixracer_top.jpg)

::: info
如果将 `TELEM2` 用于外部遥测模块，您需要将其配置为 MAVLink 串行端口。更多信息请参见：[Pixracer 接线快速入门 > 外部遥测](../assembly/quick_start_pixracer.md#external-telemetry)
:::

![Grau setup pixracer bottom](../../assets/flight_controller/pixracer/grau_setup_pixracer_bottom.jpg)

![setup pixracer GPS](../../assets/flight_controller/pixracer/grau_setup_pixracer_gps.jpg)

![Grau b Pixracer FrSkyS.Port Connection](../../assets/flight_controller/pixracer/grau_b_pixracer_frskys.port_connection.jpg)

![Grau ACSP4 2 roh](../../assets/flight_controller/pixracer/grau_acsp4_2_roh.jpg)

![Grau ACSP5 roh](../../assets/flight_controller/pixracer/grau_acsp5_roh.jpg)

## 连接器

所有连接器都遵循 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。除非另有说明，否则所有连接器都是 JST GH。

## 引脚定义

![Pixracer 顶部引脚定义](../../assets/flight_controller/pixracer/pixracer_r09_top_pinouts.jpg)

![Pixracer 底部引脚定义](../../assets/flight_controller/pixracer/pixracer_r09_bot_pinouts.jpg)

![Pixracer esp](../../assets/flight_controller/pixracer/pixracer_r09_esp_01.jpg)

#### TELEM1, TELEM2+OSD 端口

| 引脚      | 信号      | 电压  |
| ------- | ------- | --- |
| 1（红）   | VCC     | +5V |
| 2（黑）   | TX（OUT） | +3.3V |
| 3（黑）   | RX（IN）  | +3.3V |
| 4（黑）   | CTS（IN） | +3.3V |
| 5（黑）   | RTS（OUT） | +3.3V |
| 6（黑）   | GND     | GND |

#### GPS 端口

| 引脚      | 信号       | 电压  |
| ------- | -------- | --- |
| 1（红）   | VCC      | +5V |
| 2（黑）   | TX（OUT） | +3.3V |
| 3（黑）   | RX（IN）  | +3.3V |
| 4（黑）   | I2C1 SCL | +3.3V |
| 5（黑）   | I2C1 SDA | +3.3V |
| 6（黑）   | GND      | GND |

#### FrSky 遥测 / SERIAL4

| 引脚      | 信号       | 电压  |
| ------- | -------- | --- |
| 1（红）   | VCC      | +5V |
| 2（黑）   | TX（OUT） | +3.3V |
| 3（黑）   | RX（IN）  | +3.3V |
| 4（黑）   | GND      | GND |

#### RC 输入（接受 PPM / S.BUS / Spektrum / SUMD / ST24）

| 引脚      | 信号       | 电压  |
| ------- | -------- | --- |
| 1（红）   | VCC      | +5V |
| 2（黑）   | RC IN    | +3.3V |
| 3（黑）   | RSSI IN  | +3.3V |
| 4（黑）   | VDD 3V3  | +3.3V |
| 5（黑）   | GND      | GND |

#### CAN

| 引脚      | 信号     | 电压   |
| ------- | ------ | ---- |
| 1（红）   | VCC    | +5V  |
| 2（黑）   | CAN_H  | +12V |
| 3（黑）   | CAN_L  | +12V |
| 4（黑）   | GND    | GND  |

#### POWER

| 引脚      | 信号      | 电压  |
| ------- | ------- | --- |
| 1（红）   | VCC     | +5V |
| 2（黑）   | VCC     | +5V |
| 3（黑）   | CURRENT | +3.3V |
| 4（黑）   | VOLTAGE | +3.3V |
| 5（黑）   | GND     | GND |
| 6（黑）   | GND     | GND |

#### SWITCH

| 引脚      | 信号             | 电压  |
| ------- | -------------- | --- |
| 1（红）   | SAFETY         | GND |
| 2（黑）   | !IO_LED_SAFETY | GND |
| 3（黑）   | VCC            | +3.3V |
| 4（黑）   | BUZZER-        | -   |
| 5（黑）   | BUZZER+        | -   |

#### 调试端口

引脚定义和连接器符合在 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)中定义的 [Pixhawk Debug Mini](../debug/swd_debug.md#pixhawk-debug-mini) 接口（JST SM06B 连接器）。

| 引脚      | 信号             | 电压  |
| ------- | -------------- | --- |
| 1（红）   | VCC TARGET SHIFT | +3.3V |
| 2（黑）   | CONSOLE TX（OUT） | +3.3V |
| 3（黑）   | CONSOLE RX（IN）  | +3.3V |
| 4（黑）   | SWDIO          | +3.3V |
| 5（黑）   | SWCLK          | +3.3V |
| 6（黑）   | GND            | GND |

有关使用此端口的信息，请参阅：

- [SWD 调试端口](../debug/swd_debug.md)
- [PX4 系统控制台](../debug/system_console.md)（注意，FMU 控制台映射到 UART7）。

## 串口映射

| UART   | 设备         | 端口                    |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | WiFi (ESP8266)        |
| USART2 | /dev/ttyS1 | TELEM1（流控制）          |
| USART3 | /dev/ttyS2 | TELEM2（流控制）          |
| UART4  |            |                       |
| UART7  | 控制台        |                       |
| UART8  | SERIAL4    |                       |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 原理图

参考提供为：[Altium 设计文件](https://github.com/AUAV-OpenSource/FMUv4-PixRacer)

提供以下 PDF 文件_仅供参考_：

- [pixracer-rc12-12-06-2015-1330.pdf](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/pixracer/pixracer-rc12-12-06-2015-1330.pdf)
- [pixracer-r14.pdf](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/pixracer/pixracer-r14.pdf) - R14 或 RC14 印在 SDCard 插槽旁边

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时由 _QGroundControl_ 自动安装。
:::

为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v4_default
```

## 配置

[罗盘校准](../config/compass.md)应在断开 USB 连接的情况下进行。始终建议这样做，但在 Pixracer 上是必需的，因为 USB 连接会产生特别大的磁干扰。

其他配置与其他板相同。

## 鸣谢

此设计由 Nick Arsov 和 Phillip Kocmoud 创建，由 Lorenz Meier、David Sidrane 和 Leonard Hall 设计架构。
