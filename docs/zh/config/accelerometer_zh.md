# 加速度计校准

加速度计必须在首次使用时或飞行控制器方向改变时进行校准。
除此之外，不需要重新校准（除非在冬季，如果飞行控制器在工厂没有进行[热校准](../advanced_config/sensor_thermal_calibration.md)）。

::: info
糟糕的加速度计校准通常会被飞行前检查和解锁拒绝消息捕获（QGC警告通常指"高加速度计偏差"和"一致性检查失败"）。
:::

:::tip
这类似于[罗盘校准](../config/compass.md)，除了您需要在每个方向上保持飞行器静止（而不是旋转它）。
:::

## 执行校准

_QGroundControl_ 将指导您将飞行器放置并保持在多个方向（当需要移动到下一个位置时会提示您）。

校准步骤如下：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 选择**"Q"图标 > 飞行器设置 > 传感器**（侧边栏）打开_传感器设置_。
1. 点击**加速度计**传感器按钮。

   ![加速度计校准](../../assets/qgc/setup/sensor/accelerometer.png)

   ::: info
   您应该已经设置了[自动驾驶仪方向](../config/flight_controller_orientation.md)。
   如果没有，您也可以在这里设置。
   :::

1. 点击**确定**开始校准。
1. 按照屏幕上_图像_的指导放置飞行器。
   一旦提示（方向图像变为黄色），保持飞行器静止。
   当前方向的校准完成后，屏幕上相应的图像将变为绿色。

   ::: info
   校准使用最小二乘"拟合"算法，不需要您有"完美"的90度方向。
   只要在校准序列中的某个时候每个轴主要指向上方和下方，并且飞行器保持静止，精确的方向并不重要。
   :::

   ![加速度计校准](../../assets/qgc/setup/sensor/accelerometer_positions_px4.png)

1. 对所有飞行器方向重复校准过程。

一旦您在所有位置校准了飞行器，_QGroundControl_ 将显示_校准完成_（所有方向图像将显示为绿色，进度条将完全填满）。
然后您可以继续下一个传感器。

## 更多信息

- [QGroundControl用户指南 > 传感器](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors_px4.html#accelerometer)
- [PX4设置视频 - @1m46s](https://youtu.be/91VGmdSlbo4?t=1m46s) (Youtube)
