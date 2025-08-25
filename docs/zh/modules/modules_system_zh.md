# 模块参考: 系统

## battery_simulator

源代码: [modules/simulation/battery_simulator](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/battery_simulator)

### 描述

### 用法 {#battery_simulator_usage}

```
battery_simulator <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## battery_status

源代码: [modules/battery_status](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/battery_status)

### 描述

提供的功能包括：

- 读取 ADC 驱动程序的输出（通过 ioctl 接口）并发布 `battery_status`。

### 实现

它在自己的线程中运行，并轮询当前选择的陀螺仪主题。

### 用法 {#battery_status_usage}

```
battery_status <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## camera_feedback

源代码: [modules/camera_feedback](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/camera_feedback)

### 描述

camera_feedback 模块在图像捕获被触发时发布 `CameraCapture` UORB 主题。

如果启用了相机捕获，则发布来自相机捕获引脚的触发信息；
否则发布在命令相机触发时的触发信息
（来自 `camera_trigger` 模块）。

然后根据 `CameraCapture` 更新发出 `CAMERA_IMAGE_CAPTURED` 消息（由流代码）。
`CameraCapture` 主题也会被记录，可用于地理标记。

### 实现

`CameraTrigger` 主题由 `camera_trigger` 模块发布（`feedback` 字段设置为 `false`）
当图像捕获被触发时，如果相机捕获引脚被激活，
也可能由 `camera_capture` 驱动程序发布（`feedback` 字段设置为 `true`）。

`camera_feedback` 模块订阅 `CameraTrigger`。
如果启用了相机捕获，它会丢弃来自 `camera_trigger` 模块的主题。
对于未被丢弃的主题，它创建一个 `CameraCapture` 主题，其中包含
来自 `CameraTrigger` 的时间戳信息和来自飞行器的位置信息。

### 用法 {#camera_feedback_usage}

```
camera_feedback <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## cdcacm_autostart

源代码: [drivers/cdcacm_autostart](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/cdcacm_autostart)

### 描述

此模块监听 USB 并根据接收到的字节自动配置协议。
支持的协议有：MAVLink、nsh 和 ublox 串行直通。如果参数 SYS_USB_AUTO=2
模块将只在检测到 USB VBUS 时尝试启动 mavlink。否则它将旋转
并继续检查 VBUS 并在检测到时启动 mavlink。

### 用法 {#cdcacm_autostart_usage}

```
cdcacm_autostart <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## commander

源代码: [modules/commander](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/commander)

### 描述

commander 模块包含模式切换和故障保护行为的状态机。

### 用法 {#commander_usage}

```
commander <command> [arguments...]
 Commands:
   start
     [-h]        启用 HIL 模式

   calibrate     运行传感器校准
     mag|baro|accel|gyro|level|esc|airspeed 校准类型
     quick       快速校准 [mag, accel (不推荐)]

   check         运行飞行前检查

   arm
     [-f]        强制解锁（不运行飞行前检查）

   disarm
     [-f]        强制上锁（空中上锁）

   takeoff

   land

   transition    VTOL 转换

   mode          更改飞行模式
     manual|acro|offboard|stabilized|altctl|posctl|position:slow|auto:mission|au
                 to:loiter|auto:rtl|auto:takeoff|auto:land|auto:precland|ext1
                 飞行模式

   pair

   termination
     on|off      打开或关闭锁定

   set_ekf_origin
     lat, lon, alt 原点纬度、经度、海拔

   lat|lon|alt   原点纬度经度海拔

   poweroff      关闭板子（如果支持）

   stop

   status        打印状态信息
```

## dataman

源代码: [modules/dataman](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/dataman)

### 描述

模块以简单数据库的形式通过 C API 为系统其余部分提供持久存储。
根据板子支持多个后端：

- 文件（例如在 SD 卡上）
- RAM（这显然不是持久的）

它用于存储不同类型的结构化数据：任务航点、任务状态和地理围栏多边形。
每种类型都有特定的类型和固定的最大存储项目数量，以便快速随机访问。

### 实现

读取和写入单个项目始终是原子的。

