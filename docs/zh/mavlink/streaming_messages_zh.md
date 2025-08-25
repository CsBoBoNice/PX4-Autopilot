# 流式传输 MAVLink 消息

本教程演示了如何将 uORB 消息作为 MAVLink 消息进行流式传输，适用于标准消息和自定义消息。

## 概述

[MAVLink 消息](../middleware/mavlink.md) 使用从 `MavlinkStream` 派生的流式传输类进行流式传输，该类已添加到 PX4 流列表中。
该类具有您实现的框架方法，以便 PX4 可以从生成的 MAVLink 消息定义中获取所需的信息。
它还有一个 `send()` 方法，每次需要发送消息时都会调用该方法 — 您重写此方法以将信息从 uORB 订阅复制到要发送的 MAVLink 消息对象。

一旦您创建了流式传输类，就可以按需流式传输相应的消息。
您还可以配置 PX4 默认流式传输消息，这取决于 MAVLink 配置。

## 先决条件

通常您已经有一个 [uORB](../middleware/uorb.md) 消息，其中包含您想要流式传输的信息，以及您想要流式传输的 MAVLink 消息的定义。

对于此示例，我们假设您想要将（现有的）[BatteryStatus](../msg_docs/BatteryStatus.md) uORB 消息流式传输到新的 MAVLink 电池状态消息，我们将其命名为 `BATTERY_STATUS_DEMO`。

将此 `BATTERY_STATUS_DEMO` 消息复制到您的 PX4 源代码中 `development.xml` 的消息部分，该文件位于：`\src\modules\mavlink\mavlink\message_definitions\v1.0\development.xml`。

```xml
    <message id="11514" name="BATTERY_STATUS_DEMO">
      <description>Simple demo battery.</description>
      <field type="uint8_t" name="id" instance="true">Battery ID</field>
      <field type="int16_t" name="temperature" units="cdegC" invalid="INT16_MAX">Temperature of the whole battery pack (not internal electronics). INT16_MAX field not provided.</field>
      <field type="uint8_t" name="percent_remaining" units="%" invalid="UINT8_MAX">Remaining battery energy. Values: [0-100], UINT8_MAX: field not provided.</field>
    </message>
```

