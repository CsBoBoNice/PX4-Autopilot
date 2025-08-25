# 模块参考: 通信

## frsky_telemetry

源代码: [drivers/telemetry/frsky_telemetry](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/telemetry/frsky_telemetry)

FrSky 遥测支持。自动检测 D 或 S.PORT 协议。

### 用法 {#frsky_telemetry_usage}

```
frsky_telemetry <command> [arguments...]
 Commands:
   start
     [-d <val>]  选择串行设备
                 值: <file:dev>, 默认: /dev/ttyS6
     [-t <val>]  扫描超时 [s] (默认: 无超时)
                 默认: 0
     [-m <val>]  选择协议 (默认: 自动检测)
                 值: sport|sport_single|sport_single_invert|dtype, 默认:
                 auto

   stop

   status
```

## mavlink

源代码: [modules/mavlink](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mavlink)

### 描述

此模块实现了 MAVLink 协议，可在串行链路或 UDP 网络连接上使用。
它通过 uORB 与系统通信：一些消息在模块中直接处理（例如任务协议），其他消息通过 uORB 发布（例如 vehicle_command）。

流用于以特定速率发送周期性消息，例如飞行器姿态。
启动 mavlink 实例时，可以指定一种模式，该模式定义了启用的流集及其速率。
对于正在运行的实例，可以通过 `mavlink stream` 命令配置流。

模块可以有多个独立实例，每个实例连接到一个串行设备或网络端口。

### 实现

实现使用 2 个线程，一个发送线程和一个接收线程。发送器以固定速率运行，如果组合带宽高于配置的速率 (`-r`) 或物理链路饱和，则动态降低流的速率。这可以通过 `mavlink status` 检查，查看 `rate mult` 是否小于 1。

**注意**：一些数据从两个线程访问和修改，因此在更改代码或扩展功能时，需要考虑这一点，以避免竞争条件和数据损坏。

### 示例

在 ttyS1 串行端口上启动 mavlink，波特率为 921600，最大发送速率为 80kB/s：

```
mavlink start -d /dev/ttyS1 -b 921600 -m onboard -r 80000
```

在 UDP 端口 14556 上启动 mavlink 并启用 HIGHRES_IMU 消息，频率为 50Hz：

```
mavlink start -u 14556 -r 1000000
mavlink stream -u 14556 -s HIGHRES_IMU -r 50
```

### 用法 {#mavlink_usage}

```
mavlink <command> [arguments...]
 Commands:
   start         启动新实例
     [-d <val>]  选择串行设备
                 值: <file:dev>, 默认: /dev/ttyS1
     [-b <val>]  波特率 (也可以是 p:<param_name>)
                 默认: 57600
     [-r <val>]  最大发送数据速率 B/s (如果为 0，则使用波特率 / 20)
                 默认: 0
     [-p]        启用广播
     [-u <val>]  选择 UDP 网络端口 (本地)
                 默认: 14556
     [-o <val>]  选择 UDP 网络端口 (远程)
                 默认: 14550
     [-t <val>]  合作伙伴 IP (可以通过 -p 标志启用广播)
                 默认: 127.0.0.1
     [-m <val>]  模式: 设置默认流和速率
                 值: custom|camera|onboard|osd|magic|config|iridium|minimal|
                 extvision|extvisionmin|gimbal|onboard_low_bandwidth|uavionix|lo
                 w_bandwidth|distance_sensor, 默认: normal
     [-n <val>]  wifi/以太网接口名称
                 值: <interface_name>
     [-c <val>]  组播地址 (可以通过 MAV_{i}_BROADCAST 参数启用组播)
                 值: 组播地址范围
                 [239.0.0.0,239.255.255.255]
     [-F <val>]  设置铱星模式的传输频率
                 默认: 0.0
     [-f]        启用消息转发到其他 Mavlink 实例
     [-w]        等待发送，直到收到第一条消息
     [-x]        启用 FTP
     [-z]        强制硬件流控制始终开启
     [-Z]        强制硬件流控制始终关闭

   stop-all      停止所有实例

   stop          停止正在运行的实例
     [-u <val>]  通过本地网络端口选择 Mavlink 实例
     [-d <val>]  通过串行设备选择 Mavlink 实例
                 值: <file:dev>

   status        打印所有实例的状态
     [streams]   打印所有启用的流

   stream        配置正在运行实例的流发送速率
     [-u <val>]  通过本地网络端口选择 Mavlink 实例
     [-d <val>]  通过串行设备选择 Mavlink 实例
                 值: <file:dev>
     -s <val>    要配置的 Mavlink 流
     -r <val>    频率 Hz (0 = 关闭, -1 = 设置为默认)

   boot_complete 启用消息发送。(必须)作为启动脚本的最后一步调用。
```

## uorb

源代码: [systemcmds/uorb](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/uorb)

### 描述

uORB 是内部的发布-订阅消息系统，用于模块间通信。

### 实现

实现是异步且无锁的，即发布者不等待订阅者，反之亦然。
这是通过在发布者和订阅者之间设置单独的缓冲区来实现的。

代码经过优化，以最小化内存占用和交换消息的延迟。

消息在 `/msg` 目录中定义。它们在构建时转换为 C/C++ 代码。

如果使用 ORB_USE_PUBLISHER_RULES 编译，可以使用带有 uORB 发布规则的文件来配置哪些模块被允许发布哪些主题。这用于系统范围的重放。

### 示例

监控主题发布速率。除了 `top`，这是系统检查的重要命令：

```
uorb top
```

### 用法 {#uorb_usage}

```
uorb <command> [arguments...]
 Commands:
   status        打印主题统计信息

   top           监控主题发布速率
     [-a]        打印所有主题而不是仅打印当前有订阅者的发布主题
     [-1]        只运行一次，然后退出
     [<filter1> [<filter2>]] 要匹配的主题 (隐含 -a)
```