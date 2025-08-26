# 标准配置

本节涵盖大多数PX4飞行器所需的常见软件配置和校准。

您必须首先[加载固件并选择您的飞行器机架/类型](#firmware-vehicle-selection)。
大多数其他步骤可以不按顺序进行，除了[调参](#tuning)，必须最后进行。

## 先决条件

在开始之前，您应该[下载QGroundControl](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html)并将其安装在您的**桌面**计算机上。
然后打开QGC应用程序菜单（左上角的"Q"图标）并在_选择工具_弹出窗口中选择**飞行器设置**：

![QGC主菜单弹出窗口：突出显示飞行器设置](../../assets/qgc/setup/menu_setup.png)

## 配置步骤

### 固件/飞行器选择

- [加载固件](../config/firmware.md)
- [飞行器（机架）选择](../config/airframe.md)

### 电机/执行器设置

- [ESC校准](../advanced_config/esc_calibration.md)
- [执行器配置和测试](../config/actuators.md)

### 传感器校准

- [传感器方向](../config/flight_controller_orientation.md)
- [磁力计（罗盘）](../config/compass.md)
- [陀螺仪](../config/gyroscope.md)
- [加速度计](../config/accelerometer.md)
- [水平校准](../config/level_horizon_calibration.md)
- [空速](../config/airspeed.md)（仅固定翼/VTOL）
  - [空速验证](../advanced_config/airspeed_validation.md)。

::: info
这些和其他传感器的设置位于[传感器硬件和设置](../sensor/index.md)中。
:::

### 手动控制设置

无线电控制：

- [无线电控制器（RC）设置](../config/radio.md)
- [飞行模式配置](../config/flight_mode.md)

摇杆/游戏手柄：

- [摇杆设置](../config/joystick.md)

### 安全配置

- [电池估算调参](../config/battery.md)（需要[电源模块](../power_module/index.md)）
- [安全配置（故障保护）](../config/safety.md)

### 调参

自动调参受支持，并建议用于以下机架：

- [自动调参（多旋翼）](../config/autotune_mc.md)
- [自动调参（固定翼）](../config/autotune_fw.md)
- [自动调参（VTOL）](../config/autotune_vtol.md)

## 视频指南

下面的视频显示了大部分校准过程（它使用较旧版本的 _QGroundControl_，但大部分过程没有改变）。

<lite-youtube videoid="91VGmdSlbo4" title="PX4自动驾驶仪设置教程预览"/>

## 支持

如果您需要配置帮助，可以在[QGroundControl支持论坛](https://discuss.px4.io/c/qgroundcontrol/qgroundcontrol-usage/18)上寻求帮助。

## 另见

- [QGroundControl > 设置](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/setup_view.html)
- [飞行控制器外设](../peripherals/index.md) - 设置特定传感器、可选传感器、执行器等。
- [高级配置](../advanced_config/index.md) - 工厂/OEM校准、配置高级功能、不常见的配置。
- 以飞行器为中心的配置/调参：
  - [多旋翼配置/调参](../config_mc/index.md)
  - [直升机配置/调参](../config_heli/index.md)
  - [固定翼配置/调参](../config_fw/index.md)
  - [VTOL配置/调参](../config_vtol/index.md)
