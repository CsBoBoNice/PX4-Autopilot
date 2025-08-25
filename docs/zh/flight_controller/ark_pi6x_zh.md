# ARK Pi6X Flow

[ARK Pi6X Flow](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-pi6x-flow) 将树莓派计算模块 4（CM4）载板、[ARKV6X 飞行控制器](../flight_controller/ark_v6x.md)、[ARK Flow 传感器](../dronecan/ark_flow.md)、[ARK PAB 电源模块](../power_module/ark_pab_power_module.md) 和 4 合 1 电调集成在一块紧凑的板卡上。

![ARK Pi6X Flow Flight Controller](../../assets/flight_controller/ark_pi6x_flow/ark_pi6xflow.jpg)

## 购买地点

从以下渠道订购此模块：

- [ARK Electronics](https://arkelectron.com/product/ark-pi6x-flow/)（美国）

## 主要组件

### 树莓派计算模块 4 载板

- 自驾仪固件：PX4
- 特点：
  - MicroSD 插槽（适用于 CM4 Lite）
  - Micro HDMI
  - 以太网
  - USB C 主机
  - 2x USB JST GH
  - 2x MIPI CSI（22 针 FFC）
  - 编程 micro USB
  - I2C、UART
  - LED 灯带 GPIO
  - 通用 GPIO
  - 控制台
  - CPU 风扇

### 自驾仪

- 通信：
  - TELEM（UART）
  - RC 输入（UART）
  - GPS（UART、I2C）
  - CAN
- 控制和监控：
  - 8 个 PWM 输出
  - 蜂鸣器
  - 调试（SWD、UART 控制台）
  - 用于数据存储的 MicroSD 插槽

### 传感器

- 2x ICM-42688-P 加速度计/陀螺仪（包含加热器）
- PAW3902 光流传感器
- AFBR-S50LV85D 30 米距离传感器
- ST IIS2MDC 磁力计
- BMP390 气压计
- INA226 电压/电流监控器

### 美国制造且符合 NDAA 标准

## 电源要求

- 电池输入：最高 6s/25.2V（实际要求取决于使用情况和外设）

## 尺寸和重量

- 尺寸：91.5mm x 56mm（不含 Pi CM4 和电调）
- 重量：
  - 41g（不含 Pi CM4、Pi SD 和电调）
  - 53g（包含 Pi CM4 和 Pi SD，不含电调）

## 附加信息

- 包含：飞行控制器 MicroSD
- 套装选项包括：
  - 树莓派计算模块 4 带 WiFi、4GB RAM Lite – CM4104000
  - SanDisk 128GB 高耐久视频 MicroSDXC，预装 [ARK-OS](https://github.com/ARK-Electronics/ARK-OS)

## 刷写指南

[ARK Pi6X 刷写指南](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-pi6x-flow/flashing-guide)

## 引脚分布

![ARK Pi6X Flow Pinout](../../assets/flight_controller/ark_pi6x_flow/ark_pi6xflow_pinout.png)

### PWM UART4 - 11 针 JST-GH

| 引脚编号 | 信号名称     | 电压 |
| :------- | :----------- | :--- |
| 1        | FMU_CH1_EXT  | 3.3V |
| 2        | FMU_CH2_EXT  | 3.3V |
| 3        | FMU_CH3_EXT  | 3.3V |
| 4        | FMU_CH4_EXT  | 3.3V |
| 5        | FMU_CH5_EXT  | 3.3V |
| 6        | FMU_CH6_EXT  | 3.3V |
| 7        | FMU_CH7_EXT  | 3.3V |
| 8        | FMU_CH8_EXT  | 3.3V |
| 9        | UART4_TX_EXT | 3.3V |
| 10       | UART4_RX_EXT | 3.3V |
| 11       | GND          | GND  |

### RC - 4 针 JST-GH

| 引脚编号 | 信号名称             | 电压 |
| :------- | :------------------- | :--- |
| 1        | VDD_5V_SBUS_RC       | 5.0V |
| 2        | USART6_RX_IN_EXT     | 3.3V |
| 3        | USART6_TX_OUTPUT_EXT | 3.3V |
| 4        | GND                  | GND  |

### CAN - 4 针 JST-GH

| 引脚编号 | 信号名称       | 电压 |
| :------- | :------------- | :--- |
| 1        | VDD_5V_HIPOWER | 5.0V |
| 2        | CAN1_P         | 5.0V |
| 3        | CAN1_N         | 5.0V |
| 4        | GND            | GND  |

### GPS - 6 针 JST-GH

| 引脚编号 | 信号名称           | 电压 |
| :------- | :----------------- | :--- |
| 1        | VDD_5V_HIPOWER     | 5.0V |
| 2        | USART1_TX_GPS1_EXT | 3.3V |
| 3        | USART1_RX_GPS1_EXT | 3.3V |
| 4        | I2C1_SCL_GPS1_EXT  | 3.3V |
| 5        | I2C1_SDA_GPS1_EXT  | 3.3V |
| 6        | GND                | GND  |

### Telem1 - 6 针 JST-GH

| 引脚编号 | 信号名称             | 电压 |
| :------- | :------------------- | :--- |
| 1        | VDD_5V_HIPOWER       | 5.0V |
| 2        | UART7_TX_TELEM1_EXT  | 3.3V |
| 3        | UART7_RX_TELEM1_EXT  | 3.3V |
| 4        | UART7_CTS_TELEM1_EXT | 3.3V |
| 5        | UART7_RTS_TELEM1_EXT | 3.3V |
| 6        | GND                  | GND  |

### 飞行控制器调试 - 10 针 JST-SH

| 引脚编号 | 信号名称           | 电压 |
| :------- | :----------------- | :--- |
| 1        | 3V3_FMU            | 3.3V |
| 2        | USART4_TX_DEBUG    | 3.3V |
| 3        | USART4_RX_DEBUG    | 3.3V |
| 4        | FMU_SWDIO          | 3.3V |
| 5        | FMU_SWCLK          | 3.3V |
| 6        | SPI6_SCK_EXTERNAL1 | 3.3V |
| 7        | NFC_GPIO           | 3.3V |
| 8        | PD15               | 3.3V |
| 9        | FMU_NRST           | 3.3V |
| 10       | GND                | GND  |

### Pi I2C1 - 4 针 JST-GH

| 引脚编号 | 信号名称     | 电压 |
| :------- | :----------- | :--- |
| 1        | 5.0V         | 5.0V |
| 2        | I2C1_SCL_EXT | 3.3V |
| 3        | I2C1_SDA_EXT | 3.3V |
| 4        | GND          | GND  |

### Pi UART3 - 6 针 JST-GH

| 引脚编号 | 信号名称      | 电压 |
| :------- | :------------ | :--- |
| 1        | 5.0V          | 5.0V |
| 2        | UART3_TX_EXT  | 3.3V |
| 3        | UART3_RX_EXT  | 3.3V |
| 4        | UART3_CTS_EXT | 3.3V |
| 5        | UART3_RTS_EXT | 3.3V |
| 6        | GND           | GND  |

### Pi ETH - 4 针 JST-GH

| 引脚编号 | 信号名称 | 电压 |
| :------- | :------- | :--- |
| 1        | ETH_RD_N | 3.3V |
| 2        | ETH_RD_P | 3.3V |
| 3        | ETH_TD_N | 3.3V |
| 4        | ETH_TD_P | 3.3V |

### Pi LED 灯带 - 8 针 JST-GH

| 引脚编号 | 信号名称   | 电压 |
| :------- | :--------- | :--- |
| 1        | 5.0V       | 5.0V |
| 2        | 5.0V       | 5.0V |
| 3        | GPIO12_EXT | 3.3V |
| 4        | GPIO16_EXT | 3.3V |
| 5        | GPIO17_EXT | 3.3V |
| 6        | GPIO20_EXT | 3.3V |
| 7        | GND        | GND  |
| 8        | GND        | GND  |

### Pi GPIO - 6 针 JST-GH

| 引脚编号 | 信号名称   | 电压 |
| :------- | :--------- | :--- |
| 1        | 5.0V       | 5.0V |
| 2        | GPIO21_EXT | 3.3V |
| 3        | GPIO22_EXT | 3.3V |
| 4        | GPIO23_EXT | 3.3V |
| 5        | GPIO24_EXT | 3.3V |
| 6        | GND        | GND  |

### Pi 风扇 - 4 针 JST-GH

| 引脚编号 | 信号名称     | 电压 |
| :------- | :----------- | :--- |
| 1        | GND          | GND  |
| 2        | 5.0V         | 5.0V |
| 3        | FAN_TACH_CON | 5.0V |
| 4        | FAN_PWM_Q\*  | 5.0V |

### Pi 控制台 - 6 针 JST-SH

| 引脚编号 | 信号名称     | 电压 |
| :------- | :----------- | :--- |
| 1        | 3.3V_RPI     | 3.3V |
| 2        | CONSOLE_TXD0 | 3.3V |
| 3        | CONSOLE_RXD0 | 3.3V |
| 4        | NC           | NC   |
| 5        | NC           | NC   |
| 6        | GND          | GND  |

### Pi USB - 4 针 JST-GH (VBUS2_FLT)

| 引脚编号 | 信号名称   | 电压 |
| :------- | :--------- | :--- |
| 1        | VBUS2_FLT  | 5.0V |
| 2        | USB2_EXT_N | 3.3V |
| 3        | USB2_EXT_P | 3.3V |
| 4        | GND        | GND  |

### Pi USB - 4 针 JST-GH (VBUS4_FLT)

| 引脚编号 | 信号名称   | 电压 |
| :------- | :--------- | :--- |
| 1        | VBUS4_FLT  | 5.0V |
| 2        | USB4_EXT_N | 3.3V |
| 3        | USB4_EXT_P | 3.3V |
| 4        | GND        | GND  |

### CAM0 - 22 针

0.5mm FFC 0545482271

| 引脚编号 | 信号名称  | 电压 |
| :------- | :-------- | :--- |
| 1        | GND       | GND  |
| 2        | CAM0_D0_N | 1.2V |
| 3        | CAM0_D0_P | 1.2V |
| 4        | GND       | GND  |
| 5        | CAM0_D1_N | 1.2V |
| 6        | CAM0_D1_P | 1.2V |
| 7        | GND       | GND  |
| 8        | CAM0_C_N  | 1.2V |
| 9        | CAM0_C_P  | 1.2V |
| 10       | GND       | GND  |
| 11       | NC        | NC   |
| 12       | NC        | NC   |
| 13       | GND       | GND  |
| 14       | NC        | NC   |
| 15       | NC        | NC   |
| 16       | GND       | GND  |
| 17       | CAM_GPIO  | 3.3V |
| 18       | NC        | NC   |
| 19       | GND       | GND  |
| 20       | ID_SC     | 3.3V |
| 21       | ID_SD     | 3.3V |
| 22       | 3.3V_RPI  | 3.3V |

### CAM1 - 22 针 0.5mm FFC 0545482271

| 引脚编号 | 信号名称  | 电压 |
| :------- | :-------- | :--- |
| 1        | GND       | GND  |
| 2        | CAM1_D0_N | 1.2V |
| 3        | CAM1_D0_P | 1.2V |
| 4        | GND       | GND  |
| 5        | CAM1_D1_N | 1.2V |
| 6        | CAM1_D1_P | 1.2V |
| 7        | GND       | GND  |
| 8        | CAM1_C_N  | 1.2V |
| 9        | CAM1_C_P  | 1.2V |
| 10       | GND       | GND  |
| 11       | CAM1_D2_N | 1.2V |
| 12       | CAM1_D2_P | 1.2V |
| 13       | GND       | GND  |
| 14       | CAM1_D3_N | 1.2V |
| 15       | CAM1_D3_P | 1.2V |
| 16       | GND       | GND  |
| 17       | CAM_GPIO  | 3.3V |
| 18       | NC        | NC   |
| 19       | GND       | GND  |
| 20       | SCL0      | 3.3V |
| 21       | SDA0      | 3.3V |
| 22       | 3.3V_RPI  | 3.3V |

## 另请参阅

- [ARK Pi6X Flow 文档](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-pi6x-flow)（ARK 文档）
