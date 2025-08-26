# QAV-R 5" KISS ESC竞速机（Pixracer）

本主题提供了组装QAV-R 5" KISS ESC竞速机和使用_QGroundControl_配置PX4的完整说明。

## 关键信息

- **机架：** Lumenier QAV-R 5"
- **飞行控制器：** [Pixracer](../flight_controller/pixracer.md)

![QAV-R 5" KISS ESC竞速机](../../assets/airframes/multicopter/qav_r_5_kiss_esc_racer/qav_r_5_kiss_esc_racer_hero.jpg)

## 物料清单

用于此组装的组件：

- 飞行控制器：[Pixracer](../flight_controller/pixracer.md)
- 机架：[Lumenier QAV-R 5"](http://www.lumenier.com/products/multirotors/qav-r-fpv-racing-quadcopter)
- 电机：[Lumenier RX2206-11 2350KV](http://www.lumenier.com/products/motors/rx-series/rx2206-11-2350kv)
- 电调：[KISS ESC 2-5S 30A](http://www.flyduino.net/KISS-ESC-2-5S-30A_1)
- 螺旋桨：[HQProp 5x4.5x3 RaceKraft](http://www.lumenier.com/products/propellers/hqprop/hqprop-5x4-5x3-racekraft)
- GPS：[M8N GPS](https://store.3dr.com/products/3dr-gps-ublox-with-compass)
- 电源：[ISDT Q6 Plus](https://www.icharger.co.nz/products/isdt-q6-plus-300w-14s-pocket-lipo-charger)
- 数传：[Holybro 100mW 433MHz](https://holybro.com/products/sik-telemetry-radio-v3) 或 [Holybro 100mW 915MHz](https://holybro.com/products/sik-telemetry-radio-v3)
- 遥控：[FrSky Taranis](https://www.frsky-rc.com/product/taranis-q-x7-2/)
- 电池：[Team Blacksheep Graphene 1300mAh 4S 75C](https://www.team-blacksheep.com/products/prod:graphene_1300_4s_75c)

### 可选零件

- 摄像头：[RunCam Swift RR Edition](https://shop.runcam.com/runcam-swift-rotor-riot-special-edition/) FPV摄像头
- 接收器：[FrSky X4R-SB](https://www.frsky-rc.com/product/x4r-sb/)

## 硬件

### 机架

| 项目描述                 | 数量 |
| ----------------------- | ---- |
| 单体式顶板              | 1    |
| 单体式底板              | 1    |
| 飞行控制器固定板         | 1    |
| PDB                     | 1    |
| 摄像头板                | 1    |
| 35mm支柱                | 6    |
| 黑色尼龙螺丝和螺母       | 4    |
| 黑色钢螺丝              | 8    |
| 钢螺母                  | 8    |
| 7mm钢螺丝               | 12   |
| 魔术贴电池绑带           | 1    |
| 电池泡沫                | 1    |
| 着陆垫                  | 4    |

![QAV-R 5" 机架套件](../../assets/airframes/multicopter/qav_r_5_kiss_esc_racer/qav_r_5_frame_kit.jpg)

### 电子设备

| 项目描述                     | 数量 |
| --------------------------- | ---- |
| Pixracer自动驾驶仪           | 1    |
| KISS ESC 30A（BLHeli_S）     | 4    |
| M8N GPS + 罗盘              | 1    |
| FrSky X4R-SB接收器          | 1    |
| FrSky Taranis遥控器         | 1    |
| Lumenier RX2206-11 2350KV电机 | 4   |
| HQProp 5x4.5x3螺旋桨        | 1    |
| TBS Graphene 1300mAh 4S电池 | 1    |
| SiK数传电台                 | 1    |

### 所需工具

这次组装中使用以下工具：

- 2.0mm内六角螺丝刀
- 3mm十字螺丝刀
- 剪线钳
- 精密镊子
- 烙铁
- 热缩管

![所需工具](../../assets/airframes/multicopter/qav_r_5_kiss_esc_racer/qav_r_5_kiss_esc_racer_tools_required.jpg)

## 组装

估计组装时间约为3.5小时（机架组装2小时，自动驾驶仪安装和配置1.5小时）

### 机架组装

[详细组装步骤按原文档翻译...]

### 电子设备安装

[详细安装步骤按原文档翻译...]

## PX4配置

_QGroundControl_用于安装PX4自动驾驶仪并为机架配置/调整它。
为您的平台[下载并安装](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html) _QGroundControl_。

:::tip
安装和配置PX4的完整说明可以在[基本配置](../config/index.md)中找到。
:::

[配置步骤详细翻译...]
