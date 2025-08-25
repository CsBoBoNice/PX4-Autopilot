# 添加标准 MAVLink 定义（消息/命令）

本主题解释了如何添加期望成为常规 PX4 构建_一部分_的新 MAVLink 消息和命令。

## 标准 MAVLink 消息

PX4/PX4-Autopilot 源代码仅使用已被 MAVLink 标准化的消息。
也就是说，在发布版本中使用 [common.xml](https://mavlink.io/en/messages/common.html) 中的标准定义，在开发过程中使用 [development.xml](https://mavlink.io/en/messages/development.html)。
这些消息至少存在于一个重要的飞行栈中，并且其他飞行栈的成员已经接受它们作为合理的设计，如果需要相同功能的话可能会被采用。

::: tip
[自定义 MAVLink 消息](../mavlink/custom_messages.md) 是指不属于标准的消息。
这些消息在您自己的 PX4 分支中定义在您自己的 XML 中。
如果您使用 [自定义 MAVLink 消息](../mavlink/custom_messages.md)，您需要在 PX4、您的地面站以及与其通信的任何其他 SDK 中维护这些定义。
通常您应该尽可能使用（或添加到）标准定义，以减少维护负担。
:::

新的标准定义首先添加到 `development.xml`，然后在经过审查、原型制作和 MAVLink 团队接受后移动到 `common.xml`。

如果您打算让您的消息成为默认 PX4 构建的一部分，您需要通过向 [development.xml](https://github.com/mavlink/mavlink/blob/master/message_definitions/v1.0/development.xml) 提交拉取请求 (PR) 来向 MAVLink 社区提出建议。
[MAVLink 开发者指南](https://mavlink.io/en/getting_started/) 在 [如何定义 MAVLink 消息和枚举](https://mavlink.io/en/guide/define_xml_element.html) 中解释了如何定义新消息。

## 生成消息头文件

在开发过程中，您可以将您的定义添加到 `PX4-Autopilot/src/modules/mavlink/mavlink/message_definitions/v1.0/development.xml`（或从 MAVLink 拉取它们）。

当您构建 PX4 时，这些消息定义的头文件会在构建目录（`/build/<build target>/mavlink/`）中生成。
如果没有为您的消息构建头文件，它们可能格式错误或使用了冲突的 id。
检查构建日志以获取信息。

## 实现消息发送器/接收器

一旦在 PX4 构建中为您的定义生成了消息头文件，您就可以在代码中使用它们来发送和接收消息：

- [流式传输 MAVLink 消息](../mavlink/streaming_messages.md)
- [接收 MAVLink 消息](../mavlink/receiving_messages.md)

## 测试

调试的第一步是确认您创建的任何消息都按预期发送/接收。

您应该首先使用 `uorb top [<message_name>]` 命令来实时验证您的消息已发布以及频率（参见 [uORB 消息传递](../middleware/uorb.md#uorb-top-command)）。
这种方法也可以用来测试发布 uORB 主题的传入消息（对于其他消息，您可能在代码中使用 `printf` 并在 SITL 中测试）。

您可以使用几种方法来查看 MAVLink 流量：

- 为您的方言创建一个 [Wireshark MAVLink 插件](https://mavlink.io/en/guide/wireshark.html)。
  这允许您检查 IP 接口上的 MAVLink 流量 - 例如在 _QGroundControl_ 或 MAVSDK 与您的真实或模拟 PX4 版本之间。

  :::tip
  生成 wireshark 插件并在 Wireshark 中检查流量，比用您的方言重新构建 QGroundControl 并使用 MAVLink Inspector 要容易得多。
  :::

- [记录与您的 MAVLink 消息相关联的 uORB 主题](../dev_log/logging.md)。
- 在 QGroundControl [MAVLink Inspector](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/analyze_view/mavlink_inspector.html) 中查看接收到的消息。
  您需要 [使用新消息定义重新构建 QGroundControl](#updating-ground-stations)。

### 使用 Shell 设置流式传输速率

为了测试，有时在运行时增加个别主题的流式传输速率很有用（例如在 QGC 中检查）。
这可以通过 [QGC MAVLink 控制台](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/analyze_view/mavlink_console.html)（或其他一些 shell）调用 [mavlink](../modules/modules_communication.md#mavlink) 模块来实现：

```sh
mavlink stream -u <port number> -s <mavlink topic name> -r <rate>
```

您可以使用 `mavlink status` 获取端口号，它会输出（其中包括）`transport protocol: UDP (<port number>)`。
一个示例是：

```sh
mavlink stream -u 14556 -s CA_TRAJECTORY -r 300
```

## 更新地面站

最终您会希望通过提供相应的地面站或 MAVSDK 实现来使用您的新 MAVLink 接口。

这里要记住的重要一点是，MAVLink 要求您使用构建到相同定义（XML 文件）的库版本。
因此，如果您在 PX4 中创建了自定义消息，除非您使用相同的定义构建 QGC 或 MAVSDK，否则您将无法使用它。

### 更新 QGroundControl

您需要 [构建 QGroundControl](https://docs.qgroundcontrol.com/master/en/qgc-dev-guide/getting_started/index.html)，包括包含您的自定义消息的预构建 C 库。

QGC 使用必须位于 QGC 源代码中 [/qgroundcontrol/libs/mavlink/include/mavlink](https://github.com/mavlink/qgroundcontrol/tree/master/libs/mavlink/include/mavlink) 的预构建 C 库。

默认情况下，这作为来自 <https://github.com/mavlink/c_library_v2> 的子模块预先包含，但您可以 [生成您自己的 MAVLink 库](https://mavlink.io/en/getting_started/generate_libraries.html)。

QGC 默认使用 **all.xml** 方言，其中包括 **common.xml**。
您可以在任一文件中包含您的消息。

请注意，如果您使用自己的_自定义方言_，那么它应该包括 **ArduPilotMega.xml**（否则它会丢失所有现有消息），并且您需要通过在运行 _qmake_ 时在 [`MAVLINK_CONF`](https://github.com/mavlink/qgroundcontrol/blob/master/QGCExternalLibs.pri#L52) 中设置它来更改使用的方言。

### 更新 MAVSDK

有关如何使用 [MAVLink 头文件和方言](https://mavsdk.mavlink.io/main/en/cpp/guide/build.html) 的信息，请参阅 MAVSDK 文档。
