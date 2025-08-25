# 模块参考: 相机 (驱动程序)

## camera_trigger

源代码: [drivers/camera_trigger](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/camera_trigger)


### 描述

相机触发驱动程序。

此模块触发连接到飞控输出的相机，
或实现 MAVLink 触发协议的简单 MAVLink 相机。

驱动程序响应在任务中找到或通过 MAVLink 接收的以下 MAVLink 触发命令：

- `MAV_CMD_DO_TRIGGER_CONTROL`
- `MAV_CMD_DO_DIGICAM_CONTROL`
- `MAV_CMD_DO_SET_CAM_TRIGG_DIST`
- `MAV_CMD_OBLIQUE_SURVEY`

这些命令使驱动程序基于时间或距离触发相机图像捕获。
每次触发图像捕获时，都会发出 `CAMERA_TRIGGER` MAVLink 消息。

"简单 MAVLink 相机"是指支持上述命令集的相机。
当为此类相机配置时，驱动程序所做的就是按预期发出 `CAMERA_TRIGGER` MAVLink 消息。
传入的命令必须转发到 MAVLink 相机，并且在任务中找到时会自动发送到 MAVLink 通道。

驱动程序使用 [相机触发参数](../advanced_config/parameter_reference.md#camera-trigger) 进行配置。
特别是：

- `TRIG_INTERFACE` - 相机如何连接到飞控 (PWM, GPIO, Seagull, MAVLink)
- `TRIG_MODE` - 基于距离或时间的触发，值由 `TRIG_DISTANCE` 和 `TRIG_INTERVAL` 设置。

[设置/使用信息](../camera/index.md)。

### 用法 {#camera_trigger_usage}

```
camera_trigger <command> [arguments...]
 Commands:
   start

   stop          停止驱动程序

   status        打印驱动程序状态信息

   test          触发一张图像 (不记录或转发到地面站)

   test_power    切换电源
```