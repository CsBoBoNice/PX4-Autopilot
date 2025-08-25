# 模块参考: 命令



## actuator_test

源代码: [systemcmds/actuator_test](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/actuator_test)


测试执行器的实用程序。

警告：使用此命令前请移除所有螺旋桨。

### 用法 {#actuator_test_usage}

```
actuator_test <command> [arguments...]
 Commands:
   set           将执行器设置为特定输出值

 执行器可以通过电机、舵机或功能直接指定：
     [-m <val>]  要测试的电机 (1...8)
     [-s <val>]  要测试的舵机 (1...8)
     [-f <val>]  直接指定功能
     -v <val>    值 (-1...1)
     [-t <val>]  超时秒数（如果未设置则交互式运行）
                 默认: 0

   iterate-motors 迭代所有电机，依次启动和停止

   iterate-servos 迭代所有舵机，依次偏转
```

## bl_update

源代码: [systemcmds/bl_update](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/bl_update)

从文件刷写引导程序的实用程序
### 用法 {#bl_update_usage}

```
bl_update [arguments...]
   setopt        设置选项位以解锁 FLASH（仅在锁定状态下需要）

   <file>        引导程序 bin 文件
```

## bsondump

源代码: [systemcmds/bsondump](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/bsondump)

读取 BSON 文件并打印或输出文档大小的实用程序。
### 用法 {#bsondump_usage}

```
bsondump [arguments...]
     <file>      要解码和打印的 BSON 文件。
```

## dumpfile

源代码: [systemcmds/dumpfile](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/dumpfile)

转储文件实用程序。以二进制模式（不将 LF 替换为 CR LF）将文件大小和内容打印到标准输出。
### 用法 {#dumpfile_usage}

```
dumpfile [arguments...]
     <file>      要转储的文件
```

## dyn

源代码: [systemcmds/dyn](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/dyn)


### 描述
加载并运行未编译到 PX4 二进制文件中的动态 PX4 模块。

### 示例
```
dyn ./hello.px4mod start
```


### 用法 {#dyn_usage}

```
dyn [arguments...]
     <file>      包含模块的文件
     [arguments...] 模块的参数
```

## failure

源代码: [systemcmds/failure](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/failure)


### 描述
向系统注入故障。

### 实现
此系统命令通过 uORB 发送车辆命令以触发故障。

### 示例
通过停止 GPS 测试 GPS 故障保护：

failure gps off

### 用法 {#failure_usage}

```
failure [arguments...]
   help          显示此帮助文本

   gps|...       指定组件

   ok|off|...    指定故障类型
     [-i <val>]  传感器实例 (0=全部)
                 默认: 0
```

## gpio

源代码: [systemcmds/gpio](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/gpio)


### 描述
此命令用于读取和写入 GPIO
```
gpio read <PORT><PIN>/<DEVICE> [PULLDOWN|PULLUP] [--force]
gpio write <PORT><PIN>/<DEVICE> <VALUE> [PUSHPULL|OPENDRAIN] [--force]
```

### 示例
读取端口 H 引脚 4 上配置为上拉的值，并且为高电平
```
gpio read H4 PULLUP
```
1 OK

将端口 E 引脚 7 的输出值设置为高电平
```
gpio write E7 1 --force
```

将设备 /dev/gpio1 的输出值设置为高电平
```
gpio write /dev/gpio1 1
```


### 用法 {#gpio_usage}

```
gpio [arguments...]
   read
     <PORT><PIN>/<DEVICE> GPIO 端口和引脚或设备
     [PULLDOWN|PULLUP] 下拉/上拉
     [--force]   强制（忽略板载 gpio 列表）

   write
     <PORT> <PIN> GPIO 端口和引脚
     <VALUE>     要写入的值
     [PUSHPULL|OPENDRAIN] 推挽/开漏
     [--force]   强制（忽略板载 gpio 列表）
```

## hardfault_log

源代码: [systemcmds/hardfault_log](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/hardfault_log)

硬故障实用程序

在启动脚本中用于处理硬故障

### 用法 {#hardfault_log_usage}

