# 接收 MAVLink 消息

本主题解释了如何接收 [MAVLink 消息](../middleware/mavlink.md) 并将其发布到 uORB。

## 概述

本主题展示了我们如何处理接收到的 `BATTERY_STATUS_DEMO` 消息（如 [流式传输 MAVLink 消息](../mavlink/streaming_messages.md) 中定义的），然后使用包含的信息更新（现有的）[BatteryStatus uORB 消息](../msg_docs/BatteryStatus.md)。

这是您为支持与 PX4 的 MAVLink 电池集成而提供的实现类型。

## 步骤

在 [mavlink_receiver.h](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_receiver.h#L77) 中添加要发布到的 uORB 主题的头文件：

```cpp
#include <uORB/topics/battery_status.h>
```

在 [mavlink_receiver.h](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_receiver.h#L126) 的 `MavlinkReceiver` 类中为处理传入 MAVLink 消息的函数添加函数签名：

```cpp
void handle_message_battery_status_demo(mavlink_message_t *msg);
```

通常您会在 [mavlink_receiver.h](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_receiver.h#L296) 的 `MavlinkReceiver` 类中为要发布的 uORB 主题添加 uORB 发布器。
在这种情况下，[BatteryStatus](../msg_docs/BatteryStatus.md) uORB 主题已经存在：

```cpp
uORB::Publication<battery_status_s> _battery_pub{ORB_ID(battery_status)};
```

这创建了到单个 uORB 主题实例的发布，默认情况下是_第一个_实例。

::: info
此实现不适用于多电池系统，因为几个电池可能会向主题的第一个实例发布数据，并且无法区分它们。
要支持多个电池，我们需要使用 `PublicationMulti` 并将 MAVLink 消息实例 ID 映射到特定的 uORB 主题实例。
:::

在 [mavlink_receiver.cpp](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_receiver.cpp) 中实现 `handle_message_battery_status_demo` 函数。

```cpp
void
MavlinkReceiver::handle_message_battery_status_demo(mavlink_message_t *msg)
{
	if ((msg->sysid != mavlink_system.sysid) || (msg->compid == mavlink_system.compid)) {
		// ignore battery status coming from other systems or from the autopilot itself
		return;
	}

	// external battery measurements
	mavlink_battery_status_t battery_mavlink;
	mavlink_msg_battery_status_decode(msg, &battery_mavlink);

	battery_status_s battery_status{};
	battery_status.timestamp = hrt_absolute_time();

	battery_status.remaining = (float)battery_mavlink.battery_remaining / 100.0f;
	battery_status.temperature = (float)battery_mavlink.temperature;
	battery_status.connected = true;

	_battery_pub.publish(battery_status);
}
```

::: info
上面我们只写入主题中定义的电池字段。
在实际中，您会使用有效或无效值更新所有字段：为简洁起见，这已经被缩减了。
:::

最后确保在 [MavlinkReceiver::handle_message()](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_receiver.cpp#L228) 中调用它：

```cpp
MavlinkReceiver::handle_message(mavlink_message_t *msg)
 {
    switch (msg->msgid) {
        ...
    case MAVLINK_MSG_ID_BATTERY_STATUS_DEMO:
        handle_message_battery_status_demo(msg);
        break;
        ...
    }
 }
```
