# 飞行器（机架）选择

安装固件后，您需要选择一个[飞行器类型和机架配置](../airframes/airframe_reference.md)。
这将为所选机架应用适当的初始参数值，如飞行器类型、电机数量、相对电机位置等。
这些参数稍后可以在[执行器配置和测试](../config/actuators.md)中为您的飞行器进行自定义。

::: tip
如果存在与您的飞行器品牌和型号匹配的机架，请选择该机架，否则选择与您的飞行器最匹配的"通用"机架选项。
:::

## 设置机架

设置机架：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 选择**"Q"图标 > 飞行器设置 > 机架**（侧边栏）打开_机架设置_。
1. 选择与您的机架匹配的大的飞行器组/类型，然后使用组内的下拉菜单选择最匹配您的飞行器的机架。

   ![在QGroundControl中选择通用六旋翼X型机架](../../assets/qgc/setup/airframe/airframe_px4.jpg)

   上面的示例显示从_六旋翼X_组中选择了_通用六旋翼X几何_。

1. 点击**应用并重启**。
   在以下提示中点击**应用**以保存设置并重启飞行器。

   <img src="../../assets/qgc/setup/airframe/airframe_px4_apply_prompt.jpg" width="300px" title="应用机架选择提示" />

## 下一步

[执行器配置和测试](../config/actuators.md)显示如何设置飞行器电机和执行器的精确几何形状，以及它们到飞行控制器输出的映射。
在将执行器映射到输出后，如果使用PWM或OneShot ESC，您应该执行[ESC校准](../advanced_config/esc_calibration.md)。

## 更多信息

- [QGroundControl用户指南 > 机架](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/airframe.html)
- [PX4设置视频 - @37s](https://youtu.be/91VGmdSlbo4?t=35s) (Youtube)