```
hardfault_log <command> [arguments...]
 Commands:
   check         检查是否有未提交的硬故障

   rearm         丢弃未提交的硬故障

   fault         生成硬故障（此命令会使系统崩溃 :)
     [0|1|2|3]   硬故障类型: 0=除以 0, 1=断言, 2=跳转到 0x0,
                 3=写入 0x0 (默认=0)

   commit        将未提交的硬故障写入 /fs/microsd/fault_%i.txt（并重新武装，但不重置）

   count         读取重启计数器，计算未提交硬故障的重启次数（作为程序的退出代码返回）

   reset         重置重启计数器
```

## hist

源代码: [systemcmds/hist](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/hist)

命令行工具，用于显示 px4 消息历史。没有参数。
### 用法 {#hist_usage}

```
hist [arguments...]
```

## i2cdetect

源代码: [systemcmds/i2cdetect](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/i2cdetect)

扫描特定总线上 I2C 设备的实用程序。
### 用法 {#i2cdetect_usage}

```
i2cdetect [arguments...]
     [-b <val>]  I2C 总线
                 默认: 1
```

## led_control

源代码: [systemcmds/led_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/led_control)


### 描述
用于控制和测试（外部）LED 的命令行工具。

要使用它，请确保有一个驱动程序正在运行，该驱动程序处理 led_control uorb 主题。

有不同的优先级，例如一个模块可以以低优先级设置颜色，另一个模块可以以高优先级闪烁 N 次，LED 会在闪烁后自动返回到较低优先级状态。`reset` 命令也可用于返回到较低优先级。

### 示例
使第一个 LED 蓝色闪烁 5 次：
```
led_control blink -c blue -l 0 -n 5
```


### 用法 {#led_control_usage}

```
led_control <command> [arguments...]
 Commands:
   test          运行测试模式

   on            打开 LED

   off           关闭 LED

   reset         重置 LED 优先级

   blink         闪烁 LED N 次
     [-n <val>]  闪烁次数
                 默认: 3
     [-s <val>]  设置闪烁速度
                 值: fast|normal|slow, 默认: normal

   breathe       连续淡入淡出 LED

   flash         两次快速闪烁然后以 1Hz 频率关闭

 以下参数适用于除 'test' 之外的所有上述命令：
     [-c <val>]  颜色
                 值: red|blue|green|yellow|purple|amber|cyan|white, 默认:
                 white
     [-l <val>]  控制哪个 LED: 0, 1, 2, ... (默认=全部)
     [-p <val>]  优先级
                 默认: 2
```

## listener

源代码: [systemcmds/topic_listener](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/topic_listener)


监听 uORB 主题并将数据打印到控制台的实用程序。

随时可以通过按 Ctrl+C、Esc 或 Q 退出监听器。

### 用法 {#listener_usage}

```
listener <command> [arguments...]
 Commands:
     <topic_name> uORB 主题名称
     [-i <val>]  主题实例
                 默认: 0
     [-n <val>]  消息数量
                 默认: 1
     [-r <val>]  订阅速率（如果为 0 则无限制）
                 默认: 0
```

## mfd

源代码: [systemcmds/mft](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/mft)

与清单交互的实用程序
### 用法 {#mfd_usage}

```
mfd <command> [arguments...]
 Commands:
   query         如果不存在则返回 true
```

## mft_cfg

源代码: [systemcmds/mft_cfg](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/mft_cfg)

设置和获取清单配置的工具
### 用法 {#mft_cfg_usage}

```
mft_cfg <command> [arguments...]
 Commands:
   get           获取清单配置

   set           设置清单配置

   reset         重置清单配置
     hwver|hwrev 选择类型: MTD_MTF_VER|MTD_MTF_REV
     -i <val>    设置扩展硬件 ID 的参数（id == 版本对于 <hwver>，id == 修订对于 <hwrev> ）
```

## mtd

源代码: [systemcmds/mtd](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/mtd)

挂载和测试分区的实用程序（基于板子定义的 FRAM/EEPROM 存储）
### 用法 {#mtd_usage}

```
mtd <command> [arguments...]
 Commands:
   status        打印状态信息

   readtest      执行读取测试

   rwtest        执行读写测试

   erase         擦除分区

 'readtest' 和 'rwtest' 命令有一个可选的实例索引：
     [-i <val>]  存储索引（如果板子有多个存储）
                 默认: 0

 'readtest'、'rwtest' 和 'erase' 命令有一个可选参数：
     [<partition_name1> [<partition_name2> ...]] 分区名称（例如
                 /fs/mtd_params），如果未提供则使用系统默认
```

