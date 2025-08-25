# 模块参考: 距离传感器 (驱动程序)

## afbrs50

源代码: [drivers/distance_sensor/broadcom/afbrs50](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/broadcom/afbrs50)

### 描述

Broadcom AFBRS50 驱动程序。

### 示例

尝试在指定的串行设备上启动驱动程序。

```
afbrs50 start
```

停止驱动程序

```
afbrs50 stop
```

### 用法 {#afbrs50_usage}

```
afbrs50 <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备
     [-r <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop          停止驱动程序
```

## gy_us42

源代码: [drivers/distance_sensor/gy_us42](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/gy_us42)

### 用法 {#gy_us42_usage}

```
gy_us42 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop

   status        打印状态信息
```

## leddar_one

源代码: [drivers/distance_sensor/leddar_one](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/leddar_one)

### 描述

LeddarOne LiDAR 的串行总线驱动程序。

大多数板子都配置为使用 SENS_LEDDAR1_CFG 参数在指定的 UART 上启用/启动驱动程序。

设置/使用信息: https://docs.px4.io/main/en/sensor/leddar_one.html

### 示例

尝试在指定的串行设备上启动驱动程序。

```
leddar_one start -d /dev/ttyS1
```

停止驱动程序

```
leddar_one stop
```

### 用法 {#leddar_one_usage}

```
leddar_one <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备
     [-r <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop          停止驱动程序
```

## lightware_laser_i2c

源代码: [drivers/distance_sensor/lightware_laser_i2c](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/lightware_laser_i2c)

### 描述

Lightware SFxx 系列 LIDAR 测距仪的 I2C 总线驱动程序: SF10/a, SF10/b, SF10/c, SF11/c, SF/LW20。

设置/使用信息: https://docs.px4.io/main/en/sensor/sfxx_lidar.html

### 用法 {#lightware_laser_i2c_usage}

```
lightware_laser_i2c <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 102
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop

   status        打印状态信息
```

## lightware_laser_serial

源代码: [drivers/distance_sensor/lightware_laser_serial](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/lightware_laser_serial)

### 描述

LightWare SF02/F, SF10/a, SF10/b, SF10/c, SF11/c 激光测距仪的串行总线驱动程序。

大多数板子都配置为使用 SENS_SF0X_CFG 参数在指定的 UART 上启用/启动驱动程序。

设置/使用信息: https://docs.px4.io/main/en/sensor/sfxx_lidar.html

### 示例

尝试在指定的串行设备上启动驱动程序。

```
lightware_laser_serial start -d /dev/ttyS1
```

停止驱动程序

```
lightware_laser_serial stop
```

### 用法 {#lightware_laser_serial_usage}

```
lightware_laser_serial <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop          停止驱动程序
```

## lightware_sf45_serial

源代码: [drivers/distance_sensor/lightware_sf45_serial](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/lightware_sf45_serial)

### 描述

Lightware SF45/b 激光测距仪的串行总线驱动程序。

### 示例

尝试在指定的串行设备上启动驱动程序。

```
lightware_sf45_serial start -d /dev/ttyS1
```

停止驱动程序

```
lightware_sf45_serial stop
```

### 用法 {#lightware_sf45_serial_usage}

```
lightware_sf45_serial <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备

   stop          停止驱动程序
```

## ll40ls

源代码: [drivers/distance_sensor/ll40ls](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/ll40ls)

### 描述

LidarLite 测距仪的 I2C 总线驱动程序。

传感器/驱动程序必须使用参数 SENS_EN_LL40LS 启用。

设置/使用信息: https://docs.px4.io/main/en/sensor/lidar_lite.html

### 用法 {#ll40ls_usage}

```
ll40ls <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 98
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   regdump

   stop

   status        打印状态信息
```

## ll40ls_pwm

源代码: [drivers/distance_sensor/ll40ls_pwm](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/ll40ls_pwm)

### 描述

LidarLite 测距仪的 PWM 驱动程序。

传感器/驱动程序必须使用参数 SENS_EN_LL40LS 启用。

设置/使用信息: https://docs.px4.io/main/en/sensor/lidar_lite.html

### 用法 {#ll40ls_pwm_usage}

```
ll40ls_pwm <command> [arguments...]
 Commands:
   start         启动驱动程序
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   status        打印驱动程序状态信息

   stop          停止驱动程序
```

## mappydot

源代码: [drivers/distance_sensor/mappydot](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/mappydot)

