# 飞行报告

PX4 记录详细的飞行器状态和传感器数据，这些数据可用于分析性能问题。
本主题解释了如何下载和分析日志，并与开发团队分享以供审查。

:::tip
在某些司法管辖区，保留飞行日志是法律要求。
:::

## 从飞行控制器下载日志

可以使用 [QGroundControl](https://qgroundcontrol.com/) 下载日志：**[分析视图 > 日志下载](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/analyze_view/log_download.html)**。

![飞行日志下载](../../assets/qgc/analyze/log_download.jpg)

::: tip
加密的日志无法通过 QGroundControl 下载，也无法上传到公共的 Flight Review 服务。
下载和提取加密日志的最简单方法是使用[日志加密工具](../dev_log/log_encryption.md)。
您也可以托管一个[私有 Flight Review 服务器](../dev_log/log_encryption.md#flight-review-encrypted-logs)，它会在上传时使用您的私钥自动解密日志。
:::

## 分析日志

将日志文件上传到在线 [Flight Review](https://logs.px4.io/) 工具。
上传后，您将收到一封包含日志分析页面链接的电子邮件。

[使用 Flight Review 进行日志分析](../log/flight_review.md)解释了如何解释图表，可以帮助您验证/排除常见问题的原因：过度振动、PID 调优不当、控制器饱和、飞行器不平衡、GPS 噪声等。

::: info
还有许多其他优秀的工具用于可视化和分析 PX4 日志。
更多信息请参见：[飞行分析](../dev_log/flight_log_analysis.md)。
:::

:::tip
如果您与飞行器有恒定的高速率 MAVLink 连接（不仅仅是遥测链路），那么您可以使用 _QGroundControl_ 自动将日志直接上传到 _Flight Review_。
更多信息请参见[设置 > MAVLink 设置 > MAVLink 2 日志记录（仅限 PX4）](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/settings_view/mavlink.html#logging)。
:::

## 分享日志文件供 PX4 开发人员审查

[Flight Review](https://logs.px4.io/) 日志文件链接可以在[支持论坛](../contribute/support.md#forums-and-chat)或 [Github 问题](../index.md#reporting-bugs-issues)中分享讨论。

## 日志配置

日志系统默认配置为收集适合与 [Flight Review](https://logs.px4.io/) 一起使用的合理日志。

可以使用 [SD 日志记录](../advanced_config/parameter_reference.md#sd-logging)参数或 SD 卡上的文件进一步配置日志记录。
配置详细信息可在[日志记录配置文档](../dev_log/logging.md#configuration)中找到。

## 关键链接

- [Flight Review](https://logs.px4.io/)
- [使用 Flight Review 进行日志分析](../log/flight_review.md)
- [飞行日志分析](../dev_log/flight_log_analysis.md)
