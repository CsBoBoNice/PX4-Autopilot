# 第一个应用程序教程（Hello Sky）

本主题介绍如何创建和运行您的第一个机载应用程序。
它涵盖了在PX4上进行应用程序开发所需的所有基本概念和API。

::: info
为了简化，省略了更高级的功能，如启动/停止功能和命令行参数。
这些内容在[应用程序/模块模板](../modules/module_template.md)中介绍。
:::

## 先决条件

您需要满足以下条件：

- [PX4 SITL仿真器](../simulation/index.md) _或者_ [PX4兼容的飞控](../flight_controller/index.md)。
- 针对目标平台的[PX4开发工具链](../dev_setup/dev_env.md)。
- 从Github[下载PX4源代码](../dev_setup/building_px4.md#download-the-px4-source-code)

源代码[PX4-Autopilot/src/examples/px4_simple_app](https://github.com/PX4/PX4-Autopilot/tree/main/src/examples/px4_simple_app)目录包含了本教程的完整版本，如果遇到困难可以参考。

- 重命名（或删除）**px4_simple_app**目录。

## 最小应用程序

在这一部分，我们创建一个_最小应用程序_，它只是打印出`Hello Sky!`。
这包括一个_C_文件和一个_cmake_定义（告诉工具链如何构建应用程序）。

1. 创建一个新目录**PX4-Autopilot/src/examples/px4_simple_app**。
1. 在该目录中创建一个名为**px4_simple_app.c**的新C文件：
   - 将默认头部复制到页面顶部。
     这应该出现在所有贡献的文件中！

     ```c
     /****************************************************************************
      *
      *   Copyright (c) 2012-2022 PX4 Development Team. All rights reserved.
      *
      * Redistribution and use in source and binary forms, with or without
      * modification, are permitted provided that the following conditions
      * are met:
      *
      * 1. Redistributions of source code must retain the above copyright
      *    notice, this list of conditions and the following disclaimer.
      * 2. Redistributions in binary form must reproduce the above copyright
      *    notice, this list of conditions and the following disclaimer in
      *    the documentation and/or other materials provided with the
      *    distribution.
      * 3. Neither the name PX4 nor the names of its contributors may be
      *    used to endorse or promote products derived from this software
      *    without specific prior written permission.
      *
      * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
      * "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
      * LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
      * FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
      * COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
      * INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
      * BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
      * OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
      * AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
      * LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
      * ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
      * POSSIBILITY OF SUCH DAMAGE.
      *
      ****************************************************************************/
     ```

   - 将以下代码复制到默认头部下方。
     这应该出现在所有贡献的文件中！

     ```c
     /**
      * @file px4_simple_app.c
      * PX4自动驾驶仪的最小应用程序示例
      *
      * @author Example User <mail@example.com>
      */

     #include <px4_platform_common/log.h>

     __EXPORT int px4_simple_app_main(int argc, char *argv[]);

     int px4_simple_app_main(int argc, char *argv[])
     {
     	PX4_INFO("Hello Sky!");
     	return OK;
     }
     ```

     :::tip
     主函数必须命名为`<module_name>_main`并从模块中导出，如图所示。
     :::

     :::tip
     `PX4_INFO`相当于PX4 shell的`printf`（从**px4_platform_common/log.h**包含）。
     有不同的日志级别：`PX4_INFO`、`PX4_WARN`、`PX4_ERR`、`PX4_DEBUG`。
     警告和错误还会被添加到[ULog](../dev_log/ulog_file_format.md)并显示在[Flight Review](https://logs.px4.io/)上。
     :::

1. 创建并打开一个名为**CMakeLists.txt**的新_cmake_定义文件。
   复制以下文本：

   ```cmake
   ############################################################################
   #
   #   Copyright (c) 2015 PX4 Development Team. All rights reserved.
   #
   # Redistribution and use in source and binary forms, with or without
   # modification, are permitted provided that the following conditions
   # are met:
   #
   # 1. Redistributions of source code must retain the above copyright
   #    notice, this list of conditions and the following disclaimer.
   # 2. Redistributions in binary form must reproduce the above copyright
   #    notice, this list of conditions and the following disclaimer in
   #    the documentation and/or other materials provided with the
   #    distribution.
   # 3. Neither the name PX4 nor the names of its contributors may be
   #    used to endorse or promote products derived from this software
   #    without specific prior written permission.
   #
   # THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
   # "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
   # LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
   # FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
   # COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
   # INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
   # BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
   # OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
   # AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
   # LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
   # ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
   # POSSIBILITY OF SUCH DAMAGE.
   #
   ############################################################################
   px4_add_module(
   	MODULE examples__px4_simple_app
   	MAIN px4_simple_app
   	STACK_MAIN 2000
   	SRCS
   		px4_simple_app.c
   	DEPENDS
   	)
   ```

   `px4_add_module()`方法从模块描述构建静态库。
   - `MODULE`块是模块的固件唯一名称（按约定，模块名称以父目录为前缀，直到`src`）。
   - `MAIN`块列出模块的入口点，它向NuttX注册命令，以便可以从PX4 shell或SITL控制台调用。

   :::tip
   `px4_add_module()`格式记录在[PX4-Autopilot/cmake/px4_add_module.cmake](https://github.com/PX4/PX4-Autopilot/blob/main/cmake/px4_add_module.cmake)中。 <!-- NEED px4_version -->
   :::

   ::: info
   如果您将`DYNAMIC`指定为`px4_add_module`的选项，则在POSIX平台上创建_共享库_而不是静态库（这些库可以在不重新编译PX4的情况下加载，并作为二进制文件而不是源代码与他人共享）。
   您的应用程序不会成为内置命令，而是在名为`examples__px4_simple_app.px4mod`的单独文件中结束。
   然后，您可以使用`dyn`命令在运行时加载文件来运行命令：`dyn ./examples__px4_simple_app.px4mod`
   :::

1. 创建并打开一个名为**Kconfig**的新_Kconfig_定义文件，并定义用于命名的符号（参见[Kconfig命名约定](../hardware/porting_guide_config.md#px4-kconfig-symbol-naming-convention)）。
   复制以下文本：

   ```
   menuconfig EXAMPLES_PX4_SIMPLE_APP
   	bool "px4_simple_app"
   	default n
   	---help---
   		Enable support for px4_simple_app
   ```

## 构建应用程序/固件

应用程序现在已经完成。
为了运行它，您首先需要确保它作为PX4的一部分构建。
应用程序在相应的板级_px4board_文件中添加到构建/固件中：

- PX4 SITL（仿真器）：[PX4-Autopilot/boards/px4/sitl/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/sitl/default.px4board)
- Pixhawk v1/2：[PX4-Autopilot/boards/px4/fmu-v2/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v2/default.px4board)
- Pixracer（px4/fmu-v4）：[PX4-Autopilot/boards/px4/fmu-v4/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v4/default.px4board)
- 其他板子的_px4board_文件可以在[PX4-Autopilot/boards/](https://github.com/PX4/PX4-Autopilot/tree/main/boards)中找到

要启用将应用程序编译到固件中，请在_px4board_文件中添加相应的Kconfig键`CONFIG_EXAMPLES_PX4_SIMPLE_APP=y`，或运行[boardconfig](../hardware/porting_guide_config.md#px4-menuconfig-setup) `make px4_fmu-v4_default boardconfig`：

```
examples  --->
    [x] PX4 Simple app  ----
```

::: info
对于大多数文件，该行已经存在，因为示例默认包含在固件中。
:::

使用板子特定的命令构建示例：

- jMAVSim仿真器：`make px4_sitl_default jmavsim`
- Pixhawk v1/2：`make px4_fmu-v2_default`（或只是`make px4_fmu-v2`）
- Pixhawk v3：`make px4_fmu-v4_default`
- 其他板子：[构建代码](../dev_setup/building_px4.md#building-for-nuttx)

## 测试应用程序（硬件）

### 将固件上传到您的板子

启用上传器，然后重置板子：

- Pixhawk v1/2：`make px4_fmu-v2_default upload`
- Pixhawk v3：`make px4_fmu-v4_default upload`

在您重置板子之前，它应该打印出一些编译消息，最后显示：

```sh
Loaded firmware for X,X, waiting for the bootloader...
```

板子重置并上传后，它会打印：

```sh
Erase  : [====================] 100.0%
Program: [====================] 100.0%
Verify : [====================] 100.0%
Rebooting.

[100%] Built target upload
```

### 连接控制台

现在通过串口或USB连接到[系统控制台](../debug/system_console.md)。
按**ENTER**会显示shell提示符：

```sh
nsh>
```

输入'help'并按ENTER

```sh
nsh> help
  help usage:  help [-v] [<cmd>]

  [           df          kill        mkfifo      ps          sleep
  ?           echo        losetup     mkrd        pwd         test
  cat         exec        ls          mh          rm          umount
  cd          exit        mb          mount       rmdir       unset
  cp          free        mkdir       mv          set         usleep
  dd          help        mkfatfs     mw          sh          xd

Builtin Apps:
  reboot
  perf
  top
  ..
  px4_simple_app
  ..
  sercon
  serdis
```

注意`px4_simple_app`现在是可用命令的一部分。
通过输入`px4_simple_app`并按ENTER来启动它：

```sh
nsh> px4_simple_app
Hello Sky!
```

应用程序现在已正确注册到系统中，可以扩展为执行有用的任务。

## 测试应用程序（SITL）

如果您使用SITL，_PX4控制台_会自动启动（参见[构建代码 > 第一次构建（使用仿真器）](../dev_setup/building_px4.md#first-build-using-a-simulator)）。
与_nsh控制台_一样（参见上一节），您可以输入`help`来查看内置应用程序列表。

输入`px4_simple_app`来运行最小应用程序。

```sh
pxh> px4_simple_app
INFO  [px4_simple_app] Hello Sky!
```

应用程序现在可以扩展为实际执行有用的任务。

## 订阅传感器数据

要做一些有用的事情，应用程序需要订阅输入并发布输出（例如电机或舵机命令）。

:::tip
PX4硬件抽象的优势在这里发挥作用！
无需以任何方式与传感器驱动程序交互，如果板子或传感器更新，也无需更新您的应用程序。
:::

应用程序之间的单个消息通道称为[主题](../middleware/uorb.md)。在本教程中，我们对[SensorCombined](https://github.com/PX4/PX4-Autopilot/blob/main/msg/SensorCombined.msg)主题感兴趣，它保存整个系统的同步传感器数据。

订阅主题很简单：

```cpp
#include <uORB/topics/sensor_combined.h>
..
int sensor_sub_fd = orb_subscribe(ORB_ID(sensor_combined));
```

`sensor_sub_fd`是一个主题句柄，可用于非常高效地执行阻塞等待新数据。
当前线程会休眠，一旦有新数据可用，调度器会自动唤醒它，等待时不消耗任何CPU周期。
为此，我们使用[poll()](https://pubs.opengroup.org/onlinepubs/007908799/xsh/poll.html) POSIX系统调用。

在订阅中添加`poll()`看起来像这样（_伪代码，完整实现见下文_）：

```cpp
#include <poll.h>
#include <uORB/topics/sensor_combined.h>
..
int sensor_sub_fd = orb_subscribe(ORB_ID(sensor_combined));

/* 可以使用这种技术等待多个主题，这里只使用一个 */
px4_pollfd_struct_t fds[] = {
    { .fd = sensor_sub_fd,   .events = POLLIN },
};

while (true) {
	/* 等待1个文件描述符的传感器更新1000毫秒（1秒） */
	int poll_ret = px4_poll(fds, 1, 1000);
	..
	if (fds[0].revents & POLLIN) {
		/* 获得第一个文件描述符的数据 */
		struct sensor_combined_s raw;
		/* 将传感器原始数据复制到本地缓冲区 */
		orb_copy(ORB_ID(sensor_combined), sensor_sub_fd, &raw);
		PX4_INFO("Accelerometer:\t%8.4f\t%8.4f\t%8.4f",
					(double)raw.accelerometer_m_s2[0],
					(double)raw.accelerometer_m_s2[1],
					(double)raw.accelerometer_m_s2[2]);
	}
}
```

通过输入以下命令重新编译应用程序：

```sh
make
```

### 测试uORB订阅

最后一步是通过在nsh shell中输入以下命令将您的应用程序作为后台进程/任务启动：

```sh
px4_simple_app &
```

您的应用程序将在控制台中显示5个传感器值，然后退出：

```sh
[px4_simple_app] Accelerometer:   0.0483          0.0821          0.0332
[px4_simple_app] Accelerometer:   0.0486          0.0820          0.0336
[px4_simple_app] Accelerometer:   0.0487          0.0819          0.0327
[px4_simple_app] Accelerometer:   0.0482          0.0818          0.0323
[px4_simple_app] Accelerometer:   0.0482          0.0827          0.0331
[px4_simple_app] Accelerometer:   0.0489          0.0804          0.0328
```

:::tip
[完整应用程序的模块模板](../modules/module_template.md)可用于编写可从命令行控制的后台进程。
:::

## 发布数据

为了使用计算的输出，下一步是_发布_结果。
下面我们展示如何发布姿态主题。

::: info
我们选择`attitude`是因为我们知道_mavlink_应用程序将其转发到地面控制站 - 提供了一种查看结果的简单方法。
:::

接口非常简单：初始化要发布的主题的`struct`并通告主题：

```c
#include <uORB/topics/vehicle_attitude.h>
..
/* 通告姿态主题 */
struct vehicle_attitude_s att;
memset(&att, 0, sizeof(att));
orb_advert_t att_pub_fd = orb_advertise(ORB_ID(vehicle_attitude), &att);
```

在主循环中，当信息准备好时发布：

```c
orb_publish(ORB_ID(vehicle_attitude), att_pub_fd, &att);
```

## 完整示例代码

[完整示例代码](https://github.com/PX4/PX4-Autopilot/blob/main/src/examples/px4_simple_app/px4_simple_app.c)现在是：

```c
/****************************************************************************
 *
 *   Copyright (c) 2012-2019 PX4 Development Team. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 * 1. Redistributions of source code must retain the above copyright
 *    notice, this list of conditions and the following disclaimer.
 * 2. Redistributions in binary form must reproduce the above copyright
 *    notice, this list of conditions and the following disclaimer in
 *    the documentation and/or other materials provided with the
 *    distribution.
 * 3. Neither the name PX4 nor the names of its contributors may be
 *    used to endorse or promote products derived from this software
 *    without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
 * "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
 * LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
 * FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
 * COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
 * INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
 * BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
 * OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
 * AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
 * LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
 * ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
 * POSSIBILITY OF SUCH DAMAGE.
 *
 ****************************************************************************/

/**
 * @file px4_simple_app.c
 * PX4自动驾驶仪的最小应用程序示例
 *
 * @author Example User <mail@example.com>
 */

#include <px4_platform_common/px4_config.h>
#include <px4_platform_common/tasks.h>
#include <px4_platform_common/posix.h>
#include <unistd.h>
#include <stdio.h>
#include <poll.h>
#include <string.h>
#include <math.h>

#include <uORB/uORB.h>
#include <uORB/topics/sensor_combined.h>
#include <uORB/topics/vehicle_attitude.h>

__EXPORT int px4_simple_app_main(int argc, char *argv[]);

int px4_simple_app_main(int argc, char *argv[])
{
	PX4_INFO("Hello Sky!");

	/* 订阅sensor_combined主题 */
	int sensor_sub_fd = orb_subscribe(ORB_ID(sensor_combined));
	/* 限制更新率为5 Hz */
	orb_set_interval(sensor_sub_fd, 200);

	/* 通告姿态主题 */
	struct vehicle_attitude_s att;
	memset(&att, 0, sizeof(att));
	orb_advert_t att_pub = orb_advertise(ORB_ID(vehicle_attitude), &att);

	/* 可以使用这种技术等待多个主题，这里只使用一个 */
	px4_pollfd_struct_t fds[] = {
		{ .fd = sensor_sub_fd,   .events = POLLIN },
		/* 这里可以有更多文件描述符，形式如下：
		 * { .fd = other_sub_fd,   .events = POLLIN },
		 */
	};

	int error_counter = 0;

	for (int i = 0; i < 5; i++) {
		/* 等待1个文件描述符的传感器更新1000毫秒（1秒） */
		int poll_ret = px4_poll(fds, 1, 1000);

		/* 处理poll结果 */
		if (poll_ret == 0) {
			/* 这意味着我们的提供者都没有给我们数据 */
			PX4_ERR("Got no data within a second");

		} else if (poll_ret < 0) {
			/* 这是严重错误 - 应该是紧急情况 */
			if (error_counter < 10 || error_counter % 50 == 0) {
				/* 使用计数器防止泛洪（并减慢我们的速度） */
				PX4_ERR("ERROR return value from poll(): %d", poll_ret);
			}

			error_counter++;

		} else {

			if (fds[0].revents & POLLIN) {
				/* 获得第一个文件描述符的数据 */
				struct sensor_combined_s raw;
				/* 将传感器原始数据复制到本地缓冲区 */
				orb_copy(ORB_ID(sensor_combined), sensor_sub_fd, &raw);
				PX4_INFO("Accelerometer:\t%8.4f\t%8.4f\t%8.4f",
					 (double)raw.accelerometer_m_s2[0],
					 (double)raw.accelerometer_m_s2[1],
					 (double)raw.accelerometer_m_s2[2]);

				/* 设置att并发布此信息给其他应用程序
				 以下没有任何意义，只是一个示例
				*/
				att.q[0] = raw.accelerometer_m_s2[0];
				att.q[1] = raw.accelerometer_m_s2[1];
				att.q[2] = raw.accelerometer_m_s2[2];

				orb_publish(ORB_ID(vehicle_attitude), att_pub, &att);
			}

			/* 这里可以有更多文件描述符，形式如下：
			 * if (fds[1..n].revents & POLLIN) {}
			 */
		}
	}

	PX4_INFO("exiting");

	return 0;
}
```

## 运行完整示例

最后运行您的应用程序：

```sh
px4_simple_app
```

如果您启动_QGroundControl_，您可以在实时图表中检查传感器值（[分析 > MAVLink检查器](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/analyze_view/mavlink_inspector.html)）。

## 总结

本教程涵盖了开发基本PX4自动驾驶仪应用程序所需的所有内容。
请记住，完整的uORB消息/主题列表[在此可用](https://github.com/PX4/PX4-Autopilot/tree/main/msg/)，头文件有很好的文档记录并作为参考。

更多信息和故障排除/常见陷阱可以在这里找到：[uORB](../middleware/uorb.md)。

下一页提供了一个编写具有启动和停止功能的完整应用程序的模板。