### 用法 {#mappydot_usage}

```
mappydot <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)

   stop

   status        打印状态信息
```

## mb12xx

源代码: [drivers/distance_sensor/mb12xx](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/mb12xx)

### 用法 {#mb12xx_usage}

```
mb12xx <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)

   set_address
     [-a <val>]  I2C 地址
                 默认: 112

   stop

   status        打印状态信息
```

## pga460

源代码: [drivers/distance_sensor/pga460](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/pga460)

### 描述

超声波测距仪驱动程序，处理与设备的通信并通过 uORB 发布距离。

### 实现

此驱动程序作为 NuttX 任务实现。选择此实现是因为需要通过 UART 轮询消息，而 work_queue 不支持此功能。此驱动程序在运行时持续进行距离测量。在驱动程序级别实现了一个简单的算法来检测错误读数，以尝试提高发布数据的质量。如果驱动程序认为传感器数据无效或不稳定，则根本不会发布数据。

### 用法 {#pga460_usage}

```
pga460 <command> [arguments...]
 Commands:
   start
     [device_path] pga460 传感器设备路径, (例如: /dev/ttyS6)

   status

   stop

   help
```

## srf02

源代码: [drivers/distance_sensor/srf02](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/srf02)

### 用法 {#srf02_usage}

```
srf02 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 112
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop

   status        打印状态信息
```

## srf05

源代码: [drivers/distance_sensor/srf05](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/srf05)

### 描述

HY-SRF05 / HC-SR05 和 HC-SR04 测距仪的驱动程序。

传感器/驱动程序必须使用参数 SENS_EN_HXSRX0X 启用。

### 用法 {#srf05_usage}

```
srf05 <command> [arguments...]
 Commands:
   start         启动驱动程序
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   status        打印驱动程序状态信息

   stop          停止驱动程序

   stop

   status        打印状态信息
```

## teraranger

源代码: [drivers/distance_sensor/teraranger](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/teraranger)

### 描述

TeraRanger 测距仪的 I2C 总线驱动程序。

传感器/驱动程序必须使用参数 SENS_EN_TRANGER 启用。

设置/使用信息: https://docs.px4.io/main/en/sensor/rangefinders.html#teraranger-rangefinders

### 用法 {#teraranger_usage}

```
teraranger <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 48
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop

   status        打印状态信息
```

## tf02pro

源代码: [drivers/distance_sensor/tf02pro](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/tf02pro)

### 用法 {#tf02pro_usage}

```
tf02pro <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 16
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop

   status        打印状态信息
```

## tfmini

源代码: [drivers/distance_sensor/tfmini](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/tfmini)

### 描述

Benewake TFmini LiDAR 的串行总线驱动程序。

大多数板子都配置为使用 SENS_TFMINI_CFG 参数在指定的 UART 上启用/启动驱动程序。

设置/使用信息: https://docs.px4.io/main/en/sensor/tfmini.html

### 示例

尝试在指定的串行设备上启动驱动程序。

```
tfmini start -d /dev/ttyS1
```

停止驱动程序

```
tfmini stop
```

### 用法 {#tfmini_usage}

```
tfmini <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   status        驱动程序状态

   stop          停止驱动程序

   status        打印驱动程序状态
```

## ulanding_radar

源代码: [drivers/distance_sensor/ulanding_radar](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/ulanding_radar)

### 描述

Aerotenna uLanding 雷达的串行总线驱动程序。

设置/使用信息: https://docs.px4.io/main/en/sensor/ulanding_radar.html

### 示例

尝试在指定的串行设备上启动驱动程序。

```
ulanding_radar start -d /dev/ttyS1
```

停止驱动程序

```
ulanding_radar stop
```

### 用法 {#ulanding_radar_usage}

```
ulanding_radar <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备
                 值: <file:dev>, 默认: /dev/ttyS3
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop          停止驱动程序
```

## vl53l0x

源代码: [drivers/distance_sensor/vl53l0x](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/vl53l0x)

### 用法 {#vl53l0x_usage}

```
vl53l0x <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 41
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop

   status        打印状态信息
```

## vl53l1x

源代码: [drivers/distance_sensor/vl53l1x](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/distance_sensor/vl53l1x)

### 用法 {#vl53l1x_usage}

```
vl53l1x <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 41
     [-R <val>]  传感器旋转 - 默认向下
                 默认: 25

   stop

   status        打印状态信息
```