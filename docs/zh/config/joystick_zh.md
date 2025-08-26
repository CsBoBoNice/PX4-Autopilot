# 摇杆设置

通过 _QGroundControl_ 连接的[计算机摇杆](https://en.wikipedia.org/wiki/Joystick)或游戏手柄可用于手动控制飞行器（_代替_使用[RC发射器](../config/radio.md)）。

此方法可用于具有集成地面控制站的手动控制单元（如下所示的 _UAVComponents_ [MicroNav](https://www.uxvtechnologies.com/ground-control-stations/micronav)）。
摇杆也常用于允许开发人员在仿真中飞行飞行器。

![摇杆MicroNav](../../assets/peripherals/joystick/micronav.jpg)

:::tip
如果仅使用摇杆，则不需要[无线电设置](../config/radio.md)（因为摇杆不是RC控制器）！
:::

::: info
_QGroundControl_ 使用跨平台[SDL2](https://www.libsdl.org/index.php)库将摇杆移动转换为MAVLink [MANUAL_CONTROL](https://mavlink.io/en/messages/common.html#MANUAL_CONTROL)消息，然后通过遥测通道发送到PX4。
因此，基于摇杆的控制器系统需要可靠的高带宽遥测通道，以确保飞行器对摇杆移动响应灵敏。
:::

## 启用PX4摇杆支持

有关如何设置摇杆的信息请参见：[QGroundControl > 摇杆设置](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/joystick.html)。

总结：

- 打开 _QGroundControl_
- 设置参数[COM_RC_IN_MODE=1](../advanced_config/parameter_reference.md#COM_RC_IN_MODE) - `摇杆`
  - 有关设置参数的信息，请参见[参数](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/parameters.html)
  - 在某些情况下，将参数设置为`2`或`3`也会启用摇杆。
- 连接摇杆
- 在**飞行器设置 > 摇杆**中配置连接的摇杆。
