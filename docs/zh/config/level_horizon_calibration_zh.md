# 水平校准

您可以使用_水平校准_来补偿控制器方向的小偏差，并在 _QGroundControl_ 飞行视图中水平地平线（蓝色在上，绿色在下）。

:::tip
仅当自动驾驶仪的方向与指定方向明显不对齐，或在非位置控制飞行模式下飞行中存在持续漂移时，才建议执行此校准步骤。
:::

## 执行校准

水平地平线：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 在顶部工具栏中选择**齿轮**图标（飞行器设置），然后在侧边栏中选择**传感器**。
1. 点击**水平校准**按钮。
   ![水平校准](../../assets/qgc/setup/sensor/sensor_level_horizon.png)
   ::: info
   您应该已经设置了[自动驾驶仪方向](../config/flight_controller_orientation.md)。如果没有，您也可以在这里设置。
   :::
1. 将飞行器放置在水平表面上的水平飞行方向：

   - 对于飞机，这是水平飞行期间的位置（飞机的机翼往往略微向上倾斜！）
   - 对于多旋翼，这是悬停位置。

1. 按**确定**开始校准过程。
1. 等待校准过程完成。

## 验证

检查飞行视图中显示的人工地平线在飞行器放置在水平表面时指示器是否在中间。

## 更多信息

- [高级方向调参](../advanced_config/advanced_flight_controller_orientation_leveling.md)（仅限高级用户）。
- [QGroundControl用户指南 > 传感器](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors_px4.html#level-horizon)
- [PX4设置视频"陀螺仪" - @1m14s](https://youtu.be/91VGmdSlbo4?t=1m14s) (Youtube)
