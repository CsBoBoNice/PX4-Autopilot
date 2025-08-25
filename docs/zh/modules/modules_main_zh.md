
# 模块和命令参考

以下页面记录了 PX4 模块、驱动程序和命令。
它们描述了提供的功能、高级实现概述以及如何
使用命令行界面。

::: info
**这是从源代码自动生成的**，包含最新的模块文档。
:::

这不是一个完整的列表，NuttX 还提供了一些额外的命令
（例如 `free`）。在控制台上使用 `help` 获取所有
可用命令的列表，在大多数情况下 `command help` 将打印用法。

由于这是从源代码生成的，错误必须在 [PX4-Autopilot](https://github.com/PX4/PX4-Autopilot) 仓库中报告/修复。
可以通过从 PX4-Autopilot 目录的根目录运行以下命令来生成文档页面：

```
make module_documentation
```
生成的文件将写入 `modules` 目录。

## 类别
- [自动调参](modules_autotune.md)
- [命令](modules_command.md)
- [通信](modules_communication.md)
- [控制器](modules_controller.md)
- [驱动程序](modules_driver.md)
- [估计器](modules_estimator.md)
- [仿真](modules_simulation.md)
- [系统](modules_system.md)
- [模板](modules_template.md)