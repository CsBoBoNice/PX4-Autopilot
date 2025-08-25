# ARK Pixhawk 自驾仪总线载板

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://arkelectron.com/contact-us/)。
:::

[ARK Pixhawk 自驾仪总线（PAB）载板](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-pixhawk-autopilot-bus-carrier) 是美国制造的飞行控制器载板，基于 [Pixhawk 自驾仪总线开源标准](https://github.com/pixhawk/Pixhawk-Standards)。

PAB 外形规格使 ARK PAB 载板能够与任何 [PAB 兼容的飞行控制器](../flight_controller/pixhawk_autopilot_bus.md) 一起使用，例如 [ARKV6X](../flight_controller/ark_v6x.md)。

![ARKPAB Main Photo](../../assets/flight_controller/arkpab/ark_pab_main.jpg)

### 购买地点

从 [Ark Electronics](https://arkelectron.com/product/ark-pixhawk-autopilot-bus-carrier/) 订购（美国）

## 特点

- [Pixhawk 自驾仪总线（PAB）外形规格](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf?_ga=2.20605755.2081055420.1671562222-391294592.1671562222)
- 美国制造

## 连接器

- PAB 板对板接口
  - 100 针 Hirose DF40
  - 40 针 Hirose DF40
- 双数字电源模块输入
  - 5V 输入
  - I2C 电源监控器
  - 6 针 Molex CLIK-Mate
- 以太网
  - 100Mbps
  - 内置磁性元件
  - 4 针 JST-GH
- 完整 GPS 加安全开关端口
  - 10 针 JST-GH
- 基本 GPS 端口
  - 6 针 JST-GH
- 双 CAN 端口
  - 4 针 JST-GH
- 三重遥测端口带流量控制
  - 6 针 JST-GH
- 八个 PWM 输出
  - 10 针 JST-GH
- UART/I2C 端口
  - 6 针 JST-GH
- I2C 端口
  - 4 针 JST-GH
- PPM RC 端口
  - 3 针 JST-GH
- DSM RC 端口
  - 3 针 JST-ZH
- SPI 端口
  - 11 针 JST-GH
- ADIO 端口
  - 8 针 JST-GH
- 调试端口
  - 10 针 JST-SH

## 尺寸

- 不含飞行控制器模块
  - 74.0mm x 43.5mm x 12.0mm
  - 22g

## 电源

- `POWER1`、`POWER2`、`USB C` 和 `USB JST-GH` 连接器上的 5V 输入
  - 输入优先级顺序：POWER1 > POWER2 > USB
  - `USB C` 和 `USB JST-GH` 并联
  - 过压保护 5.8V
  - 欠压保护 3.9V
- `VDD_5V_HIPOWER` 和 `VDD_5V_PERIPH` 在所有连接器中每个可提供总计 1.5A

## LED

- ARK PAB 上有两个 LED
  - `红色` 是以太网电源 LED
  - `绿色` 是以太网活动 LED

## 引脚分布

![ARKPAB Pinout](../../assets/flight_controller/arkpab/arkpab_pinout.jpg)

## POWER1

| 引脚      | 信号      | 电压  |
| --------- | --------- | ----- |
| 1 (红色)  | `VBRICK1` | +5.0V |
| 2 (黑色)  | `VBRICK1` | +5.0V |
| 3 (黑色)  | I2C1_SCL  | +3.3V |
| 4 (黑色)  | I2C1_SDA  | +3.3V |
| 5 (黑色)  | `GND`     | GND   |
| 6 (黑色)  | `GND`     | GND   |

## POWER2

| 引脚      | 信号      | 电压  |
| --------- | --------- | ----- |
| 1 (红色)  | `VBRICK2` | +5.0V |
| 2 (黑色)  | `VBRICK2` | +5.0V |
| 3 (黑色)  | I2C2_SCL  | +3.3V |
| 4 (黑色)  | I2C2_SDA  | +3.3V |
| 5 (黑色)  | `GND`     | GND   |
| 6 (黑色)  | `GND`     | GND   |

## PWM

| 引脚       | 信号                      | 电压  |
| ---------- | ------------------------- | ----- |
| 1 (红色)   | VDD_SERVO (未连接)        | +5.0V |
| 2 (黑色)   | FMU_CH1                   | +3.3V |
| 3 (黑色)   | FMU_CH2                   | +3.3V |
| 4 (黑色)   | FMU_CH3                   | +3.3V |
| 5 (黑色)   | FMU_CH4                   | +3.3V |
| 6 (黑色)   | FMU_CH5                   | +3.3V |
| 7 (黑色)   | FMU_CH6                   | +3.3V |
| 8 (黑色)   | FMU_CH7                   | +3.3V |
| 9 (黑色)   | FMU_CH8                   | +3.3V |
| 10 (黑色)  | `GND`                     | GND   |

## GPS1

| 引脚       | 信号                       | 电压  |
| ---------- | -------------------------- | ----- |
| 1 (红色)   | `VDD_5V_PERIPH`            | +5.0V |
| 2 (黑色)   | USART1_TX_GPS1             | +3.3V |
| 3 (黑色)   | USART1_RX_GPS1             | +3.3V |
| 4 (黑色)   | I2C1_SCL                   | +3.3V |
| 5 (黑色)   | I2C1_SDA                   | +3.3V |
| 6 (黑色)   | nSAFETY_SWITCH_IN          | +3.3V |
| 7 (黑色)   | nSAFETY_SWITCH_LED_OUT     | +3.3V |
| 8 (黑色)   | `3V3_FMU`                  | +3.3V |
| 9 (黑色)   | BUZZER                     | +5.0V |
| 10 (黑色)  | `GND`                      | GND   |

## GPS2

| 引脚      | 信号             | 电压  |
| --------- | ---------------- | ----- |
| 1 (红色)  | `VDD_5V_HIPOWER` | +5.0V |
| 2 (黑色)  | UART8_TX_GPS2    | +3.3V |
| 3 (黑色)  | UART8_RX_GPS2    | +3.3V |
| 4 (黑色)  | I2C2_SCL         | +3.3V |
| 5 (黑色)  | I2C2_SDA         | +3.3V |
| 6 (黑色)  | `GND`            | GND   |

## TELEM1

| 引脚      | 信号             | 电压  |
| --------- | ---------------- | ----- |
| 1 (红色)  | `VDD_5V_HIPOWER` | +5.0V |
| 2 (黑色)  | UART7_TX         | +3.3V |
| 3 (黑色)  | UART7_RX         | +3.3V |
| 4 (黑色)  | UART7_CTS        | +3.3V |
| 5 (黑色)  | UART7_RTS        | +3.3V |
| 6 (黑色)  | `GND`            | GND   |

## TELEM2

| 引脚      | 信号            | 电压  |
| --------- | --------------- | ----- |
| 1 (红色)  | `VDD_5V_PERIPH` | +5.0V |
| 2 (黑色)  | UART5_TX        | +3.3V |
| 3 (黑色)  | UART5_RX        | +3.3V |
| 4 (黑色)  | UART5_CTS       | +3.3V |
| 5 (黑色)  | UART5_RTS       | +3.3V |
| 6 (黑色)  | `GND`           | GND   |

## TELEM3

| 引脚      | 信号             | 电压  |
| --------- | ---------------- | ----- |
| 1 (红色)  | `VDD_5V_HIPOWER` | +5.0V |
| 2 (黑色)  | USART2_TX        | +3.3V |
| 3 (黑色)  | USART2_RX        | +3.3V |
| 4 (黑色)  | USART2_CTS       | +3.3V |
| 5 (黑色)  | USART2_RTS       | +3.3V |
| 6 (黑色)  | `GND`            | GND   |

## UART4/I2C3

| 引脚      | 信号            | 电压  |
| --------- | --------------- | ----- |
| 1 (红色)  | `VDD_5V_PERIPH` | +5.0V |
| 2 (黑色)  | UART4_TX        | +3.3V |
| 3 (黑色)  | UART4_RX        | +3.3V |
| 4 (黑色)  | I2C3_SCL        | +3.3V |
| 5 (黑色)  | I2C3_SDA        | +3.3V |
| 6 (黑色)  | `GND`           | GND   |

## I2C3

| 引脚      | 信号            | 电压  |
| --------- | --------------- | ----- |
| 1 (红色)  | `VDD_5V_PERIPH` | +5.0V |
| 2 (黑色)  | I2C3_SCL        | +3.3V |
| 3 (黑色)  | I2C3_SDA        | +3.3V |
| 4 (黑色)  | `GND`           | GND   |

## CAN1

| 引脚      | 信号             | 电压  |
| --------- | ---------------- | ----- |
| 1 (红色)  | `VDD_5V_HIPOWER` | +5.0V |
| 2 (黑色)  | CAN1_H           | +3.3V |
| 3 (黑色)  | CAN1_L           | +3.3V |
| 4 (黑色)  | `GND`            | GND   |

## CAN2

| 引脚      | 信号            | 电压  |
| --------- | --------------- | ----- |
| 1 (红色)  | `VDD_5V_PERIPH` | +5.0V |
| 2 (黑色)  | CAN2_H          | +3.3V |
| 3 (黑色)  | CAN2_L          | +3.3V |
| 4 (黑色)  | `GND`           | GND   |

## USB

所有信号与 USB C 连接器并联
| 引脚      | 信号      | 电压  |
| --------- | --------- | ----- |
| 1 (红色)  | `VBUS_IN` | +5.0V |
| 2 (黑色)  | USB_N     | +3.3V |
| 3 (黑色)  | USB_P     | +3.3V |
| 4 (黑色)  | `GND`     | GND   |

## ETH

| 引脚      | 信号     | 电压               |
| --------- | -------- | ------------------ |
| 1 (红色)  | ETH_RD_N | +50.0V 耐压        |
| 2 (黑色)  | ETH_RD_P | +50.0V 耐压        |
| 3 (黑色)  | ETH_TD_N | +50.0V 耐压        |
| 4 (黑色)  | ETH_TD_P | +50.0V 耐压        |

## ADIO

| 引脚      | 信号            | 电压  |
| --------- | --------------- | ----- |
| 1 (红色)  | `VDD_5V_PERIPH` | +5.0V |
| 2 (黑色)  | FMU_CAP         | +3.3V |
| 3 (黑色)  | BOOTLOADER      | +3.3V |
| 4 (黑色)  | FMU_RST_REQ     | +3.3V |
| 5 (黑色)  | nARMED          | +3.3V |
| 6 (黑色)  | ADC1_3V3        | +3.3V |
| 7 (黑色)  | ADC1_6V6        | +3.3V |
| 8 (黑色)  | `GND`           | GND   |

## RC/SBUS

| 引脚      | 信号               | 电压  |
| --------- | ------------------ | ----- |
| 1 (红色)  | `VDD_5V_SBUS_RC`   | +5.0V |
| 2 (黑色)  | USART6_RX_SBUS_IN  | +3.3V |
| 3 (黑色)  | USART6_TX          | +3.3V |
| 4 (黑色)  | `VDD_3V3_SPEKTRUM` | +3.3V |
| 5 (黑色)  | `GND`              | GND   |

## PPM

| 引脚      | 信号                        | 电压  |
| --------- | --------------------------- | ----- |
| 1 (红色)  | `VDD_5V_PPM_RC`             | +5.0V |
| 2 (黑色)  | DSM_INPUT/FMU_PPM_INPUT     | +3.3V |
| 3 (黑色)  | `GND`                       | GND   |

## DSM

| 引脚      | 信号                        | 电压  |
| --------- | --------------------------- | ----- |
| 1 (红色)  | `VDD_3V3_SPEKTRUM`          | +3.3V |
| 2 (黑色)  | `GND`                       | GND   |
| 3 (黑色)  | DSM_INPUT/FMU_PPM_INPUT     | +3.3V |

## SPI6

| 引脚       | 信号            | 电压  |
| ---------- | --------------- | ----- |
| 1 (红色)   | `VDD_5V_PERIPH` | +5.0V |
| 2 (黑色)   | SPI6_SCK        | +3.3V |
| 3 (黑色)   | SPI6_MISO       | +3.3V |
| 4 (黑色)   | SPI6_MOSI       | +3.3V |
| 5 (黑色)   | SPI6_nCS1       | +3.3V |
| 6 (黑色)   | SPI6_nCS2       | +3.3V |
| 7 (黑色)   | SPIX_nSYNC      | +3.3V |
| 8 (黑色)   | SPI6_DRDY1      | +3.3V |
| 9 (黑色)   | SPI6_DRDY2      | +3.3V |
| 10 (黑色)  | SPI6_nRESET     | +3.3V |
| 11 (黑色)  | `GND`           | GND   |

## 调试端口

[PX4 系统控制台](../debug/system_console.md) 和 [SWD 接口](../debug/swd_debug.md) 在 **FMU 调试** 端口上运行。

引脚分布和连接器符合 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf) 中定义的 [Pixhawk Debug Full](../debug/swd_debug.md#pixhawk-debug-full) 接口（JST SM10B 连接器）。

| 引脚       | 信号             | 电压  |
| ---------- | ---------------- | ----- |
| 1 (红色)   | `Vtref`          | +3.3V |
| 2 (黑色)   | Console TX (OUT) | +3.3V |
| 3 (黑色)   | Console RX (IN)  | +3.3V |
| 4 (黑色)   | `SWDIO`          | +3.3V |
| 5 (黑色)   | `SWCLK`          | +3.3V |
| 6 (黑色)   | `SWO`            | +3.3V |
| 7 (黑色)   | NFC GPIO         | +3.3V |
| 8 (黑色)   | PH11             | +3.3V |
| 9 (黑色)   | nRST             | +3.3V |
| 10 (黑色)  | `GND`            | GND   |

有关使用此端口的信息，请参阅：

- [SWD 调试端口](../debug/swd_debug.md)
- [PX4 系统控制台](../debug/system_console.md)（注意，FMU 控制台映射到 USART3）。

![ARKPAB Top Down Photo](../../assets/flight_controller/arkpab/ark_pab_top.jpg)

![ARKPAB Bottom Photo](../../assets/flight_controller/arkpab/ark_pab_back.jpg)

## 另请参阅

- [ARK Pixhawk 自驾仪总线载板](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-pixhawk-autopilot-bus-carrier)（ARK 文档）
