# Omnibus F4 SD

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系制造商获取支持或合规问题。
:::

_Omnibus F4 SD_是为竞速机设计的控制器板。
与典型的竞速机板相比，它有一些额外的功能，例如SD卡和更快的CPU。

<img src="../../assets/flight_controller/omnibus_f4_sd/board.jpg" width="400px" title="Omnibus F4 SD" />

与[Pixracer](../flight_controller/pixracer.md)相比，这些是主要区别：

- 价格更低
- IO端口更少（不过仍然可以连接GPS或光流传感器等）
- I2C总线上的外部GPS需要外部上拉电阻，见下面的[I2C](#i2c)
- 更少的RAM（192 KB vs. 256 KB）和闪存（1 MB vs. 2 MB）
- 与_Pixracer_相同的板尺寸，但外形尺寸稍小（因为连接器更少）
- 集成OSD（软件中尚未实现）

:::tip
所有常用的PX4功能仍然可以用于您的竞速机！
:::

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 主要特性

- 主系统芯片：[STM32F405RGT6](https://www.st.com/en/microcontrollers/stm32f405rg.html)
  - CPU：168 MHz ARM Cortex M4，带单精度FPU
  - RAM：192 KB SRAM
  - 闪存：1 MB
- 标准竞速机外形：36x36 mm，标准30.5 mm孔距
- MPU6000加速度计/陀螺仪
- BMP280气压计（并非所有板都安装）
- microSD（用于日志记录）
- Futaba S.BUS和S.BUS2 / Spektrum DSM2和DSMX / Graupner SUMD / PPM输入 / Yuneec ST24
- OneShot PWM输出（可配置）
- 内置电流传感器
- 内置OSD芯片（AB7456，通过SPI）

## 购买地点

该板由不同供应商生产，有一些变化（例如有或没有气压计）。

:::tip
PX4与支持Betaflight OMNIBUSF4SD目标的板兼容（如果产品页面上有_OMNIBUSF4SD_，该板应该与PX4兼容）。
:::

:::tip
任何标有Omnibus F4的衍生产品（例如克隆）也应该可以工作。但是，这些板上的电源分配质量参差不齐。
:::

这些是经过测试并已知可以工作的板：

- [Hobbywing XRotor Flight Controller F4](https://www.hobbywing.com/en/products/info.html?id=164)

  ::: info
  此板可以在不焊接的情况下安装在[Hobbywing XRotor Micro 40A 4合1 ESC](https://www.hobbywing.com/en/products/info.html?id=116)顶部。此ESC板还为Omnibus板提供电源。
  :::

  购买地点：
  - [Hobbywing XRotor F4 Flight Controller w/OSD](https://www.getfpv.com/hobbywing-xrotor-f4-flight-controller-w-osd.html) (getfpv)

- 原装Airbot Omnibus F4 SD

  购买地点：
  - [Airbot（中国制造商）](https://store.myairbot.com/omnibusf4prov3.html)
  - [Ready To Fly Quads（美国经销商）](https://quadsrtf.com/product/flip-32-f4-omnibus-rev-2/)

配件包括：

- [ESP8266 WiFi模块](../telemetry/esp8266_wifi_module.md)用于MAVLink遥测。
  您需要连接这些引脚：GND、RX、TX、VCC和CH-PD（CH-PD到3.3V）。波特率是921600。

## 连接器

基于此设计的不同供应商的板可能有显著不同的布局。
下面显示了各种版本的布局/丝印。

### Airbot Omnibus F4 SD

下面是Airbot Omnibus F4 SD（V1）的丝印，显示顶部和底部。

![Omnibus F4 SD v1 丝印顶部](../../assets/flight_controller/omnibus_f4_sd/silk-top.jpg)
![Omnibus F4 SD v1 丝印底部](../../assets/flight_controller/omnibus_f4_sd/silk-bottom.jpg)

### Hobbywing XRotor Flight Controller F4

下面是Hobbywing XRotor Flight Controller F4的丝印。

![Hobbywing XRotor Flight Controller F4 丝印](../../assets/flight_controller/omnibus_f4_sd/hobbywing_xrotor_silk.png)

## 引脚图

### 无线电控制

RC连接到以下端口之一：

- UART1
- SBUS/PPM端口（通过反相器，内部连接到UART1）

::: info
一些Omnibus F4板有一个跳线连接MCU SBUS和/或PPM到单个引脚接头。在使用前将跳线或焊接桥设置到适当的MCU引脚。
:::

### UART

- UART6：GPS端口
  - TX：MCU引脚PC6
  - RX：MCU引脚PC7

  - Airbot Omnibus F4 SD引脚图在端口J10（TX6/RX6）：

  ![Omnibus F4 SD UART6](../../assets/flight_controller/omnibus_f4_sd/uart6.jpg)

- UART4
  - TX：MCU引脚PA0
  - RX：MCU引脚PA1
  - 57600波特率
  - 可以配置为`TELEM 2`端口。
  - Airbot Omnibus F4 SD引脚图：
    - TX：RSSI引脚
    - RX：PWM输出5

  ![Omnibus F4 SD UART4](../../assets/flight_controller/omnibus_f4_sd/uart4.jpg)

  ![Omnibus F4 SD UART4 顶部](../../assets/flight_controller/omnibus_f4_sd/uart4-top.jpg)

### I2C

有一个I2C端口可用：

- SCL：MCU引脚PB10（可能标记为TX3）
- SDA：MCU引脚PB11（可能标记为RX3）

::: info
您需要在两个信号（时钟和数据）上外部上拉。
例如，您可以使用2.2k上拉电阻来连接外部磁力计。
:::

- Airbot Omnibus F4 SD引脚图在端口J10（SCL [时钟] / SCA [数据]）：
  <img src="../../assets/flight_controller/omnibus_f4_sd/uart6.jpg" title="Omnibus F4 SD UART6" />

这是一个示例实现。我使用Spektrum插头从DSM端口获取3.3v，仅通过2.2k电阻将3.3v +连接到每条线。

![Omnibus F4 SD上拉](../../assets/flight_controller/omnibus_f4_sd/pullup-schematic.jpg)

![Omnibus F4 SD上拉实现](../../assets/flight_controller/omnibus_f4_sd/pullup.jpg)

## 串口映射

| UART   | 设备       | 端口     |
| ------ | ---------- | -------- |
| USART1 | /dev/ttyS0 | SerialRX |
| USART4 | /dev/ttyS1 | TELEM1   |
| USART6 | /dev/ttyS2 | GPS      |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## RC遥测

Omnibus支持使用[FrSky遥测](../peripherals/frsky_telemetry.md)或[CRSF Crossfire遥测](#crsf_telemetry)向RC发射器发送遥测。

<a id="crsf_telemetry"></a>

### CRSF Crossfire遥测

[TBS CRSF遥测](../telemetry/crsf_telemetry.md)可用于将遥测数据从飞行控制器（飞行器的姿态、电池、飞行模式和GPS数据）发送到RC发射器，如Taranis。

相对于[FrSky遥测](../peripherals/frsky_telemetry.md)的好处包括：

- RC和遥测只需要一个UART。
- CRSF协议针对低延迟进行了优化。
- 150 Hz RC更新率。
- 信号未反相，因此不需要（外部）反相器逻辑。

::: info
如果您使用CRSF遥测，您需要构建自定义PX4固件。
相比之下，FrSky遥测可以使用预构建固件。
:::

对于Omnibus，我们推荐[TBS Crossfire Nano RX](https://www.team-blacksheep.com/products/prod:crossfire_nano_rx)，因为它专为小型四轴飞行器设计。

在手持控制器（例如Taranis）上，您还需要一个[发射器模块](https://www.team-blacksheep.com/shop/cat:tbs-crossfire-radio-transmitter#product_listing)。
这可以插入RC控制器的背面。

::: info
上述链接包含TX/RX模块的文档。
:::

#### 设置

按如下所示连接Nano RX和Omnibus引脚：

| Omnibus UART1 | Nano RX |
| ------------- | ------- |
| TX            | Ch2     |
| RX            | Ch1     |

接下来更新TX/RX模块以使用CRSF协议并设置遥测。
相关说明在[TBS Crossfire手册](https://www.team-blacksheep.com/media/files/tbs-crossfire-manual.pdf)中提供（搜索"设置无线电以使用CRSF"）。

#### PX4 CRSF配置

您需要构建自定义固件来使用CRSF。
更多信息请参见[CRSF遥测](../telemetry/crsf_telemetry.md#px4-configuration)。

<!-- no longer available 202507 -->

## PX4引导加载程序更新 {#bootloader}

该板预装了[Betaflight](https://github.com/betaflight/betaflight/wiki)。
在安装PX4固件之前，必须刷写_PX4引导加载程序_。
下载[omnibusf4sd_bl.hex](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/omnibus_f4_sd/omnibusf4sd_bl_d52b70cb39.hex)引导加载程序二进制文件，并阅读[此页面](../advanced_config/bootloader_update_from_betaflight.md)了解刷写说明。

## 构建固件

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make omnibus_f4sd_default
```

## 安装PX4固件

您可以使用预构建固件或您自己的自定义固件。

:::warning
如果您在无线电系统中使用[CRSF遥测](../telemetry/crsf_telemetry.md#px4-configuration)，如上所述，那么您必须使用自定义固件。
:::

固件可以通过任何正常方式安装：

- 构建和上传源代码

  ```
  make omnibus_f4sd_default upload
  ```

- 使用_QGroundControl_[加载固件](../config/firmware.md)。

## 配置

除了[基本配置](../config/index.md)之外，以下参数很重要：

| 参数                                                                   | 设置                                                                        |
| ---------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| [SYS_HAS_MAG](../advanced_config/parameter_reference.md#SYS_HAS_MAG)   | 这应该被禁用，因为板没有内部磁力计。如果您连接外部磁力计，可以启用它。     |
| [SYS_HAS_BARO](../advanced_config/parameter_reference.md#SYS_HAS_BARO) | 如果您的板没有气压计，请禁用此选项。                                        |

## 更多信息

[此页面](https://blog.unmanned.tech/omnibus-f4-flight-controller-guide/)提供了包含引脚图和设置说明的良好概述。
