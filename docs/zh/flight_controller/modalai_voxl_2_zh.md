# ModalAI VOXL 2

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://forum.modalai.com/)获取硬件支持或合规问题。
:::

ModalAI [VOXL 2](https://modalai.com/voxl-2)（[数据表](https://docs.modalai.com/voxl2-datasheets/)）是ModalAI围绕Qualcomm QRB5165处理器构建的下一代自主计算平台。VOXL 2拥有8核、集成PX4、七摄像头并发、高达15+ TOPS的先进板载AI和5G连接。重量仅16克，VOXL 2是完全自主和互联无人机的未来！

![VOXL-2](../../assets/flight_controller/modalai/voxl_2/voxl-2-hero.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 规格

### 系统

| 特性                                                                    | VOXL 2                                                           |
| ----------------------------------------------------------------------- | ---------------------------------------------------------------- |
| CPU                                                                     | QRB5165 <br>8核，最高3.091GHz <br>8GB LPDDR5<br>128GB闪存      |
| OS                                                                      | Ubuntu 18.04 - Linux内核v4.19                                   |
| GPU                                                                     | Adreno 650 GPU – 1024 ALU                                       |
| NPU                                                                     | 15 TOPS                                                          |
| 嵌入式飞行控制器                                                        | 是（传感器DSP，PX4）                                            |
| 内置WiFi                                                                | 否                                                               |
| 附加连接                                                                | WiFi、5G、4G/LTE、Microhard                                     |
| 视频编码                                                                | 8K30 h.264/h.265 108MP静态图像                                  |
| 计算机视觉传感器                                                        | 6个4通道CSI，4个CCI（例如2个立体对、高分辨率、跟踪）            |
| 跟踪传感器                                                              | 是                                                               |
| 尺寸                                                                    | 70mm x 36mm                                                      |
| 重量                                                                    | 16g                                                              |
| VOXL SDK：GPS拒止导航、SLAM、避障、物体识别                             | 是                                                               |
| ROS                                                                     | ROS 1和2                                                         |
| QGroundControl                                                          | 是                                                               |
| ATAK                                                                    | 是                                                               |
| NDAA '20第848节合规                                                     | 是，美国组装                                                     |
| PMD TOF                                                                 | 是（SDK 1.0及更新版本）                                         |
| FLIR Boson                                                              | USB                                                              |
| FLIR Lepton                                                             | USB、SPI                                                         |

::: info
更详细的硬件文档可以在[这里](https://docs.modalai.com/voxl-flight-datasheet/)找到。
:::

## 尺寸

### 2D尺寸

![VOXL2Dimensions](../../assets/flight_controller/modalai/voxl_2/voxl-2-dimensions.jpg)

### 3D尺寸

[3D STEP文件](https://storage.googleapis.com/modalai_public/modal_drawings/M0054_VOXL2_PVT_SIP_REVA.step)

## PX4固件兼容性

### voxl-dev分支

ModalAI正在积极维护可以使用的[分支PX4版本](https://github.com/modalai/px4-firmware/tree/voxl-dev)。

由于VOXL 2运行Ubuntu，VOXL 2的PX4生产版本通过[apt包管理](https://docs.modalai.com/configure-pkg-manager/)和[VOXL SDK](https://docs.modalai.com/voxl-sdk/)分发。

有关固件的更多信息可以在[这里](https://docs.modalai.com/voxl2-px4-developer-guide/)找到。

### main分支

PX4主线支持VOXL 2（板文档[这里](https://github.com/PX4/PX4-Autopilot/tree/main/boards/modalai/voxl2)）。

## QGroundControl支持

此板在QGroundControl 4.0及更高版本中受支持。

## 可用性

- [PX4自主开发套件](https://www.modalai.com/products/px4-autonomy-developer-kit)
- [Starling 2](https://www.modalai.com/products/starling-2)
- [Starling 2 MAX](https://www.modalai.com/products/starling-2-max)
- [由VOXL 2驱动的Sentinel开发无人机](https://www.modalai.com/pages/sentinel)
  - [演示视频](https://www.youtube.com/watch?v=hMhQgWPLGXo)
- [VOXL 2飞行甲板，即装即调即飞](https://www.modalai.com/collections/ready-to-mount/products/voxl-2-flight-deck)
- [VOXL 2开发套件](https://www.modalai.com/products/voxl-2)
  - [演示视频](https://www.youtube.com/watch?v=aVHBWbwp488)

## 快速入门

供应商的快速入门指南位于[这里](https://docs.modalai.com/voxl2-quickstarts/)。

### VOXL SDK

VOXL SDK（软件开发套件）包含开源的[voxl-px4](https://docs.modalai.com/voxl-px4/)、[核心库](https://docs.modalai.com/core-libs/)、[服务](https://docs.modalai.com/mpa-services/)、[工具](https://docs.modalai.com/inspect-tools/)、[实用程序](https://docs.modalai.com/sdk-utilities/)和[构建环境](https://docs.modalai.com/build-environments/)，ModalAI提供这些来加速VOXL计算板和配件的使用和开发。

VOXL SDK在VOXL、VOXL 2和RB5 Flight上运行！

VOXL SDK内项目的源代码可以在https://gitlab.com/voxl-public找到，以及构建说明。

### 连接器

有关引脚排列的详细信息可以在[这里](https://docs.modalai.com/voxl2-connectors/)找到，以及[视频概述](https://www.youtube.com/watch?v=xmqI3msjqdo)

![VOXLConnectors](../../assets/flight_controller/modalai/voxl_2/voxl-2-connectors.jpg)

B2B连接器J3、J5、J6、J7和J8上的所有单端信号都是1.8V CMOS，除非明确说明。
线缆到板连接器J10、J18和J19上的所有单端信号都是3.3V CMOS，除非明确说明。

| 连接器 | 描述                          | MPN（板侧）             | 配对MPN（板/线缆侧）          | 类型                         | 信号特性摘要                                                                                                                                                                                               |
| ------ | ----------------------------- | ----------------------- | ----------------------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| J2     | 风扇                          | SM02B-SRSS-TB(LF)(SN)   | SHR-02V-S                     | 线缆接头，2引脚直角          | 5V DC风扇 + PWM控制风扇回路（GND）                                                                                                                                                                        |
| J3     | 传统B2B                       | QSH-030-01-L-D-K-TR     | QTH-030-01-L-D-A-K-TR         | B2B插座，60引脚              | 5V/3.8V/3.3V/1.8V电源用于插件板，JTAG和调试信号，QUP扩展，GPIO，USB3.1 Gen 2（USB1）                                                                                                                    |
| J4     | 主电源输入                    | 22057045                | 0050375043                    | 线缆连接器，4引脚直角        | +5V主直流电源输入 + GND，I2C@5V用于电源监控器                                                                                                                                                             |
| J5     | 高速B2B                       | ADF6-30-03.5-L-4-2-A-TR | ADM6-30-01.5-L-4-2-A-TR       | B2B插座，120引脚             | 更多3.8V/3.3V/1.8V电源用于插件板，"SOM模式"5V电源输入，QUP扩展，GPIO（包括I2S），SDCC（SD卡V3.0），UFS1（辅助UFS闪存），2L PCIe Gen 3，AMUX和SPMI PMIC信号                                          |
| J6     | 摄像头组0                     | DF40C-60DP-0.4V(51)     | DF40C-60DS-0.4V               | B2B插头，60引脚              | 2个4L MIPI CSI端口，CCI和摄像头控制信号，8个电源轨（从1.05V到5V）用于摄像头和其他传感器，专用SPI（QUP）端口                                                                                             |
| J7     | 摄像头组1                     | DF40C-60DP-0.4V(51)     | DF40C-60DS-0.4V               | B2B插头，60引脚              | 2个4L MIPI CSI端口，CCI和摄像头控制信号，8个电源轨（从1.05V到5V）用于摄像头和其他传感器，专用SPI（QUP）端口                                                                                             |
| J8     | 摄像头组2                     | DF40C-60DP-0.4V(51)     | DF40C-60DS-0.4V               | B2B插头，60引脚              | 2个4L MIPI CSI端口，CCI和摄像头控制信号，8个电源轨（从1.05V到5V）用于摄像头和其他传感器，专用SPI（QUP）端口                                                                                             |
| J9     | USB-C（ADB）                  | UJ31-CH-3-SMT-TR        | USB Type-C                    | 线缆插座，24引脚直角         | ADB USB-C带重驱动器和显示端口替代模式（USB0）                                                                                                                                                             |
| J10    | SPI扩展                       | SM08B-GHS-TB(LF)(SN)    | GHR-08V-S                     | 线缆接头，8引脚直角          | SPI@3.3V带2个CS_N引脚，32kHz CLK_OUT@3.3V                                                                                                                                                                |
| J18    | ESC（SLPI访问）               | SM04B-GHS-TB(LF)(SN)    | GHR-04V-S                     | 线缆接头，4引脚直角          | ESC UART@3.3V，3.3V参考电压                                                                                                                                                                               |
| J19    | GNSS/MAG/RC/I2C（SLPI访问）   | SM12B-GHS-TB(LF)(SN)    | GHR-12V-S                     | 线缆接头，6引脚直角          | GNSS UART@3.3V，磁力计I2C@3.3V，5V，RC UART，备用I2C                                                                                                                                                     |

### 用户指南

VOXL 2的PX4用户指南可在[这里](https://docs.modalai.com/voxl-px4/)获取。

### 开发者指南

VOXL 2的PX4开发者指南可在[这里](https://docs.modalai.com/voxl-px4-developer-guide/)获取。

### 如何构建

有关如何构建的信息，请参见[VOXL PX4构建指南](https://docs.modalai.com/voxl2-px4-build-guide/)。

## 支持

请访问[ModalAI论坛](https://forum.modalai.com/category/26/voxl-2)获取更多信息。