::: info
请注意，这是尚未实现的 [BATTERY_STATUS_V2](https://mavlink.io/en/messages/development.html#BATTERY_STATUS_V2) 消息的精简版本，随机选择了未使用的 id `11514`。
在这里我们将消息放在 `development.xml` 中，这对于测试和如果消息最终打算成为标准消息集的一部分来说是可以的，但您也可能将 [自定义消息](../mavlink/custom_messages.md) 放在其自己的方言文件中。
:::

为 SITL 构建 PX4 并确认在 `/build/px4_sitl_default/mavlink/development/mavlink_msg_battery_status_demo.h` 中生成了相关消息。

因为 `BatteryStatus` 已经存在，您不需要做任何事情来创建或构建它。

## 定义流式传输类

首先在 [/src/modules/mavlink/streams](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mavlink/streams) 目录中为您的流式传输类（以要流式传输的消息命名）创建名为 `BATTERY_STATUS_DEMO.hpp` 的文件。

在文件顶部添加 uORB 消息的头文件（所需的 MAVLink 头文件应该已经可用）：

```cpp
#include <uORB/topics/battery_status.h>
```

::: info
uORB 主题的蛇形命名头文件是在构建时从驼峰命名的 uORB 文件名生成的。
:::

然后将下面的流式传输类定义复制到文件中：

```cpp
class MavlinkStreamBatteryStatusDemo : public MavlinkStream
{
public:
    static MavlinkStream *new_instance(Mavlink *mavlink)
    {
        return new MavlinkStreamBatteryStatusDemo(mavlink);
    }
    const char *get_name() const
    {
        return MavlinkStreamBatteryStatusDemo::get_name_static();
    }
    static const char *get_name_static()
    {
        return "BATTERY_STATUS_DEMO";
    }
    static uint16_t get_id_static()
    {
        return MAVLINK_MSG_ID_BATTERY_STATUS_DEMO;
    }
    uint16_t get_id()
    {
        return get_id_static();
    }
    unsigned get_size()
    {
        return MAVLINK_MSG_ID_BATTERY_STATUS_DEMO_LEN + MAVLINK_NUM_NON_PAYLOAD_BYTES;
    }

private:
    //Subscription to array of uORB battery status instances
    uORB::SubscriptionMultiArray<battery_status_s, battery_status_s::MAX_INSTANCES> _battery_status_subs{ORB_ID::battery_status};
    // SubscriptionMultiArray subscription is needed because battery has multiple instances.
    // uORB::Subscription is used to subscribe to a single-instance topic

    /* do not allow top copying this class */
    MavlinkStreamBatteryStatusDemo(MavlinkStreamBatteryStatusDemo &);
    MavlinkStreamBatteryStatusDemo& operator = (const MavlinkStreamBatteryStatusDemo &);

protected:
    explicit MavlinkStreamBatteryStatusDemo(Mavlink *mavlink) : MavlinkStream(mavlink)
    {}

	bool send() override
	{
		bool updated = false;

		// Loop through _battery_status_subs (subscription to array of BatteryStatus instances)
		for (auto &battery_sub : _battery_status_subs) {
            // battery_status_s is a struct that can hold the battery object topic
			battery_status_s battery_status;

			// Update battery_status and publish only if the status has changed
			if (battery_sub.update(&battery_status)) {
                // mavlink_battery_status_demo_t is the MAVLink message object
				mavlink_battery_status_demo_t bat_msg{};

				bat_msg.id = battery_status.id - 1;
				bat_msg.percent_remaining = (battery_status.connected) ? roundf(battery_status.remaining * 100.f) : -1;

				// check if temperature valid
				if (battery_status.connected && PX4_ISFINITE(battery_status.temperature)) {
					bat_msg.temperature = battery_status.temperature * 100.f;
				} else {
					bat_msg.temperature = INT16_MAX;
				}

                //Send the message
				mavlink_msg_battery_status_demo_send_struct(_mavlink->get_channel(), &bat_msg);
				updated = true;
			}
		}

		return updated;
	}

};
```

大多数流式传输类都非常相似（请参见 [/src/modules/mavlink/streams](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mavlink/streams) 中的示例）：

- 流式传输类从 [`MavlinkStream`](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_stream.h) 派生，并使用模式 `MavlinkStream<CamelCaseMessageName>` 命名。
- `public` 定义是"近似样板"，允许 PX4 获取类的实例 (`new_instance()`)，然后使用它从 MAVLink 头文件获取消息的名称、id 和大小 (`get_name()`、`get_name_static()`、`get_id_static()`、`get_id()`、`get_size()`)。
  对于您自己的流式传输类，这些可以直接复制并修改以匹配您的 MAVLink 消息的值。
- `private` 定义订阅需要发布的 uORB 主题。
  在这种情况下，uORB 主题有多个实例：每个电池一个。
  我们使用 `uORB::SubscriptionMultiArray` 获取电池状态订阅数组。

  在这里我们还定义构造函数以防止定义被复制。

- `protected` 部分是重要工作的地方！

  在这里我们重写 `send()` 方法，将订阅的 uORB 主题中的值复制到 MAVLink 消息中的适当字段，然后发送消息。

  在这个特定示例中，我们有一个 uORB 实例数组 `_battery_status_subs`（因为我们有多个电池）。
  我们遍历数组并在每个订阅上使用 `update()` 来检查关联的电池实例是否已更改（并使用当前数据更新结构）。
  这允许我们_仅当_关联的电池 uORB 主题发生更改时才发送 MAVLink 消息：

  ```cpp
  // Struct to hold current topic data.
  battery_status_s battery_status;

  // update() populates battery_status and returns true if the status has changed
  if (battery_sub.update(&battery_status)) {
     // Use battery_status to populate message and send
  }
  ```

  如果想要发送 MAVLink 消息而不管数据是否更改，我们可以改用 `copy()`，如下所示：

  ```cpp
  battery_status_s battery_status;
  battery_sub.copy(&battery_status);
  ```

  ::: info
  对于像 [VehicleStatus](../msg_docs/VehicleStatus.md) 这样的单实例主题，我们会这样订阅：

  ```cpp
  // Create subscription _vehicle_status_sub
  uORB::Subscription _vehicle_status_sub{ORB_ID(vehicle_status)};
  ```

  我们可以以相同的方式使用 update 或 copy 来使用结果订阅。

  ```cpp
  vehicle_status_s vehicle_status{}; // vehicle_status_s is the definition of the uORB topic
  if (_vehicle_status_sub.update(&vehicle_status)) {
    // Use the vehicle_status as it has been updated.
  }
  ```

  :::

接下来我们在 [mavlink_messages.cpp](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_messages.cpp#L2193) 中包含我们的新类。
将下面的行添加到文件中包含所有其他流的部分：

```cpp
#include "streams/BATTERY_STATUS_DEMO.hpp"
```

最后将流类附加到 [mavlink_messages.cpp](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_messages.cpp) 底部的 `streams_list`：

```C
StreamListItem *streams_list[] = {
...
#if defined(BATTERY_STATUS_DEMO_HPP)
    create_stream_list_item<MavlinkStreamBatteryStatusDemo>(),
#endif // BATTERY_STATUS_DEMO_HPP
...
}
```

该类现在可用于流式传输，但不会默认流式传输。
我们在下一节中介绍这一点。

## 默认流式传输

将消息默认流式传输（作为构建的一部分）的最简单方法是将它们添加到 [mavlink_main.cpp](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/mavlink_main.cpp) 中的适当消息组。

如果您在文件中搜索，您会在 switch 语句中找到定义的消息组：

- `MAVLINK_MODE_NORMAL`：流式传输到地面站。
- `MAVLINK_MODE_ONBOARD`：流式传输到快速链路上的伴随计算机，如以太网
- `MAVLINK_MODE_ONBOARD_LOW_BANDWIDTH`：流式传输到伴随计算机以重新路由到减少流量的链路，如地面站。
- `MAVLINK_MODE_GIMBAL`：流式传输到云台
- `MAVLINK_MODE_EXTVISION`：流式传输到外部视觉系统
- `MAVLINK_MODE_EXTVISIONMIN`：流式传输到较慢链路上的外部视觉系统
- `MAVLINK_MODE_OSD`：流式传输到 OSD，如 FPV 头显。
- `MAVLINK_MODE_CUSTOM`：默认不流式传输任何内容。用于使用 MAVLink 配置流式传输时使用。
- `MAVLINK_MODE_MAGIC`：与 `MAVLINK_MODE_CUSTOM` 相同
- `MAVLINK_MODE_CONFIG`：通过 USB 流式传输，速率高于 `MAVLINK_MODE_NORMAL`。
- `MAVLINK_MODE_MINIMAL`：流式传输最少的消息集。通常用于差的遥测链路。
- `MAVLINK_MODE_IRIDIUM`：流式传输到铱星卫星电话

通常您会在地面站上进行测试，所以您可以使用 `configure_stream_local()` 方法将消息添加到 `MAVLINK_MODE_NORMAL` 情况。
例如，以 5 Hz 流式传输 CA_TRAJECTORY：

```cpp
	case MAVLINK_MODE_CONFIG: // USB
		// Note: streams requiring low latency come first
		...
		configure_stream_local("BATTERY_STATUS_DEMO", 5.0f);
        ...
```

也可以通过在 [启动脚本](../concept/system_startup.md) 中使用 `stream` 参数调用 [mavlink](../modules/modules_communication.md#mavlink) 模块来添加流。
例如，您可能将以下行添加到 [/ROMFS/px4fmu_common/init.d-posix/px4-rc.mavlink](https://github.com/PX4/PX4-Autopilot/blob/main/ROMFS/px4fmu_common/init.d-posix/px4-rc.mavlink) 中，以便在 UDP 端口 `14556` 上以 50Hz 流式传输 `BATTERY_STATUS_DEMO`（`-r` 配置流式传输速率，`-u` 标识 UDP 端口 14556 上的 MAVLink 通道）。

```sh
mavlink stream -r 50 -s BATTERY_STATUS_DEMO -u 14556
```

## 按需流式传输

一些消息只在连接特定硬件或在其他情况下才需要。
为了避免使用不需要的消息堵塞通信链路，您可能不会默认流式传输所有消息，即使是低速率。

如果需要，地面站或其他 MAVLink API 可以使用 [MAV_CMD_SET_MESSAGE_INTERVAL](https://mavlink.io/en/messages/common.html#MAV_CMD_SET_MESSAGE_INTERVAL) 请求以特定速率流式传输特定消息。
可以使用 [MAV_CMD_REQUEST_MESSAGE](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_MESSAGE) 只请求一次特定消息。