### 用法 {#dataman_usage}

```
dataman <command> [arguments...]
 Commands:
   start
     [-f <val>]  存储文件
                 值: <file>
     [-r]        使用 RAM 后端（非持久）

 选项 -f 和 -r 是互斥的。如果未指定任何内容，则使用文件 'dataman'

   stop

   status        打印状态信息
```

## dmesg

源代码: [systemcmds/dmesg](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/dmesg)

### 描述

用于显示启动控制台消息的命令行工具。
请注意，NuttX 工作队列和 syslog 的输出不会被捕获。

### 示例

在后台持续打印所有消息：

```
dmesg -f &
```

### 用法 {#dmesg_usage}

```
dmesg <command> [arguments...]
 Commands:
     [-f]        跟随：等待新消息
```

## esc_battery

源代码: [modules/esc_battery](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/esc_battery)

### 描述

这实现了使用来自 ESC 状态的信息并将其发布为电池状态。

### 用法 {#esc_battery_usage}

```
esc_battery <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## gyro_calibration

源代码: [modules/gyro_calibration](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/gyro_calibration)

### 描述

简单的在线陀螺仪校准。

### 用法 {#gyro_calibration_usage}

```
gyro_calibration <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## gyro_fft

源代码: [modules/gyro_fft](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/gyro_fft)

### 描述

### 用法 {#gyro_fft_usage}

```
gyro_fft <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## hardfault_stream

源代码: [modules/hardfault_stream](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/hardfault_stream)

### 描述

通过 MAVLink 流式传输最新硬故障的后台进程。

当需要快速将硬故障推送到地面站时，该模块特别有用。
这在无人机在飞行中遇到硬故障时很有用。
它确保在 crash 期间永久存储被破坏时保留一些数据。

为了可靠地流式传输，有必要以足够高的频率通过 MAVLink 发送 STATUSTEXT 消息。
推荐的频率是 10 Hz 或更高。

### 用法 {#hardfault_stream_usage}

```
hardfault_stream <command> [arguments...]
 Commands:
   start         启动后台任务

   stop

   status        打印状态信息
```

## heater

源代码: [drivers/heater](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/heater)

### 描述

在 LP 工作队列上定期运行的后台进程，用于将 IMU 温度调节到设定点。

此任务可以通过在启动脚本中设置 SENS_EN_THERMAL 或通过 CLI 在启动时启动。

### 用法 {#heater_usage}

```
heater <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## i2c_launcher

源代码: [systemcmds/i2c_launcher](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/i2c_launcher)

### 描述

基于找到的 I2C 设备启动驱动程序的守护进程。

### 用法 {#i2c_launcher_usage}

```
i2c_launcher <command> [arguments...]
 Commands:
   start
     -b <val>    总线号
     -t <val>    用于校准值的电池索引 (1 或 3)

   stop

   status        打印状态信息
```

## internal_combustion_engine_control

源代码: [modules/internal_combustion_engine_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/internal_combustion_engine_control)

### 描述

该模块控制内燃机 (ICE) 功能，包括：
点火（开/关）、节气门和阻风门水平、启动发动机延迟和用户请求。

### 启用

此功能默认未启用，需要在您的板子的构建目标中配置
以及 rpm 捕获驱动程序：

```
CONFIG_MODULES_INTERNAL_COMBUSTION_ENGINE_CONTROL=y
CONFIG_DRIVERS_RPM_CAPTURE=y
```

此外，要启用模块：

