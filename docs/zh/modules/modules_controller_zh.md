# 模块参考: 控制器

## airship_att_control

源代码: [modules/airship_att_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/airship_att_control)

### 描述

这实现了飞艇的姿态和速率控制器。理想情况下，它会
将姿态设定点 (`vehicle_attitude_setpoint`) 或速率设定点（在特技模式下
通过 `manual_control_setpoint` 主题）作为输入，并输出执行器控制消息。

目前它直接将 `manual_control_setpoint` 主题馈送到执行器。

### 实现

为了减少控制延迟，模块直接轮询 IMU 驱动程序发布的陀螺仪主题。

### 用法 {#airship_att_control_usage}

```
airship_att_control <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## control_allocator

源代码: [modules/control_allocator](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/control_allocator)

### 描述

这实现了控制分配。它将扭矩和推力设定点
作为输入，并输出执行器设定点消息。

### 用法 {#control_allocator_usage}

```
control_allocator <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## flight_mode_manager

源代码: [modules/flight_mode_manager](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/flight_mode_manager)

### 描述

这实现了所有模式的设定点生成。它将飞行器的当前模式状态作为输入
并输出控制器的设定点。

### 用法 {#flight_mode_manager_usage}

```
flight_mode_manager <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## fw_att_control

源代码: [modules/fw_att_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/fw_att_control)

### 描述

fw_att_control 是固定翼姿态控制器。

### 用法 {#fw_att_control_usage}

```
fw_att_control <command> [arguments...]
 Commands:
   start
     [vtol]      VTOL 模式

   stop

   status        打印状态信息
```

## fw_lat_lon_control

源代码: [modules/fw_lateral_longitudinal_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/fw_lateral_longitudinal_control)

### 描述

fw_lat_lon_control 从横向和纵向控制设定点计算姿态和油门设定点。

### 用法 {#fw_lat_lon_control_usage}

```
fw_lat_lon_control <command> [arguments...]
 Commands:
   start
     [vtol]      VTOL 模式

   stop

   status        打印状态信息
```

## fw_mode_manager

源代码: [modules/fw_mode_manager](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/fw_mode_manager)

### 描述

这实现了所有 PX4 内部固定翼模式、高度率控制及更高层级的设定点生成。
它将飞行器的当前模式状态作为输入，并输出由固定翼
横向-纵向控制器和其下的控制器（姿态、速率）消耗的设定点。

### 用法 {#fw_mode_manager_usage}

```
fw_mode_manager <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## fw_rate_control

源代码: [modules/fw_rate_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/fw_rate_control)

### 描述

fw_rate_control 是固定翼速率控制器。

### 用法 {#fw_rate_control_usage}

```
fw_rate_control <command> [arguments...]
 Commands:
   start
     [vtol]      VTOL 模式

   stop

   status        打印状态信息
```

## mc_att_control

源代码: [modules/mc_att_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mc_att_control)

### 描述

这实现了多旋翼姿态控制器。它将姿态
设定点 (`vehicle_attitude_setpoint`) 作为输入并输出速率设定点。

控制器有一个用于角度误差的 P 环

记录实现的四元数姿态控制的出版物：
非线性四旋翼飞行器姿态控制 (2013)
作者：Dario Brescianini, Markus Hehn 和 Raffaello D'Andrea
动态系统与控制研究所 (IDSC), ETH 苏黎世

https://www.research-collection.ethz.ch/bitstream/handle/20.500.11850/154099/eth-7387-01.pdf

### 用法 {#mc_att_control_usage}

```
mc_att_control <command> [arguments...]
 Commands:
   start
     [vtol]      VTOL 模式

   stop

   status        打印状态信息
```

## mc_nn_control

源代码: [modules/mc_nn_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mc_nn_control)

### 描述

多旋翼神经网络控制模块。
这是一个端到端的多旋翼神经网络控制系统。
它接收 15 个输入值并输出 4 个控制动作。
输入：[pos_err(3), att(6), vel(3), ang_vel(3)]
输出：[执行器电机(4)]

### 用法 {#mc_nn_control_usage}

