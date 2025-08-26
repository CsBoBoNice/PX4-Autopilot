# Holybro X500 + Pixhawk 4 组装

本主题提供了组装[Holybro X500套件](https://holybro.com/collections/x500-kits)和使用_QGroundControl_配置PX4的完整说明。

## 关键信息

- **套件：** [Holybro X500套件](https://holybro.com/collections/x500-kits)
- **飞行控制器：** [Pixhawk 4](../flight_controller/pixhawk4.md)
- **组装时间（约）：** 55分钟（机架25分钟，自动驾驶仪安装/配置30分钟）

![完整X500套件](../../assets/airframes/multicopter/x500_holybro_pixhawk4/x500_hero.png)

## 物料清单

Holybro [X500套件](https://holybro.com/collections/x500-kits)包括几乎所有必需的组件：

- X500机架套件
  - 机身 - 全碳纤维顶部和底部板（144 x 144mm，2mm厚）
  - 机臂 - 高强度和超轻量级16mm碳纤维管
  - 起落架 - 16mm和10mm直径碳纤维管
  - 平台板 - 带有GPS和流行伴随计算机的安装孔
  - 双10mm直径杆x 250mm长导轨安装系统
  - 带两个电池绑带的电池安装架
  - 安装手工工具
- Holybro电机 - 2216 KV880 x4
- Holybro BLHeli S电调20A x4
- 螺旋桨 - 1045 x4
- 电源分配板 - 电池XT60插头和电调及外设XT30插头

此组装中的其他零件（**套件中不包括**）：

- [Pixhawk 4自动驾驶仪](../flight_controller/pixhawk4.md)
- [M8N GPS](https://holybro.com/products/m8n-gps)
- [电源模块 - PM07](../power_module/holybro_pm07_pixhawk4_power_module.md)
- [433/915 MHz数传电台](../telemetry/holybro_sik_radio.md)

此外，如果您想手动控制无人机，您还需要电池（Holybro推荐4S 5000mAh）和接收器（[兼容的无线电系统](../getting_started/rc_transmitter_receiver.md)）。

## 套件硬件

本节列出了机架和自动驾驶仪安装的所有硬件。

| 项目              | 描述                      | 数量 |
| ---------------- | ------------------------ | ---- |
| 底板             | 碳纤维（2mm厚）           | 1    |
| 顶板             | 碳纤维（1.5mm厚）         | 1    |
| 机臂             | 碳纤维管（预装电机）       | 4    |
| 起落架 - 垂直杆   | 碳纤维管+工程塑料         | 2    |
| 起落架 - 横杆     | 碳纤维管+工程塑料+泡沫    | 2    |
| 安装导轨          | 直径：10mm长度：250mm    | 2    |
| 电池安装板        | 厚度：2mm                | 1    |
| 电池垫           | 3mm硅胶片黑色             | 1    |
| 平台板           | 厚度：2mm                | 1    |
| 吊环和橡胶环垫圈  | 内孔直径：10mm黑色        | 8    |

### 电子设备

| 项目描述                                                           | 数量 |
| ----------------------------------------------------------------- | ---- |
| Pixhawk 4及各种电缆                                                | 1    |
| M8N GPS模块                                                        | 1    |
| 电源模块PM07（预焊接电调电源电缆）                                 | 1    |
| 电机2216 KV880                                                     | 4    |
| Holybro BLHeli S电调20A x4                                         | 4    |
| 433 MHz / 915 MHz [Holybro数传电台](../telemetry/holybro_sik_radio.md) | 1    |

### 所需工具

套件包含组装工具，但您可能需要：

- 剪线钳
- 精密镊子

## 组装

估计组装时间为55分钟（机架25分钟，自动驾驶仪安装/配置30分钟）

[详细组装步骤按原文档翻译...]

## PX4配置

:::tip
安装和配置PX4的完整说明可以在[基本配置](../config/index.md)中找到。
:::

_QGroundControl_用于安装PX4自动驾驶仪并为X500机架配置/调整它。
为您的平台[下载并安装](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html) _QGroundControl_。

[配置步骤详细翻译...]
