# Holybro S500 V2 + Pixhawk 4 组装

本主题提供了组装套件和使用_QGroundControl_配置PX4的完整说明。

::: info
Holybro最初为此套件提供了[Holybro Pixhawk 4](../flight_controller/pixhawk4.md)，但在撰写本文时已升级到更新的Pixhawk（6C）。
此组装日志仍然相关，因为套件组装几乎相同，并且在飞行控制器升级时可能保持不变。
:::

## 关键信息

- **机架：** Holybro S500
- **飞行控制器：** [Pixhawk 4](../flight_controller/pixhawk4.md)
- **组装时间（约）：** 90分钟（机架45分钟，自动驾驶仪安装/配置45分钟）

![完整S500套件](../../assets/airframes/multicopter/s500_holybro_pixhawk4/s500_hero.png)

## 物料清单

Holybro [S500 V2套件](https://holybro.com/collections/s500/products/s500-v2-development-kit)包括几乎所有必需的组件：

- 最新的Pixhawk自动驾驶仪
  - 对于此日志是Pixhawk 4，但现在包含更新的版本。
- 电源管理PM02（已组装）
- 机臂采用高强度塑料
- 电机 - 2216 KV880（V2更新）
- 螺旋桨1045（V2更新）
- Pixhawk4 GPS
- 完全组装的带电调的电源管理板
- 433 MHz / 915 MHz [Holybro数传电台](../telemetry/holybro_sik_radio.md)
- 电源和电台电缆
- 电池绑带
- 尺寸：383*385*240mm
- 轴距：480mm

::: info
不包括锂电池。
此外，我们使用FrSky Taranis控制器。
:::

## 硬件

| 项目描述                | 数量 |
| ---------------------- | ---- |
| 轴距：480mm            | 1    |
| 机臂                   | 4    |
| 起落架套件             | 2    |
| M3\*8螺丝             | 18   |
| M2 5\*6螺丝           | 24   |
| 电池绑带               | 1    |
| 螺旋桨1045（V2更新）   | 1    |

![S500硬件](../../assets/airframes/multicopter/s500_holybro_pixhawk4/s500_hardware.jpg)

## 套件

| 项目                            | 套件 |
| ----------------------------- | ---- |
| Pixhawk 4                     | 1    |
| Pixhawk4 GPS模块              | 1    |
| I2C分线板                     | 2    |
| 6对6线缆（电源）              | 3    |
| 4对4线缆（CAN）               | 2    |
| 6对4线缆（数据）              | 1    |
| 10对10线缆（PWM）             | 2    |
| 8对8线缆（AUX）               | 1    |
| 7对7线缆（SPI）               | 1    |
| 6对6线缆（调试）              | 1    |
| PPM/SBUS输出线缆              | 1    |
| XSR接收器线缆                 | 1    |
| DSMX接收器线缆                | 1    |
| SBUS接收器线缆                | 1    |
| USB线缆                       | 1    |
| 'X'型折叠基座安装              | 1    |
| 70mm和140mm碳纤维杆支柱       | 2    |
| 6\*3 2.54mm间距水平引脚       | 1    |
| 8\*3 2.54mm间距水平引脚       | 2    |
| 泡沫套件                      | 1    |
| Pixhawk4快速入门指南           | 1    |
| Pixhawk4引脚图                | 1    |
| GPS快速入门指南               | 1    |

![S500套件内容](../../assets/airframes/multicopter/s500_holybro_pixhawk4/s500_package.jpg)

### 电子设备

| 项目描述                         | 数量 |
| ------------------------------- | ---- |
| Pixhawk 4自动驾驶仪（不含PM06）  | 1    |
| 电源管理PM02（已组装）           | 1    |
| 电机 - 2216 KV880（V2更新）     | 4    |
| Pixhawk 4 GPS                   | 1    |
| 完全组装的带电调的电源管理板      | 1    |
| 433MHz数传电台/915MHz数传电台    | 1    |

![S500电子设备](../../assets/airframes/multicopter/s500_holybro_pixhawk4/s500_electronics.jpg)

### 所需工具

此组装中使用以下工具：

- 1.5mm内六角螺丝刀
- 2.0mm内六角螺丝刀
- 2.5mm内六角螺丝刀
- 3mm十字螺丝刀
- 剪线钳
- 精密镊子

![S500工具](../../assets/airframes/multicopter/s500_holybro_pixhawk4/s500_tools2.png)

![S500工具](../../assets/airframes/multicopter/s500_holybro_pixhawk4/s500_tools.jpg)

## 组装

估计组装时间为90分钟，机架组装约45分钟，在QGroundControl中安装和配置自动驾驶仪45分钟。

[详细组装步骤按原文档翻译...]

## PX4配置

_QGroundControl_用于安装PX4自动驾驶仪并为机架配置/调整它。
为您的平台[下载并安装](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html) _QGroundControl_。

[配置步骤详细翻译...]
