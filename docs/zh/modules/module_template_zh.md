# 完整应用程序的模块模板

应用程序可以编写为运行在 *任务*（具有自己堆栈和进程优先级的模块）或 *工作队列任务*（在工作队列线程上运行的模块，与其他工作队列上的任务共享堆栈和线程优先级）。

在大多数情况下可以使用工作队列任务，因为这样可以最小化资源使用。

::: info
[架构概述 > 运行时环境](../concept/architecture.md#runtime-environment) 提供了有关任务和工作队列任务的更多信息。
:::

::: info
在 [第一个应用程序教程](../modules/hello_sky.md) 中学到的所有内容都与编写完整应用程序相关。
:::

## 工作队列任务

PX4-Autopilot 包含一个用于编写作为 *工作队列任务* 运行的新应用程序（模块）的模板：
[src/examples/work_item](https://github.com/PX4/PX4-Autopilot/tree/main/src/examples/work_item)。

工作队列任务应用程序与普通（任务）应用程序相同，只是它需要指定自己是工作队列任务，并在初始化期间安排自己运行。

示例展示了如何操作。总结如下：
1. 在 cmake 定义文件 ([CMakeLists.txt](https://github.com/PX4/PX4-Autopilot/blob/main/src/examples/work_item/CMakeLists.txt)) 中指定对工作队列库的依赖：
   ```
   ...
   DEPENDS
      px4_work_queue
   ```
1. 除了 `ModuleBase`，任务还应该从 `ScheduledWorkItem` 派生（包含在 [ScheduledWorkItem.hpp]( https://github.com/PX4/PX4-Autopilot/blob/main/platforms/common/include/px4_platform_common/px4_work_queue/ScheduledWorkItem.hpp) 中）
1. 在构造函数初始化中指定要将任务添加到的队列。
   [work_item](https://github.com/PX4/PX4-Autopilot/blob/main/src/examples/work_item/WorkItemExample.cpp#L42) 示例将自己添加到 `wq_configurations::test1` 工作队列，如下所示：
   ```cpp
   WorkItemExample::WorkItemExample() :
	   ModuleParams(nullptr),
	   ScheduledWorkItem(MODULE_NAME, px4::wq_configurations::test1)
   {
   }
   ```

   ::: info
   可用的工作队列 (`wq_configurations`) 列在 [WorkQueueManager.hpp](https://github.com/PX4/PX4-Autopilot/blob/main/platforms/common/include/px4_platform_common/px4_work_queue/WorkQueueManager.hpp#L49) 中。
   :::

1. 实现 `ScheduledWorkItem::Run()` 方法来执行"工作"。
1. 实现 `task_spawn` 方法，指定任务是工作队列（使用 `task_id_is_work_queue` id）。
1. 使用调度方法之一调度工作队列任务（在示例中，我们在 `init` 方法中使用 `ScheduleOnInterval`）。



## 任务

PX4/PX4-Autopilot 包含一个用于编写作为任务在其自己的堆栈上运行的新应用程序（模块）的模板：
[src/templates/template_module](https://github.com/PX4/PX4-Autopilot/tree/main/src/templates/template_module)。

该模板演示了完整应用程序所需或有用的以下附加功能/方面：

- 访问参数并对参数更新做出反应。
- uORB 订阅和等待主题更新。
- 通过 `start`/`stop`/`status` 控制在后台运行的任务。
  然后可以将 `module start [<arguments>]` 命令直接添加到
  [启动脚本](../concept/system_startup.md) 中。
- 命令行参数解析。
- 文档：`PRINT_MODULE_*` 方法有两个目的（API 在
  [源代码中](https://github.com/PX4/PX4-Autopilot/blob/v1.8.0/src/platforms/px4_module.h#L381) 有文档）：
  - 当在控制台输入 `module help` 时，它们用于打印命令行用法。
  - 它们通过脚本自动提取以生成 [模块和命令参考](../modules/modules_main.md) 页面。