## nshterm

源代码: [systemcmds/nshterm](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/nshterm)

在给定端口上启动 NSH shell。

这以前用于在 USB 串口上启动 shell。
现在运行 mavlink，并且可以通过 mavlink 使用 shell。

### 用法 {#nshterm_usage}

```
nshterm [arguments...]
     <file:dev>  启动 shell 的设备（例如 /dev/ttyACM0）
```

## param

源代码: [systemcmds/param](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/param)


### 描述
通过 shell 或脚本访问和操作参数的命令。

例如，这在启动脚本中用于设置特定于机型的参数。

参数在更改时会自动保存，例如使用 `param set`。它们通常存储到 FRAM 或 SD 卡中。`param select` 可用于更改后续保存的存储位置（这需要在每次启动时重新配置）。

如果启用了基于 FLASH 的后端（这是在编译时完成的，例如对于 Intel Aero 或 Omnibus），`param select` 没有效果，默认值始终是 FLASH 后端。但是 `param save/load <file>` 仍然可以用于写入/读取文件。

每个参数都有一个 'used' 标志，它在启动时读取参数时设置。它用于只向地面控制站显示相关参数。

### 示例
更改机型并确保加载该机型的默认参数：
```
param set SYS_AUTOSTART 4001
param set SYS_AUTOCONFIG 1
reboot
```

### 用法 {#param_usage}

```
param <command> [arguments...]
 Commands:
   load          从文件加载参数（覆盖所有）
     [<file>]    文件名（如果未提供则使用默认）

   import        从文件导入参数
     [<file>]    文件名（如果未提供则使用默认）

   save          将参数保存到文件
     [<file>]    文件名（如果未提供则使用默认）

   select        选择默认文件
     [<file>]    文件名

   select-backup 选择默认文件
     [<file>]    文件名

   show          显示参数值
     [-a]        显示所有参数（不仅仅是已使用的）
     [-c]        仅显示已更改的参数（包括未使用的）
     [-q]        静默模式，仅打印参数值（名称需要完全匹配）
     [<filter>]  按参数名称过滤（末尾允许通配符，例如 sys_*）

   show-for-airframe 显示机型配置的已更改参数

   status        打印参数系统状态

   set           将参数设置为值
     <param_name> <value> 参数名称和要设置的值
     [fail]      如果提供，当找不到参数时让命令失败

   set-default   将参数默认值设置为值
     [-s]        如果提供，在参数不存在时静默错误
     <param_name> <value> 参数名称和要设置的值
     [fail]      如果提供，当找不到参数时让命令失败

   compare       将参数与值进行比较。如果相等则命令成功
     [-s]        如果提供，在参数不存在时静默错误
     <param_name> <value> 参数名称和要比较的值

   greater       将参数与值进行比较。如果参数大于值则命令成功
     [-s]        如果提供，在参数不存在时静默错误
     <param_name> <value> 参数名称和要比较的值
     <param_name> <value> 参数名称和要比较的值

   touch         将参数标记为已使用
     [<param_name1> [<param_name2>]] 参数名称（一个或多个）

   reset         仅将指定参数重置为默认值
     [<param1> [<param2>]] 要重置的参数名称（末尾允许通配符）

   reset_all     将所有参数重置为默认值
     [<exclude1> [<exclude2>]] 不重置匹配的参数（末尾允许通配符）

   index         显示给定索引的参数
     <index>     索引: 一个 >= 0 的整数

   index_used    显示给定索引的已使用参数
     <index>     索引: 一个 >= 0 的整数

   find          显示参数的索引
     <param>     参数名称
```

## payload_deliverer

源代码: [modules/payload_deliverer](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/payload_deliverer)


### 描述
处理有效载荷投放，使用夹爪或绞盘并设置适当的超时/反馈传感器，
并在内部将投放结果作为确认信息进行通信


### 用法 {#payload_deliverer_usage}

```
payload_deliverer <command> [arguments...]
 Commands:
   start

   gripper_test  测试夹爪的释放和抓取序列

   gripper_open  打开夹爪

   gripper_close 关闭夹爪

   stop

   status        打印状态信息
```

