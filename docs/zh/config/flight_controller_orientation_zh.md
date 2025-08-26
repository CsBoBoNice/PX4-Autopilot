# 飞行控制器/传感器方向

默认情况下，飞行控制器和外部罗盘（如果存在）应放置在机架顶部朝上，定向使箭头指向飞行器前方。
如果板或任何外部罗盘以任何其他方向安装，则需要在固件中配置这一点。

## 计算方向

飞行控制器的横滚（ROLL）、俯仰（PITCH）和/或偏航（YAW）偏移是相对于飞行器围绕前进（x）、右（y）、下（z）轴计算的。

![机架朝向](../../assets/concepts/frame_heading.png)

旋转轴从一个旋转步骤到下一个保持相同。
因此执行旋转的坐标系保持固定。
这也称为_外旋转_。

![飞行器方向](../../assets/qgc/setup/sensor/fc_orientation_1.png)

例如，下面显示的飞行器绕z轴旋转（即仅偏航）对应于：`ROTATION_NONE`、`ROTATION_YAW_90`、`ROTATION_YAW_180`、`ROTATION_YAW_270`。

![偏航旋转](../../assets/qgc/setup/sensor/yaw_rotation.png)

::: info
对于VTOL尾座式机架，根据其多旋翼配置设置飞行器方向（即相对于起飞、悬停、着陆期间的飞行器）进行所有传感器校准。

轴通常相对于稳定前进飞行期间飞行器的方向。
更多信息请参见[基本概念](../getting_started/px4_basic_concepts.md#heading-and-directions)。
:::

## 设置飞行控制器方向

设置方向：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 选择**"Q"图标 > 飞行器设置 > 传感器**（侧边栏）打开_传感器设置_。
1. 选择**方向**按钮。

   ![设置传感器方向](../../assets/qgc/setup/sensor/sensor_orientation_set_orientations.jpg)

1. 选择**自动驾驶仪方向**（如[上面计算的](#calculating-orientation)）。

   ![方向选项](../../assets/qgc/setup/sensor/sensor_orientation_selector_values.jpg)

1. 按**确定**。

::: info
您可以使用[水平校准](../config/level_horizon_calibration.md)来补偿控制器方向的小偏差并在飞行视图中水平地平线。
:::

## 设置罗盘方向

PX4将在[罗盘校准](../config/compass.md)过程中自动检测罗盘方向（[默认](../advanced_config/parameter_reference.md#SENS_MAG_AUTOROT)），适用于任何[标准MAVLink方向](https://mavlink.io/en/messages/common.html#MAV_SENSOR_ORIENTATION)（正面朝上向前，或在任何轴上任何45°倍数偏移）。

::: info
您可以通过查看[CAL_MAGn_ROT](../advanced_config/parameter_reference.md#CAL_MAG0_ROT)参数来确认自动检测是否有效。
:::

如果使用了非标准方向，您需要为每个罗盘设置[CAL_MAGx_ROLL](../advanced_config/parameter_reference.md#CAL_MAG0_ROLL)、[CAL_MAGx_PITCH](../advanced_config/parameter_reference.md#CAL_MAG0_PITCH)和[CAL_MAGx_YAW](../advanced_config/parameter_reference.md#CAL_MAG0_YAW)参数为使用的角度。

这将自动将[CAL_MAGn_ROT](../advanced_config/parameter_reference.md#CAL_MAG0_ROT)设置为"自定义欧拉角"，并防止所选罗盘的自动校准（即使设置了[SENS_MAG_AUTOROT](../advanced_config/parameter_reference.md#SENS_MAG_AUTOROT)）。

## 更多信息

- [高级方向调参](../advanced_config/advanced_flight_controller_orientation_leveling.md)（仅限高级用户）。
- [QGroundControl用户指南 > 传感器](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors_px4.html#flight_controller_orientation)
