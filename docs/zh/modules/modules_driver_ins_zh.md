# 模块参考: 惯性导航系统 (驱动程序)

## MicroStrain

源代码: [drivers/ins/microstrain](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/ins/microstrain)

### 描述

MicroStrain by HBK 惯性传感器驱动程序。
目前支持以下传感器：

-[CV7-AR](https://www.hbkworld.com/en/products/transducers/inertial-sensors/vertical-reference-units--vru-/3dm-cv7-ar) -[CV7-AHRS](https://www.hbkworld.com/en/products/transducers/inertial-sensors/attitude-and-heading-reference-systems--ahrs-/3dm-cv7-ahrs) -[CV7-INS](https://www.hbkworld.com/en/products/transducers/inertial-sensors/inertial-navigation-systems--ins-/3dm-cv7-ins) -[CV7-GNSS/INS](https://www.hbkworld.com/en/products/transducers/inertial-sensors/inertial-navigation-systems--ins-/3dm-cv7-gnss-ins)

此驱动程序默认不包含在固件中。
通过设置
[kconfig](../hardware/porting_guide_config.md#px4-board-configuration-kconfig) 变量将模块包含在固件中：
`CONFIG_DRIVERS_INS_MICROSTRAIN` 或 `CONFIG_COMMON_INS`。

### 示例

尝试在指定的串行设备上启动驱动程序。
如果未指定端口，驱动程序将默认选择 /dev/ttyS4

```
microstrain start -d /dev/ttyS1
```

停止驱动程序

```
microstrain stop
```

### 用法 {#MicroStrain_usage}

```
MicroStrain <command> [arguments...]
 Commands:
   start         启动驱动程序
     [-d <val>]  端口
                 值: <file:dev>, 默认: /dev/ttyS4

   stop          停止驱动程序

   status        驱动程序状态
```

## ilabs

源代码: [drivers/ins/ilabs](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/ins/ilabs)

### 描述

ILabs 传感器的串行总线驱动程序。

大多数板子都配置为使用 SENS_ILABS_CFG 在指定的 UART 上启用/启动驱动程序。
之后您可以使用 ILABS_MODE 参数配置输出：

- 仅原始传感器输出（默认）。
- 传感器输出和 INS 数据，如位置和速度估计。

设置/使用信息: https://docs.px4.io/main/en/sensor/inertiallabs.html

### 示例

尝试在指定的串行设备上启动驱动程序。

```
ilabs start -d /dev/ttyS1
```

停止驱动程序

```
ilabs stop
```

### 用法 {#ilabs_usage}

```
ilabs <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备

   status        驱动程序状态

   stop          停止驱动程序

   status        打印驱动程序状态
```

## vectornav

源代码: [drivers/ins/vectornav](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/ins/vectornav)

### 描述

VectorNav VN-100, VN-200, VN-300 的串行总线驱动程序。

大多数板子都配置为使用 SENS_VN_CFG 参数在指定的 UART 上启用/启动驱动程序。

设置/使用信息: https://docs.px4.io/main/en/sensor/vectornav.html

### 示例

尝试在指定的串行设备上启动驱动程序。

```
vectornav start -d /dev/ttyS1
```

停止驱动程序

```
vectornav stop
```

### 用法 {#vectornav_usage}

```
vectornav <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备

   status        驱动程序状态

   stop          停止驱动程序

   status        打印驱动程序状态
```