## perf

源代码: [systemcmds/perf](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/perf)

打印性能计数器的工具
### 用法 {#perf_usage}

```
perf [arguments...]
   reset         重置所有计数器

   latency       打印 HRT 定时器延迟直方图

 如果没有参数则打印所有性能计数器
```

## reboot

源代码: [systemcmds/reboot](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/reboot)

重启系统
### 用法 {#reboot_usage}

```
reboot [arguments...]
     [-b]        重启到引导程序
     [-i]        重启到 ISP（第一阶段引导程序）
     [lock|unlock] 获取/释放关机锁（用于测试）
```

## sd_bench

源代码: [systemcmds/sd_bench](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/sd_bench)

测试 SD 卡的速度
### 用法 {#sd_bench_usage}

```
sd_bench [arguments...]
     [-b <val>]  每次读/写的块大小
                 默认: 4096
     [-r <val>]  运行次数
                 默认: 5
     [-d <val>]  每次运行的持续时间（毫秒）
                 默认: 2000
     [-k]        保留测试文件
     [-s]        每个块后调用 fsync（默认=每次运行结束时）
     [-u]        使用未对齐的数据测试性能
     [-U]        使用强制字节未对齐的数据测试性能
     [-v]        验证数据和块号
```

## sd_stress

源代码: [systemcmds/sd_stress](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/sd_stress)

测试 SD 卡上的操作
### 用法 {#sd_stress_usage}

```
sd_stress [arguments...]
     [-r <val>]  运行次数
                 默认: 5
     [-b <val>]  字节数
                 默认: 100
```

## serial_passthru

源代码: [systemcmds/serial_passthru](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/serial_passthru)

将数据从一个设备传递到另一个设备。

这可以用于将连接到 USB 的 u-center 与串口上的 GPS 一起使用。

### 用法 {#serial_passthru_usage}

```
serial_passthru [arguments...]
     -e <val>    外部设备路径
                 值: <file:dev>
     -d <val>    内部设备路径
                 值: <file:dev>
     [-b <val>]  波特率
                 默认: 115200
     [-t]        在内部设备上跟踪外部设备的波特率
```

## system_time

源代码: [systemcmds/system_time](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/system_time)


### 描述

设置和获取系统时间的命令行工具。

### 示例

设置系统时间并读回
```
system_time set 1600775044
system_time get
```

### 用法 {#system_time_usage}

```
system_time <command> [arguments...]
 Commands:
   set           设置系统时间，提供 unix 纪元时间格式的时间

   get           获取系统时间
```

## top

源代码: [systemcmds/top](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/top)

监控正在运行的进程及其 CPU、堆栈使用情况、优先级和状态
### 用法 {#top_usage}

```
top [arguments...]
   once          仅打印一次负载
```

## usb_connected

源代码: [systemcmds/usb_connected](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/usb_connected)

检查 USB 是否连接的实用程序。以前在启动脚本中使用。
返回值 0 表示 USB 已连接，1 表示未连接。
### 用法 {#usb_connected_usage}

```
usb_connected [arguments...]
```

## ver

源代码: [systemcmds/ver](https://github.com/PX4/PX4-Autopilot/tree/main/src/systemcmds/ver)

打印各种版本信息的工具
### 用法 {#ver_usage}

```
ver <command> [arguments...]
 Commands:
   hw            硬件架构

   mcu           MCU 信息

   git           git 版本信息

   bdate         构建日期和时间

   gcc           编译器信息

   bdate         构建日期和时间

   px4guid       PX4 GUID

   uri           构建 URI

   all           打印所有版本

   hwcmp         比较硬件版本（匹配时返回 0）
     <hw> [<hw2>] 要比较的硬件（例如 PX4_FMU_V4）。如果指定了多个，则使用 OR 比较

   hwtypecmp     比较硬件类型（匹配时返回 0）
     <hwtype> [<hwtype2>] 要比较的硬件类型（例如 V2）。如果指定了多个，则使用 OR 比较

   hwbasecmp     比较硬件基础（匹配时返回 0）
     <hwbase> [<hwbase2>] 要比较的硬件类型（例如 V2）。如果指定了多个，则使用 OR 比较
```