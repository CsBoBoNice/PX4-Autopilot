# MAVLink 消息传递

[MAVLink](https://mavlink.io/en/) 是专为无人机生态系统设计的非常轻量级的消息传递协议。

PX4 使用 _MAVLink_ 与地面站和 MAVLink SDK（如 _QGroundControl_ 和 [MAVSDK](https://mavsdk.mavlink.io/)）进行通信，以及作为连接飞行控制器外部无人机组件的集成机制：伴随计算机、支持 MAVLink 的相机等。

本主题简要概述了基本的 MAVLink 概念，如消息、命令和微服务。
它还链接了如何为以下内容添加 PX4 支持的说明：

- [添加标准消息](../mavlink/adding_messages.md)
- [流式传输 MAVLink 消息](../mavlink/streaming_messages.md)
- [处理传入的 MAVLink 消息（并写入 uORB 主题）](../mavlink/receiving_messages.md)
- [自定义 MAVLink 消息](../mavlink/custom_messages.md)
- [协议/微服务](../mavlink/protocols.md)

::: info
我们尚未涵盖_命令_处理和发送，或如何实现您自己的微服务。
:::

## MAVLink 概述

MAVLink 是专为在不可靠的低带宽无线电链路上高效发送消息而设计的轻量级协议。

_消息_ 是 MAVLink 中最简单和最"基本"的定义，由名称（例如 [ATTITUDE](https://mavlink.io/en/messages/common.html#ATTITUDE)）、id 和包含相关数据的字段组成。
它们故意轻量级，具有约束的大小，并且没有重发和确认的语义。
独立消息通常用于流式传输遥测或状态信息，以及发送不需要确认的命令 - 如高频率发送的设定点命令。

[微服务](../mavlink/protocols.md) 是构建在 MAVLink 消息之上的"元协议"。
它们用于传达无法在单个消息中发送的信息。

例如，[命令协议](https://mavlink.io/en/services/command.html) 是用于发送可能需要确认和重传（服务质量）的命令的服务。
具体命令定义为 [MAV_CMD](https://mavlink.io/en/messages/common.html#mav_commands) 枚举的值，如起飞命令 [MAV_CMD_NAV_TAKEOFF](https://mavlink.io/en/messages/common.html#MAV_CMD_NAV_TAKEOFF)，并包括多达 7 个数字"参数"值。
该协议通过将参数值打包在 `COMMAND_INT` 或 `COMMAND_LONG` 消息中发送命令，并等待 `COMMAND_ACK` 中带有结果的确认。
如果没有收到确认，命令会自动重发多次。
请注意，[MAV_CMD](https://mavlink.io/en/messages/common.html#mav_commands) 定义也用于定义任务动作，并非所有定义都支持在 PX4 上用于命令/任务。

其他服务包括 [文件传输协议](https://mavlink.io/en/services/ftp.html)、[相机协议](https://mavlink.io/en/services/camera.html)、[参数协议](https://mavlink.io/en/services/parameter.html) 和 [任务协议](https://mavlink.io/en/services/mission.html)。
有关 PX4 支持什么的更多信息，请参见 [微服务](../mavlink/protocols.md)。

MAVLink 消息、命令和枚举在 [XML 定义文件](https://mavlink.io/en/guide/define_xml_element.html) 中定义。
MAVLink 工具链包括代码生成器，可从这些定义为发送和接收消息创建特定编程语言的库。
请注意，大多数生成的库不会创建代码来实现微服务。

MAVLink 项目标准化了多个消息、命令、枚举和微服务，用于使用以下定义文件交换数据（请注意，更高级别的文件_包括_下面文件的定义）：

- [development.xml](https://mavlink.io/en/messages/development.html) — 建议成为标准一部分的定义。
  在测试后如果被接受，这些定义会移到 `common.xml`。
- [common.xml](https://mavlink.io/en/messages/common.html) — 满足许多常见无人机用例的定义"库"。
  这些得到许多飞行栈、地面站和 MAVLink 外设的支持。
  使用这些定义的飞行栈更可能互操作。
- [standard.xml](https://mavlink.io/en/messages/standard.html) — 实际标准的定义。
  它们存在于绝大多数飞行栈中，并以相同的方式实现。
- [minimal.xml](https://mavlink.io/en/messages/minimal.html) — 最小 MAVLink 实现所需的定义。

该项目还托管 [方言 XML 定义](https://mavlink.io/en/messages/#dialects)，其中包含特定于飞行栈或其他利益相关者的 MAVLink 定义。

该协议依赖于通信的每一端都有发送消息的共享定义。
这意味着，为了进行通信，通信的两端都必须使用从相同 XML 定义生成的库。

<!--
The messages are sent over-the-wire in the "payload" of a [MAVLink packet](https://mavlink.io/en/guide/serialization.html#mavlink2_packet_format).
In order to reduce the amount of information that must be sent, the packet does not include the message metadata, such as what fields are in the message and so on.
Instead, the fields are serialized in a predefined order based on data size and XML definition order, and MAVLink relies on each end of the communication having a shared definition of what messages are being sent.
The shared identity of the message is conveyed by the message id, along with a CRC ("`CRC_EXTRA`") that uniquely identifies the message based on its name and id, and the field names and types.
The receiving end of the communication will discard any packet for which the message id and the `CRC_EXTRA` do not match.
-->

## PX4 和 MAVLink

PX4 发布版本默认构建 `common.xml` MAVLink 定义，以实现与 MAVLink 地面站、库和外部组件（如 MAVLink 相机）的最大兼容性。
在 `main` 分支中，SITL 包含来自 `development.xml` 的这些，其他板子使用 `common.xml`。

::: info
要成为 PX4 发布版本的一部分，您使用的任何 MAVLink 定义都必须在 `common.xml`（或包含的文件，如 `standard.xml` 和 `minimal.xml`）中。
在开发过程中，您可以使用 `development.xml` 中的定义。
您需要与 [MAVLink 团队](https://mavlink.io/en/contributing/contributing.html) 合作来定义和贡献这些定义。
:::

PX4 在 [/src/modules/mavlink](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mavlink) 下将 [mavlink/mavlink](https://github.com/mavlink/mavlink) 存储库作为子模块包含。
这包含 [/mavlink/messages/1.0/](https://github.com/mavlink/mavlink/blob/master/message_definitions/v1.0/) 中的 XML 定义文件。

构建工具链在构建时生成 MAVLink 2 C 头文件。
为其生成头文件的 XML 文件可以在 [PX4 kconfig 板子配置](../hardware/porting_guide_config.md#px4-board-configuration-kconfig) 中按板子基础定义，使用变量 `CONFIG_MAVLINK_DIALECT`：

- 对于 SITL，`CONFIG_MAVLINK_DIALECT` 在 [boards/px4/sitl/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/sitl/default.px4board#L36) 中设置为 `development`。
  您可以将其更改为任何其他定义文件，但该文件必须包含 `common.xml`。
- 对于其他板子，`CONFIG_MAVLINK_DIALECT` 默认不设置，PX4 构建 `common.xml` 中的定义（这些默认构建到 [mavlink 模块](../modules/modules_communication.md#mavlink) 中 — 在 [src/modules/mavlink/Kconfig](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/mavlink/Kconfig#L10) 中搜索 `menuconfig MAVLINK_DIALECT`）。

文件生成到构建目录：`/build/<build target>/mavlink/`。