```
mc_nn_control <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## mc_pos_control

源代码: [modules/mc_pos_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mc_pos_control)

### 描述

控制器有两个环：位置误差的 P 环和速度误差的 PID 环。
速度控制器的输出是推力向量，该向量被分解为推力方向
（即多旋翼方向的旋转矩阵）和推力标量（即多旋翼推力本身）。

控制器不使用欧拉角进行工作，它们仅为了更人性化的控制和
记录而生成。

### 用法 {#mc_pos_control_usage}

```
mc_pos_control <command> [arguments...]
 Commands:
   start
     [vtol]      VTOL 模式

   stop

   status        打印状态信息
```

## mc_rate_control

源代码: [modules/mc_rate_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mc_rate_control)

### 描述

这实现了多旋翼速率控制器。它将速率设定点（在特技模式下
通过 `manual_control_setpoint` 主题）作为输入并输出执行器控制消息。

控制器有一个用于角速率误差的 PID 环。

### 用法 {#mc_rate_control_usage}

```
mc_rate_control <command> [arguments...]
 Commands:
   start
     [vtol]      VTOL 模式

   stop

   status        打印状态信息
```

## navigator

源代码: [modules/navigator](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/navigator)

### 描述

负责自动驾驶模式的模块。这包括任务（从数据管理器读取）、
起飞和返航。
它还负责地理围栏违规检查。

### 实现

不同的内部模式实现为从公共基类 `NavigatorMode` 继承的单独类。
成员 `_navigation_mode` 包含当前活动模式。

导航器发布位置设定点三元组 (`position_setpoint_triplet_s`)，然后由位置
控制器使用。

### 用法 {#navigator_usage}

```
navigator <command> [arguments...]
 Commands:
   start

   fencefile     从 SD 卡加载地理围栏文件，存储在 etc/geofence.txt

   fake_traffic  发布 24 个虚假的 transponder_report_s uORB 消息

   stop

   status        打印状态信息
```

## rover_ackermann

源代码: [modules/rover_ackermann](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/rover_ackermann)

### 描述

漫游车阿克曼模块。

### 用法 {#rover_ackermann_usage}

```
rover_ackermann <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## rover_differential

源代码: [modules/rover_differential](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/rover_differential)

### 描述

漫游车差速模块。

### 用法 {#rover_differential_usage}

```
rover_differential <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## rover_mecanum

源代码: [modules/rover_mecanum](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/rover_mecanum)

### 描述

漫游车麦克纳姆模块。

### 用法 {#rover_mecanum_usage}

```
rover_mecanum <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## spacecraft

源代码: [modules/spacecraft](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/spacecraft)

    ### 描述
    这实现了航天器载具的控制分配。
    它将扭矩和推力设定点作为输入并输出
    执行器设定点消息。

### 用法 {#spacecraft_usage}

```
spacecraft <command> [arguments...]
 Commands:
   start

   status

   stop

   status        打印状态信息
```

## uuv_att_control

源代码: [modules/uuv_att_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/uuv_att_control)

### 描述

控制无人水下航行器 (UUV) 的姿态。

以恒定 250Hz 发布 `vehicle_thrust_setpont` 和 `vehicle_torque_setpoint` 消息。

### 实现

目前，此实现仅支持几种模式：

- 全手动：横滚、俯仰、偏航和油门控制直接传递给执行器
- 自动任务：UUV 执行任务

### 示例

CLI 使用示例：

```
uuv_att_control start
uuv_att_control status
uuv_att_control stop
```

### 用法 {#uuv_att_control_usage}

```
uuv_att_control <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## uuv_pos_control

源代码: [modules/uuv_pos_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/uuv_pos_control)

### 描述

控制无人水下航行器 (UUV) 的姿态。
发布 `attitude_setpoint` 消息。

### 实现

目前，此实现仅支持几种模式：

- 全手动：横滚、俯仰、偏航和油门控制直接传递给执行器
- 自动任务：UUV 执行任务

### 示例

CLI 使用示例：

```
uuv_pos_control start
uuv_pos_control status
uuv_pos_control stop
```

### 用法 {#uuv_pos_control_usage}

```
uuv_pos_control <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## vtol_att_control

源代码: [modules/vtol_att_control](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/vtol_att_control)

### 描述

fw_att_control 是固定翼姿态控制器。

### 用法 {#vtol_att_control_usage}

```
vtol_att_control <command> [arguments...]
 Commands:

   stop

   status        打印状态信息
```