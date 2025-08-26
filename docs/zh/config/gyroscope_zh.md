# 陀螺仪校准

_QGroundControl_ 将指导您将飞行器放在平坦表面上并保持静止。

## 执行校准

校准步骤如下：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 选择**"Q"图标 > 飞行器设置 > 传感器**（侧边栏）打开_传感器设置_。
1. 点击**陀螺仪**传感器按钮。

   ![选择陀螺仪校准PX4](../../assets/qgc/setup/sensor/gyroscope_calibrate_px4.png)

1. 将飞行器放在表面上并保持静止。
1. 点击**确定**开始校准。

   顶部的进度条显示进度：

   ![PX4陀螺仪校准进行中](../../assets/qgc/setup/sensor/gyroscope_calibrate_progress_px4.png)

1. 完成后，_QGroundControl_ 将显示进度条_校准完成_
   ![PX4陀螺仪校准完成](../../assets/qgc/setup/sensor/gyroscope_calibrate_complete_px4.png)

::: info
如果您移动飞行器，_QGroundControl_ 将自动重启陀螺仪校准。
:::

## 更多信息

- [QGroundControl用户指南 > 陀螺仪](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors_px4.html#gyroscope)
