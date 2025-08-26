# DJI FlameWheel 450 + CUAV V5 nano 组装

本主题提供了组装套件和使用_QGroundControl_配置PX4的完整说明。

关键信息

- **机架：** DJI F450
- **飞行控制器：** [CUAV V5 nano](../flight_controller/cuav_v5_nano.md)
- **组装时间（约）：** 90分钟（机架45分钟，自动驾驶仪安装/配置45分钟）

![完成设置](../../assets/airframes/multicopter/dji_f450_cuav_5nano/f450_cuav5_nano_complete.jpg)

## 物料清单

这个组装需要的组件有：

- 飞行控制器：[CUAV V5 nano](https://store.cuav.net/shop/v5-nano/)：
  - GPS：[CUAV NEO V2 GPS](https://store.cuav.net/index.php?id_product=97&id_product_attribute=0&rewrite=cuav-new-ublox-neo-m8n-gps-module-with-shell-stand-holder-for-flight-controller-gps-compass-for-pixhack-v5-plus-rc-parts-px4&controller=product&id_lang=1)
  - 电源模块
- 机架：[DJI F450](https://www.amazon.com/Flame-Wheel-Basic-Quadcopter-Drone/dp/B00HNMVQHY)
- 螺旋桨：[DJI Phantom内置螺母升级螺旋桨 9.4x5](https://www.masterairscrew.com/products/dji-phantom-built-in-nut-upgrade-propellers-in-black-mr-9-4x5-prop-set-x4-phantom)
- 电池：[Turnigy高容量5200mAh 3S 12C锂电池包带XT60](https://hobbyking.com/en_us/turnigy-high-capacity-5200mah-3s-12c-multi-rotor-lipo-pack-w-xt60.html?___store=en_us)
- 数传：[Holybro收发器数传电台V3](../telemetry/holybro_sik_radio.md)
- 遥控接收器：[FrSky D4R-II 2.4G 4CH ACCST遥测接收器](https://www.banggood.com/FrSky-D4R-II-2_4G-4CH-ACCST-Telemetry-Receiver-for-RC-Drone-FPV-Racing-p-929069.html?cur_warehouse=GWTR)
- 电机：[DJI E305 2312E电机 (960kv,CW)](https://www.amazon.com/DJI-E305-2312E-Motor-960kv/dp/B072MBMCZN)
- 电调：Hobbywing XRotor 20A APAC无刷电调 3-4S用于遥控多旋翼

此外，我们使用了FrSky Taranis控制器。
您还需要扎带、双面胶、电烙铁。

下图显示了机架和电子组件。

![此组装中使用的所有组件](../../assets/airframes/multicopter/dji_f450_cuav_5nano/all_components.jpg)

## 硬件

### 机架

本节列出了机架的所有硬件。

| 描述                           | 数量 |
| ----------------------------- | ---- |
| DJI F450底板                   | 1    |
| DJI F450顶板                   | 1    |
| DJI F450带起落架的腿            | 4    |
| M3\*8螺丝                     | 18   |
| M2 5\*6螺丝                   | 24   |
| 魔术贴电池绑带                 | 1    |
| DJI Phantom内置螺母升级螺旋桨 9.4x5 | 1    |

![F450机架组件](../../assets/airframes/multicopter/dji_f450_cuav_5nano/f450_frame_components.png)

### CUAV v5 nano套件

本节列出了CUAV v5 nano套件中的组件。

| 描述                | 数量（默认套件） | 数量（+GPS套件） |
| ------------------ | --------------- | --------------- |
| V5 nano飞行控制器   | 1               | 1               |
| DuPont电缆         | 2               | 2               |
| I2C/CAN电缆        | 2               | 2               |
| ADC 6.6电缆        | 2               | 2               |
| SBUS信号电缆       | 1               | 1               |
| IRSSI电缆          | 1               | 1               |
| DSM信号电缆        | 1               | 1               |
| ADC 3.3电缆        | 1               | 1               |
| 调试电缆           | 1               | 1               |
| 安全开关电缆       | 1               | 1               |
| 电压和电流电缆     | 1               | 1               |
| PW-Link模块电缆    | 1               | 1               |
| 电源模块           | 1               | 1               |
| SanDisk 16GB存储卡 | 1               | 1               |
| 12C扩展板          | 1               | 1               |
| TTL板             | 1               | 1               |
| NEO GPS           | -               | 1               |
| GPS支架           | -               | 1               |

### 电子设备

| 描述                                     | 数量 |
| --------------------------------------- | ---- |
| CUAV V5 nano                            | 1    |
| CUAV NEO V2 GPS                         | 1    |
| Holibro数传                             | 1    |
| FrSky D4R-II 2.4G 4CH ACCST遥测接收器   | 1    |
| DJI E305 2312E电机 (800kv,CW)           | 4    |
| Hobbywing XRotor 20A APAC无刷电调       | 4    |
| 电源模块（包含在CUAV V5 nano套件中）     | 1    |
| Turnigy高容量5200mAh 3S 12C锂电池包带XT60 | 1    |

### 所需工具

此组装中使用以下工具：

- 2.0mm内六角螺丝刀
- 3mm十字螺丝刀
- 剪线钳
- 精密镊子
- 电烙铁

![所需工具](../../assets/airframes/multicopter/dji_f450_cuav_5nano/required_tools.jpg)

## 组装

估计组装时间约为90分钟（机架约45分钟，自动驾驶仪安装和机架配置45分钟）。

1. 使用提供的螺丝将4个机臂连接到底板。

   ![机臂连接到底板](../../assets/airframes/multicopter/dji_f450_cuav_5nano/1_attach_arms_bottom_plate.jpg)

1. 将电调（电子调速器）焊接到板上，正极（红色）和负极（黑色）。

   ![焊接电调](../../assets/airframes/multicopter/dji_f450_cuav_5nano/2_solder_esc.jpg)

1. 焊接电源模块，正极（红色）和负极（黑色）。

   ![焊接电源模块](../../assets/airframes/multicopter/dji_f450_cuav_5nano/3_solder_power_module.jpg)

1. 根据位置将电机插入电调。

   ![插入电机](../../assets/airframes/multicopter/dji_f450_cuav_5nano/4_plug_in_motors.jpg)

1. 将电机连接到相应的机臂。

   ![将电机连接到机臂（白色）](../../assets/airframes/multicopter/dji_f450_cuav_5nano/5a_attach_motors_to_arms.jpg)
   ![将电机连接到机臂（红色）](../../assets/airframes/multicopter/dji_f450_cuav_5nano/5b_attach_motors_to_arms.jpg)

1. 添加顶板（拧入腿的顶部）。

   ![添加顶板](../../assets/airframes/multicopter/dji_f450_cuav_5nano/6_add_top_board.jpg)

1. 为_CUAV V5 nano_飞行控制器添加减振泡沫。

   ![减振泡沫](../../assets/airframes/multicopter/dji_f450_cuav_5nano/7a_attach_cuav5nano.jpg)
   ![减振泡沫](../../assets/airframes/multicopter/dji_f450_cuav_5nano/7b_attach_cuav5nano.jpg)

1. 用双面胶将FrSky接收器连接到底板。

   ![用双面胶连接FrSky接收器](../../assets/airframes/multicopter/dji_f450_cuav_5nano/8_attach_frsky.jpg)

1. 使用双面胶将数传模块连接到飞行器的底板。

   ![连接数传电台](../../assets/airframes/multicopter/dji_f450_cuav_5nano/9a_telemtry_radio.jpg)
   ![连接数传电台](../../assets/airframes/multicopter/dji_f450_cuav_5nano/9b_telemtry_radio.jpg)

1. 将铝制支柱放在按钮板上并连接GPS。

   ![铝制支柱](../../assets/airframes/multicopter/dji_f450_cuav_5nano/10_aluminium_standoffs.jpg)

1. 将数传（`TELEM1`）、GPS模块（`GPS/SAFETY`）、遥控接收器（`RC`）、所有4个电调（`M1-M4`）和电源模块（`Power1`）插入飞行控制器。
   ![将外设连接到飞行控制器](../../assets/airframes/multicopter/dji_f450_cuav_5nano/12_fc_attach_periperhals.jpg)

   ::: info
   电机顺序在[机架参考 > 四旋翼x](../airframes/airframe_reference.md#quadrotor-x)中定义
   :::

就是这样！
最终组装如下所示：

![完成设置](../../assets/airframes/multicopter/dji_f450_cuav_5nano/f450_cuav5_nano_complete.jpg)

## PX4配置

_QGroundControl_用于安装PX4自动驾驶仪并为机架配置/调整它。
为您的平台[下载并安装](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html) _QGroundControl_。

:::tip
安装和配置PX4的完整说明可以在[基本配置](../config/index.md)中找到。
:::

首先更新固件、机架、几何形状和输出：

- [固件](../config/firmware.md)
- [机架](../config/airframe.md)

  ::: info
  您需要选择_通用四旋翼_机架（**四旋翼x > 通用四旋翼**）。

  ![QGroundControl - 选择通用四旋翼](../../assets/airframes/multicopter/dji_f450_cuav_5nano/qgc_airframe_generic_quadx.png)
  :::

- [执行器](../config/actuators.md)
  - 更新飞行器几何形状以匹配机架。
  - 将执行器功能分配给输出以匹配您的接线。
  - 使用滑块测试配置。

然后执行强制设置/校准：

- [传感器方向](../config/flight_controller_orientation.md)
- [罗盘](../config/compass.md)
- [加速度计](../config/accelerometer.md)
- [水平校准](../config/level_horizon_calibration.md)
- [遥控设置](../config/radio.md)
- [飞行模式](../config/flight_mode.md)

  ::: info
  对于此组装，我们在接收器上的三位开关上设置了模式_稳定_、_高度_和_位置_（映射到单个通道 - 5）。
  这是推荐给初学者的最小模式集。
  :::

理想情况下，您还应该做：

- [电调校准](../advanced_config/esc_calibration.md)
- [电池估算调整](../config/battery.md)
- [安全](../config/safety.md)

## 调整

机架选择为机架设置_默认_自动驾驶仪参数。
这些可能足以飞行，但您应该调整每个机架组装。

有关如何操作的说明，请从[自动调整](../config/autotune_mc.md)开始。

## 视频

<lite-youtube videoid="b0bKNdDqVHw" title="CUAV Nano"/>

## 致谢

此组装日志由Dronecode测试飞行团队提供。
