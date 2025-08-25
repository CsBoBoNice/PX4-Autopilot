# 自定义 MAVLink 消息

自定义 [MAVLink 消息](../middleware/mavlink.md) 是指不在默认包含到 PX4 中的标准 MAVLink 定义中的消息。

::: info
如果您使用自定义定义，您将需要分支并维护 PX4、您的地面站以及与其通信的任何其他 SDK。
通常您应该尽可能使用（或添加到）标准定义，以减少维护负担。
:::

## 添加自定义 XML

自定义定义可以添加到与 [使用标准 XML 定义时](../mavlink/adding_messages.md) 相同目录中的新方言文件中。
例如，创建 `PX4-Autopilot/src/modules/mavlink/mavlink/message_definitions/v1.0/custom_messages.xml`，并设置 `CONFIG_MAVLINK_DIALECT` 来为 SITL 构建新文件。
此方言文件应包括 `development.xml`，以便也包含所有标准定义。

对于初始原型制作，或者如果您打算让您的消息成为"标准"，您也可以将您的消息添加到 `common.xml`（或 `development.xml`）。
这简化了构建过程，因为您不需要修改所构建的方言。

MAVLink 开发者指南在 [如何定义 MAVLink 消息和枚举](https://mavlink.io/en/guide/define_xml_element.html) 中解释了如何定义新消息。

您可以通过检查构建目录（`/build/<build target>/mavlink/`）中生成的头文件来验证您的新消息是否已构建。
如果您的消息没有构建，它们可能格式不正确或使用了冲突的 id。
检查构建日志以获取信息。

一旦消息正在构建，您就可以流式传输、接收或以其他方式使用它，如以下部分所述。

::: info
[MAVLink 开发者指南](https://mavlink.io/en/getting_started/) 有更多关于使用 MAVLink 工具链的信息。
:::

## 创建自定义 MAVLink 消息的替代方案

有时需要内容不完全定义的自定义 MAVLink 消息。

例如，当使用 MAVLink 将 PX4 与嵌入式设备连接时，自动驾驶仪和设备之间交换的消息在稳定之前可能会经历多次迭代。
在这种情况下，重新生成 MAVLink 头文件并确保两个设备使用相同版本的协议可能既耗时又容易出错。

一个替代的 - 临时的 - 解决方案是重新使用调试消息。
您可以发送带有字符串键 `CA_TRAJ` 和 `x`、`y` 和 `z` 字段中数据的消息 `DEBUG_VECT`，而不是创建自定义 MAVLink 消息 `CA_TRAJECTORY`。
有关调试消息的示例用法，请参见 [本教程](../debug/debug_values.md)。

::: info
此解决方案效率不高，因为它通过网络发送字符串并涉及字符串比较。
它应该仅用于开发！
:::

## 测试和更新地面站

测试代码和更新地面站的方式与 [添加新标准 MAVLink 定义](../mavlink/adding_messages.md) 时相同。
