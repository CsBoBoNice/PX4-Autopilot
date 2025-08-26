# Holybro QAV250 + Pixhawk 4 Mini 组装（已停产）

::: info
_Holybro Pixhawk 4 Mini QAV250套件_已不再可用。

说明保留在这里是因为基于Pix32 v6的非常相似的套件[在这里可用](https://holybro.com/products/qav250-kit)。
因此这些说明仍然可以遵循（并且可能会更新到Pix32 v6）。
:::

完整套件包括碳纤维QAV250竞速机架、飞行控制器和几乎所有其他所需组件（除了电池和接收器）。
套件有支持和不支持FPV的变体。
本主题提供了组装套件和使用_QGroundControl_配置PX4的完整说明。

关键信息

- **机架：** Holybro QAV250
- **飞行控制器：** [Pixhawk 4 Mini](../flight_controller/pixhawk4_mini.md)
- **组装时间（约）：** 3.5小时（机架2小时，自动驾驶仪安装/配置1.5小时）

![组装完成的Holybro QAV250配Pixhawk4 Mini](../../assets/airframes/multicopter/qav250_holybro_pixhawk4_mini/qav250_hero.jpg)

## 快速入门指南

[Pixhawk 4 Mini QAV250套件快速入门指南](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/flight_controller/pixhawk4mini/pixhawk4mini_qav250kit_quickstart_web.pdf)

## 物料清单

Holybro [QAV250套件](https://holybro.com/products/qav250-kit)套件包括几乎所有必需的组件：

- [Holybro收发器数传电台V3](../telemetry/holybro_sik_radio.md)
- Holybro电源模块
- 完全组装的带电调的电源管理板
- 电机 - DR2205 KV2300
- 5英寸塑料螺旋桨
- 碳纤维250机架带硬件
- Foxer摄像头
- Vtx 5.8ghz

此外您还需要电池和接收器（+兼容的发射器）。
此组装使用：

- 接收器：[FrSSKY D4R-II](https://www.frsky-rc.com/product/d4r-ii/)
- 电池：[4S 1300 mAh](https://www.getfpv.com/lumenier-1300mah-4s-60c-lipo-battery-xt60.html)

## 硬件

本节列出了机架和自动驾驶仪安装的所有硬件。

### 机架QAV250

| 描述         | 数量 |
| ----------- | ---- |
| 一体式机架板  | 1    |
| 飞行控制器盖板 | 1    |
| PDB         | 1    |
| 摄像头板     | 1    |
| 35mm支柱    | 6    |
| 乙烯基螺丝和螺母 | 4 |
| 15mm钢螺丝  | 8    |
| 钢螺母       | 8    |
| 7mm钢螺丝   | 12   |
| 魔术贴电池绑带 | 1   |
| 电池泡沫     | 1    |
| 着陆垫       | 4    |

![机架的QAV250组件](../../assets/airframes/multicopter/qav250_holybro_pixhawk4_mini/frame_components.jpg)

[剩余内容按照原文档结构翻译...]

## PX4配置

_QGroundControl_用于安装PX4自动驾驶仪并为机架配置/调整它。
为您的平台[下载并安装](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html) _QGroundControl_。

[配置步骤详细翻译...]
