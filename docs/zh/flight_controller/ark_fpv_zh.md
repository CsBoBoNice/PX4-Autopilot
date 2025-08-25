# ARK FPV 飞行控制器

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://arkelectron.com/contact-us/)。
:::

美国制造的 ARK FPV 飞行控制器基于 [ARKV6X](https://arkelectron.com/product/arkv6x/)，采用 30.5mm 标准安装模式，支持 3-12s 电池输入，具有稳压 12V 2A 输出，用于视频发射器和载荷。

![ARK FPV Main Photo](../../assets/flight_controller/arkfpv/ark_fpv.jpg)

:::info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 购买地点

从 [Ark Electronics](https://arkelectron.com/product/arkv6x/) 订购（美国）

## 文档

请参阅文档 [Ark Electronics GitBook](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-fpv)

## 传感器

- [Invensense IIM-42653 工业级 IMU](https://invensense.tdk.com/products/smartindustrial/iim-42653/)
- [Bosch BMP390 气压计](https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp390/)
- [ST IIS2MDC 磁力计](https://www.st.com/en/mems-and-sensors/iis2mdc.html)

## 微处理器

- [STM32H743IIK6 MCU](https://www.st.com/en/microcontrollers-microprocessors/stm32h743ii.html)
  - 480 MHz
  - 2 MB Flash
  - 1 MB RAM

## 连接器

- USB C
  - VBUS 输入，USB
- PWM
  - VBAT 输入，模拟电流输入，遥测 RX，4x PWM
  - JST-GH 8 针
- PWM EXTRA
  - 5x PWM
  - JST-SH 6 针
- RC INPUT
  - 5V 输出，UART
  - JST-GH 4 针
- POWER AUX
  - 12V 输出，VBAT 输入/输出
  - JST-GH 3 针
- TELEM
  - 5V 输出，带流量控制的 UART
  - JST-GH 6 针
- GPS
  - 5V 输出，UART，I2C
  - JST-GH 6 针
- CAN
  - 5V 输出，CAN
  - JST-GH 4 针
- VTX
  - 12V 输出，UART TX/RX，UART RX
  - JST-GH 6 针
- SPI（OSD 或外部 IMU）
  - 5V 输出，SPI
  - JST-SH 8 针
- DEBUG
  - 3.3V 输出，UART，SWD
  - JST-SH 6 针

## 电源要求

- 5.5V - 54V
- 500 mA（300 mA 主系统，200 mA 加热器）

## 附加信息

- 重量：7.5 g（含 MicroSD 卡）
- 尺寸：3.6 x 3.6 x 0.8 cm
- 美国制造 - 符合 NDAA 标准
- 加热器：1W，用于在极寒环境中加热传感器
- LED 指示灯
- MicroSD 卡槽

## 引脚分布

请参阅 [DS-10 Pixhawk 自驾仪总线标准](https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-fpv/pinout)