- 设置 [ICE_EN](../advanced_config/parameter_reference.md#ICE_EN)
  为 true 并根据您的需要调整其他 `ICE_` 模块参数。
- 设置 [RPM_CAP_ENABLE](../advanced_config/parameter_reference.md#RPM_CAP_ENABLE) 为 true。

该模块输出点火、节气门和阻风门的控制信号，
并从 RPM 传感器获取输入。
这些必须在 [执行器配置](../config/actuators.md) 中映射到 AUX 输出/输入，
类似于下面显示的设置。

![ICE 的执行器设置](../../assets/hardware/ice/ice_actuator_setup.png)

### 实现

ICE 用 (4) 状态机实现：

![架构](../../assets/hardware/ice/ice_control_state_machine.png)

状态机：

- 检查 [Rpm.msg](../msg_docs/Rpm.md) 是否更新以知道发动机是否在运行
- 允许用户输入来自：
  - 手动控制 AUX
  - [VehicleStatus.msg](../msg_docs/VehicleStatus.md) 中的解锁状态
- 在"停止"状态下，节气门设置为 NAN，根据定义将
  节气门输出设置为为特定输出配置的解锁值。

该模块发布 [InternalCombustionEngineControl.msg](../msg_docs/InternalCombustionEngineControl.md)。

架构如下所示：

![架构](../../assets/hardware/ice/ice_control_diagram.png)

<a id="internal_combustion_engine_control_usage"></a>

### 用法 {#internal_combustion_engine_control_usage}

```
internal_combustion_engine_control <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## land_detector

源代码: [modules/land_detector](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/land_detector)

### 描述

检测飞行器自由落体和着陆状态的模块，并发布 `vehicle_land_detected` 主题。
每种飞行器类型（多旋翼、固定翼、vtol、...）都提供自己的算法，考虑各种
状态，如命令推力、解锁状态和飞行器运动。

### 实现

每种类型都在其自己的类中实现，具有共同的基类。基类维护一个状态（着陆、
可能着陆、地面接触）。每个可能的状态都在派生类中实现。一个滞后和每个内部状态的固定
优先级决定了实际的 land_detector 状态。

#### 多旋翼着陆检测器

**ground_contact**：推力设定点和 z 方向速度必须低于定义的阈值时间
GROUND_CONTACT_TRIGGER_TIME_US。当检测到 ground_contact 时，位置控制器关闭身体 x 和 y 中的推力设定点。

**maybe_landed**：它需要 ground_contact 以及更紧的推力设定点阈值和水平方向无速度。
触发时间由 MAYBE_LAND_TRIGGER_TIME 定义。当检测到 maybe_landed 时，
位置控制器将推力设定点设置为零。

**landed**：它需要 maybe_landed 为真时间 LAND_DETECTOR_TRIGGER_TIME_US。

该模块定期在 HP 工作队列上运行。

### 用法 {#land_detector_usage}

```
land_detector <command> [arguments...]
 Commands:
   start         启动后台任务
     fixedwing|multicopter|vtol|rover|airship 选择飞行器类型

   stop

   status        打印状态信息
```

## load_mon

源代码: [modules/load_mon](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/load_mon)

### 描述

在低优先级工作队列上定期运行的后台进程，用于计算 CPU 负载和 RAM
使用情况并发布 `cpuload` 主题。

在 NuttX 上，它还检查每个进程的堆栈使用情况，如果低于 300 字节，则输出警告，
这也将出现在日志文件中。

### 用法 {#load_mon_usage}

```
load_mon <command> [arguments...]
 Commands:
   start         启动后台任务

   stop

   status        打印状态信息
```

## logger

源代码: [modules/logger](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/logger)

### 描述

系统记录器，记录一组可配置的 uORB 主题和系统 printf 消息
（`PX4_WARN` 和 `PX4_ERR`）到 ULog 文件。这些可用于系统和飞行性能评估、
调优、重放和崩溃分析。

它支持 2 个后端：

- 文件：将 ULog 文件写入文件系统（SD 卡）
- MAVLink：通过 MAVLink 将 ULog 数据流式传输到客户端（客户端必须支持此功能）

两个后端都可以启用并同时使用。

文件后端支持 2 种类型的日志文件：完整（正常日志）和任务
日志。任务日志是简化版的 ulog 文件，可用于例如地理标记或
车辆管理。可以通过 SDLOG_MISSION 参数启用和配置。
正常日志始终是任务日志的超集。

### 实现

实现使用两个线程：

- 主线程，以固定速率运行（或在主题上轮询如果以 -p 启动）并检查
  数据更新
- 写入线程，将数据写入文件

中间有一个可配置大小的写入缓冲区（以及另一个固定大小的缓冲区用于
任务日志）。它应该足够大以避免丢包。

### 示例

典型的立即开始记录的用法：

```
logger start -e -t
```

或者如果已经在运行：

```
logger on
```

### 用法 {#logger_usage}

```
logger <command> [arguments...]
 Commands:
   start
     [-m <val>]  后端模式
                 值: file|mavlink|all, 默认: all
     [-x]        通过 Aux1 RC 通道启用/禁用记录
     [-a]        记录第 1 次解锁直到关机
     [-e]        在启动后立即启用记录直到上锁（否则仅在解锁时）
     [-f]        记录直到关机（隐含 -e）
     [-t]        使用日期/时间命名日志目录和文件
     [-r <val>]  记录速率 Hz，0 表示无限制速率
                 默认: 280
     [-b <val>]  记录缓冲区大小 KiB
                 默认: 12
     [-p <val>]  在主题上轮询而不是以固定速率运行（如果设置此选项，则忽略记录速率
                 和主题间隔）
                 值: <topic_name>
     [-c <val>]  记录速率因子（更高更快）
                 默认: 1.0

   on            立即开始记录，覆盖解锁（记录器必须正在运行）

   off           立即停止记录，覆盖解锁（记录器必须正在运行）

   trigger_watchdog 手动触发看门狗

   stop

   status        打印状态信息
```

## mag_bias_estimator

源代码: [modules/mag_bias_estimator](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mag_bias_estimator)

### 描述

在线磁力计偏差估计器。

### 用法 {#mag_bias_estimator_usage}

```
mag_bias_estimator <command> [arguments...]
 Commands:
   start         启动后台任务

   stop

   status        打印状态信息
```

## manual_control

源代码: [modules/manual_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/manual_control)

### 描述

消耗 manual_control_inputs 的模块，发布一个 manual_control_setpoint。

### 用法 {#manual_control_usage}

```
manual_control <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## netman

源代码: [systemcmds/netman](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/netman)

### 描述

网络配置管理器将网络设置保存在非易失性
内存中。在启动时将运行 `update` 选项。如果网络配置
不存在。默认设置将保存在非易失性内存中，
系统将重新启动。

#### update

`netman update` 由 [启动脚本](../concept/system_startup.md#system-startup) 自动运行。
运行时，`update` 选项将检查 SD 卡根目录中是否存在 `net.cfg`。
然后将 `net.cfg` 中的网络设置保存在非易失性内存中，
删除文件并重新启动系统。

#### save

`save` 选项将设置从非易失性内存保存到名为
`net.cfg` 的文件在 SD 卡文件系统上进行编辑。使用此选项编辑设置。
保存不会立即应用网络设置；用户必须重新启动飞行堆栈。
相比之下，`update` 命令由启动脚本运行，将设置提交到非易失性内存，
并重新启动飞行控制器（然后将使用新设置）。

#### show

`show` 选项将在控制台上显示 `net.cfg` 中的网络设置。

### 示例

$ netman save # 将参数保存到 SD 卡。
$ netman show # 显示当前设置。
$ netman update -i eth0 # 执行更新

### 用法 {#netman_usage}

```
netman <command> [arguments...]
 Commands:
   show          在控制台上显示当前持久网络设置。

   update        检查 SD 卡上的 net.cfg 并更新持久网络
                 设置。

   save          将当前网络参数保存到 SD 卡。
     [-i <val>]  设置接口名称
                 默认: eth0
```

## pwm_input

源代码: [drivers/pwm_input](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/pwm_input)

### 描述

通过定时器捕获 ISR 在 AUX5（或 MAIN5）上测量 PWM 输入，并通过 uORB 'pwm_input` 消息发布。

### 用法 {#pwm_input_usage}

```
pwm_input <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## rc_update

源代码: [modules/rc_update](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/rc_update)

### 描述

rc_update 模块处理 RC 通道映射：读取原始输入通道（`input_rc`），
然后应用校准，将 RC 通道映射到配置的通道和模式开关
然后发布为 `rc_channels` 和 `manual_control_input`。

### 实现

为了减少控制延迟，该模块在 input_rc 发布时调度。

### 用法 {#rc_update_usage}

```
rc_update <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## replay

源代码: [modules/replay](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/replay)

### 描述

此模块用于重放 ULog 文件。

使用 2 个环境变量进行配置：`replay`，必须设置为 ULog 文件名 - 它是
要重放的日志文件。第二个是模式，通过 `replay_mode` 指定：

- `replay_mode=ekf2`：特定的 EKF2 重放模式。它只能与 ekf2 模块一起使用，但允许重放
  以尽可能快的速度运行。
- 否则为通用模式：这可用于重放任何模块，但重放将以
  与记录相同的速率进行。

该模块通常与 uORB 发布者规则一起使用，以指定应重放哪些消息。
重放模块将发布在日志中找到的所有消息。它还应用参数从
日志。

重放过程在 [系统范围重放](https://docs.px4.io/main/en/debug/system_wide_replay.html)
页面上有文档。

### 用法 {#replay_usage}

```
replay <command> [arguments...]
 Commands:
   start         开始重放，使用 ENV 变量 'replay' 中的日志文件

   trystart      与 'start' 相同，但如果未给出日志文件则静默退出

   tryapplyparams 尝试应用日志文件中的参数

   stop

   status        打印状态信息
```

## send_event

源代码: [modules/events](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/events)

### 描述

在 LP 工作队列上定期运行的后台进程，执行内务处理任务。
目前仅负责 RC 丢失时的音调警报。

任务可以通过 CLI 或 uORB 主题（来自 MAVLink 的 vehicle_command 等）启动。

### 用法 {#send_event_usage}

```
send_event <command> [arguments...]
 Commands:
   start         启动后台任务

   stop

   status        打印状态信息
```

## sensor_agp_sim

源代码: [modules/simulation/sensor_agp_sim](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/sensor_agp_sim)

### 描述

用于模拟辅助全球位置测量的模块，具有 SIH 仿真的可选故障模式。

### 用法 {#sensor_agp_sim_usage}

```
sensor_agp_sim <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## sensor_arispeed_sim

源代码: [modules/simulation/sensor_airspeed_sim](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/sensor_airspeed_sim)

### 描述

### 用法 {#sensor_arispeed_sim_usage}

```
sensor_arispeed_sim <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## sensor_baro_sim

源代码: [modules/simulation/sensor_baro_sim](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/sensor_baro_sim)

### 描述

### 用法 {#sensor_baro_sim_usage}

```
sensor_baro_sim <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## sensor_gps_sim

源代码: [modules/simulation/sensor_gps_sim](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/sensor_gps_sim)

### 描述

### 用法 {#sensor_gps_sim_usage}

```
sensor_gps_sim <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## sensor_mag_sim

源代码: [modules/simulation/sensor_mag_sim](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/sensor_mag_sim)

### 描述

### 用法 {#sensor_mag_sim_usage}

```
sensor_mag_sim <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## sensors

源代码: [modules/sensors](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/sensors)

### 描述

传感器模块是整个系统的核心。它接受来自驱动程序的低级输出，将其
转换为更可用的形式，并为系统其余部分发布。

提供的功能包括：

- 读取传感器驱动程序的输出（`SensorGyro` 等）。
  如果有多个相同类型，进行投票和故障转移处理。
  然后应用板旋转和温度校准（如果启用）。最后发布数据；其中一个
  主题是 `SensorCombined`，系统许多部分使用。
- 确保传感器驱动程序在参数更改时或
  启动时获得更新的校准参数（比例和偏移）。传感器驱动程序使用 ioctl 接口进行参数更新。为了使其正常工作，
  启动 `sensors` 时传感器驱动程序必须已经在运行。
- 进行传感器一致性检查并发布 `SensorsStatusImu` 主题。

### 实现

它在自己的线程中运行，并轮询当前选择的陀螺仪主题。

### 用法 {#sensors_usage}

```
sensors <command> [arguments...]
 Commands:
   start
     [-h]        在 HIL 模式下启动

   stop

   status        打印状态信息
```

## system_power_simulation

源代码: [modules/simulation/system_power_simulator](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/system_power_simulator)

### 描述

### 用法 {#system_power_simulation_usage}

```
system_power_simulation <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## tattu_can

源代码: [drivers/tattu_can](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/tattu_can)

### 描述

用于从 Tattu 12S 16000mAh 智能电池读取数据的驱动程序。

### 用法 {#tattu_can_usage}

```
tattu_can <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## temperature_compensation

源代码: [modules/temperature_compensation](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/temperature_compensation)

### 描述

温度补偿模块允许系统中的所有陀螺仪、加速度计和气压计进行温度
补偿。该模块监控来自传感器的数据，并在检测到温度变化时更新相关的 sensor_correction 主题。
该模块还可以配置为在下次启动时执行系数计算
例程，这允许在飞行器经历
温度循环时计算热校准系数。

### 用法 {#temperature_compensation_usage}

```
temperature_compensation <command> [arguments...]
 Commands:
   start         启动模块，监控传感器并更新
                 sensor_correction 主题

   calibrate     运行温度校准过程
     [-a]        校准加速度计
     [-g]        校准陀螺仪
     [-m]        校准磁力计
     [-b]        校准气压计（如果未给出这些，则全部校准）

   stop

   status        打印状态信息
```

## time_persistor

源代码: [modules/time_persistor](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/time_persistor)

### 描述

周期性地将 RTC 时间写入文件并在启动时重新加载此值。
这允许在只有软件 RTC（未电池供电）的系统上实现单调时间。
显式向后设置时间（例如通过 system_time）仍然可能。

### 用法 {#time_persistor_usage}

```
time_persistor <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## tune_control

源代码: [systemcmds/tune_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/tune_control)

### 描述

用于控制和测试（外部）曲调的命令行工具。

曲调用于提供可听的通知和警告（例如，当系统解锁、获得位置锁定等时）。
该工具要求运行一个可以处理 tune_control uorb 主题的驱动程序。

有关曲调格式和预定义系统曲调的信息可以在这里找到：
https://github.com/PX4/PX4-Autopilot/blob/main/src/lib/tunes/tune_definition.desc

### 示例

播放系统曲调 #2：

```
tune_control play -t 2
```

### 用法 {#tune_control_usage}

```
tune_control <command> [arguments...]
 Commands:
   play          播放系统曲调或单个音符。
     error       播放错误曲调
     [-t <val>]  播放预定义系统曲调
                 默认: 1
     [-f <val>]  音符频率 Hz (0-22kHz)
     [-d <val>]  音符持续时间 us
     [-s <val>]  音符音量水平（响度）(0-100)
                 默认: 40
     [-m <val>]  字符串形式的旋律
                 值: <string> - 例如 "MFT200e8a8a"

   libtest       测试库

   stop          停止播放（用于重复曲调）
```

## uxrce_dds_client

源代码: [modules/uxrce_dds_client](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/uxrce_dds_client)

### 描述

用于通过串行或 UDP 与代理通信 uORB 主题的 UXRCE-DDS 客户端。

### 示例

```
uxrce_dds_client start -t serial -d /dev/ttyS3 -b 921600
uxrce_dds_client start -t udp -h 127.0.0.1 -p 15555
```

### 用法 {#uxrce_dds_client_usage}

```
uxrce_dds_client <command> [arguments...]
 Commands:
   start
     [-t <val>]  传输协议
                 值: serial|udp, 默认: udp
     [-d <val>]  串行设备
                 值: <file:dev>
     [-b <val>]  波特率（也可以是 p:<param_name>）
                 默认: 0
     [-h <val>]  代理 IP。如果未提供，则默认为 UXRCE_DDS_AG_IP
                 值: <IP>
     [-p <val>]  代理监听端口。如果未提供，则默认为
                 UXRCE_DDS_PRT
     [-n <val>]  客户端 DDS 命名空间

   stop

   status        打印状态信息
```

## work_queue

源代码: [systemcmds/work_queue](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/work_queue)

### 描述

用于显示工作队列状态的命令行工具。

### 用法 {#work_queue_usage}

```
work_queue <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```