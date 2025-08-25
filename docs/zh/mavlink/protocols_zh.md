# MAVLink 微服务（协议）

MAVLink "微服务" 是使用组件之间交换的多个消息来传达更复杂信息的协议。
例如，[命令协议](https://mavlink.io/en/services/command.html) 提供了一种有效的机制，用于在（特定）消息中打包命令并在另一个消息中接收命令的确认。

MAVLink 微服务记录在 [MAVLink 指南](https://mavlink.io/en/services/) 中（这不是详尽的：并非所有消息都归类为协议，也不是所有协议都有文档记录）。

本节列出了此版本中已知受支持/不受支持的服务。

## 受支持的微服务

已知这些服务在某种形式下受支持：

- [电池协议](https://mavlink.io/en/services/battery.html)
  - [BATTERY_STATUS](https://mavlink.io/en/messages/common.html#BATTERY_STATUS) 和 [BATTERY_INFO](https://mavlink.io/en/messages/common.html#BATTERY_STATUS) 被流式传输。
- 相机协议
  - [相机协议 v2](https://mavlink.io/en/services/camera.html)
    - [相机定义](https://mavlink.io/en/services/camera_def.html)
- [命令协议](https://mavlink.io/en/services/command.html)
- [组件元数据协议](https://mavlink.io/en/services/component_information.html)
- [事件接口](https://mavlink.io/en/services/events.html)
- [文件传输协议 (FTP)](https://mavlink.io/en/services/ftp.html)
- 云台协议
  - [云台协议 v2](https://mavlink.io/en/services/gimbal_v2.html)
    - 可以通过 [云台配置](../advanced/gimbal_control.md#mavlink-gimbal-mnt-mode-out-mavlink) 启用
    - PX4 可以为一个与 FC 连接的云台充当 MAVLink 云台
- [心跳/连接协议](https://mavlink.io/en/services/heartbeat.html)
- [高延迟协议](https://mavlink.io/en/services/high_latency.html) — PX4 流式传输 [HIGH_LATENCY2](https://mavlink.io/en/messages/common.html#HIGH_LATENCY2)
- [图像传输协议](https://mavlink.io/en/services/image_transmission.html)
- [着陆目标协议](https://mavlink.io/en/services/landing_target.html)
- [手动控制（操纵杆）协议](https://mavlink.io/en/services/manual_control.html)
- [MAVLink ID 分配（sysid、compid）](https://mavlink.io/en/services/mavlink_id_assignment.html)
- [任务协议](https://mavlink.io/en/services/mission.html)
- [离板控制协议](https://mavlink.io/en/services/offboard_control.html)
- [远程 ID](../peripherals/remote_id.md) ([开放无人机 ID 协议](https://mavlink.io/en/services/opendroneid.html))
- [参数协议](https://mavlink.io/en/services/parameter.html)
- [扩展参数协议](https://mavlink.io/en/services/parameter_ext.html) — 允许设置字符串参数。用于设置相机定义文件中设置的字符串参数。
- [载荷协议](https://mavlink.io/en/services/payload.html)
- [Ping 协议](https://mavlink.io/en/services/ping.html)
- [标准模式协议](../mavlink/standard_modes.md)
- [地形协议](https://mavlink.io/en/services/terrain.html)
- [时间同步](https://mavlink.io/en/services/timesync.html)
- [交通管理 (UTM/ADS-B)](https://mavlink.io/en/services/traffic_management.html)
- [解锁授权协议](https://mavlink.io/en/services/arm_authorization.html)

## 不受支持

这些服务不受 PX4 支持/使用：

- [照明器协议](https://mavlink.io/en/services/illuminator.html)
- [隧道协议](https://mavlink.io/en/services/tunnel.html)
