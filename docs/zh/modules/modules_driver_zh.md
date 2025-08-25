# 模块参考: 驱动程序

子类别:

- [空速传感器](modules_driver_airspeed_sensor.md)
- [气压计](modules_driver_baro.md)
- [相机](modules_driver_camera.md)
- [距离传感器](modules_driver_distance_sensor.md)
- [惯性测量单元](modules_driver_imu.md)
- [惯性导航系统](modules_driver_ins.md)
- [磁力计](modules_driver_magnetometer.md)
- [光流](modules_driver_optical_flow.md)
- [无线电控制](modules_driver_radio_control.md)
- [转速传感器](modules_driver_rpm_sensor.md)
- [应答器](modules_driver_transponder.md)

## MCP23009

源代码: [drivers/gpio/mcp23009](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/gpio/mcp23009)

### 用法 {#MCP23009_usage}

```
MCP23009 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 37
     [-D <val>]  方向
                 默认: 0
     [-O <val>]  输出
                 默认: 0
     [-P <val>]  上拉电阻
                 默认: 0
     [-U <val>]  更新间隔 [ms]
                 默认: 0

   stop

   status        打印状态信息
```

## adc

源代码: [drivers/adc/board_adc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/adc/board_adc)

### 描述

ADC 驱动程序。

### 用法 {#adc_usage}

```
adc <command> [arguments...]
 Commands:
   start

   test
     [-n]        不发布 ADC 报告，仅系统电源

   stop

   status        打印状态信息
```

## ads1115

源代码: [drivers/adc/ads1115](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/adc/ads1115)

### 描述

驱动程序用于通过 I2C 连接的外部 [ADS1115](https://www.adafruit.com/product/1085) ADC。

对于没有内部模数转换器的板子，如 [PilotPi](../flight_controller/raspberry_pi_pilotpi.md) 或 [CUAV Nora](../flight_controller/cuav_nora.md)，该驱动程序默认包含在固件中
(在板配置文件中搜索 `CONFIG_DRIVERS_ADC_ADS1115`)。

它使用 [ADC_ADS1115_EN](../advanced_config/parameter_reference.md#ADC_ADS1115_EN) 参数启用/禁用，默认情况下是禁用的。
如果启用，内部 ADC 将不被使用。

### 用法 {#ads1115_usage}

```
ads1115 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 72

   stop

   status        打印状态信息
```

## atxxxx

源代码: [drivers/osd/atxxxx](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/osd/atxxxx)

### 描述

用于安装在 OmnibusF4SD 板上的 ATXXXX 芯片的 OSD 驱动程序。

可以使用 OSD_ATXXXX_CFG 参数启用。

### 用法 {#atxxxx_usage}

```
atxxxx <command> [arguments...]
 Commands:
   start
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)

   stop

   status        打印状态信息
```

## batmon

源代码: [drivers/smart_battery/batmon](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/smart_battery/batmon)

### 描述

用于与启用 BatMon 的智能电池进行 SMBUS 通信的驱动程序
设置/使用信息: https://rotoye.com/batmon-tutorial/

### 示例

要在地址 0x0B，总线 4 上启动

```
batmon start -X -a 11 -b 4
```

### 用法 {#batmon_usage}

```
batmon <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 11

   man_info      打印制造商信息。

   suspend       暂停驱动程序重新调度周期。

   resume        从暂停中恢复驱动程序。

   stop

   status        打印状态信息
```

## batt_smbus

源代码: [drivers/batt_smbus](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/batt_smbus)

### 描述

用于 BQ40Z50 燃料表 IC 的智能电池驱动程序。

### 示例

要写入闪存以设置参数。地址，字节数，字节0，... ，字节N

```
batt_smbus -X write_flash 19069 2 27 0
```

### 用法 {#batt_smbus_usage}

```
batt_smbus <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 11

   man_info      打印制造商信息。

   unseal        解封设备闪存以启用 write_flash 命令。

   seal          封装设备闪存以禁用 write_flash 命令。

   suspend       暂停驱动程序重新调度周期。

   resume        从暂停中恢复驱动程序。

   write_flash   写入闪存。设备必须首先使用 unseal 命令解封。
     [address]   开始写入的地址。
     [number of bytes] 要发送的字节数。
     [data[0]...data[n]] 一次一个字节的数据，用空格分隔。

   stop

   status        打印状态信息
```

## bst

源代码: [drivers/telemetry/bst](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/telemetry/bst)

### 用法 {#bst_usage}

```
bst <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 118

   stop

   status        打印状态信息
```

## dshot

源代码: [drivers/dshot](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/dshot)

### 描述

这是 DShot 输出驱动程序。它类似于 fmu 驱动程序，可以用作替代品
使用 DShot 作为 ESC 通信协议而不是 PWM。

启动时，模块尝试占用所有可用引脚用于 DShot 输出。
它跳过所有已在使用的引脚（例如相机触发模块）。

它支持：

- DShot150, DShot300, DShot600
- 通过独立 UART 的遥测并发布为 esc_status 消息
- 通过 CLI 发送 DShot 命令

### 示例

永久反转电机 1：

```
dshot reverse -m 1
dshot save -m 1
```

保存后，反转方向将被视为正常方向。要再次反转，请重复相同的命令。

### 用法 {#dshot_usage}

```
dshot <command> [arguments...]
 Commands:
   start

   telemetry     在 UART 上启用遥测
     -d <val>    UART 设备
                 值: <device>
     [-x]        交换 RX/TX 引脚

   reverse       反转电机方向
     [-m <val>]  电机索引 (1-based, 默认=全部)

   normal        正常电机方向
     [-m <val>]  电机索引 (1-based, 默认=全部)

   save          保存当前设置
     [-m <val>]  电机索引 (1-based, 默认=全部)

   3d_on         启用 3D 模式
     [-m <val>]  电机索引 (1-based, 默认=全部)

   3d_off        禁用 3D 模式
     [-m <val>]  电机索引 (1-based, 默认=全部)

   beep1         发送蜂鸣模式 1
     [-m <val>]  电机索引 (1-based, 默认=全部)

   beep2         发送蜂鸣模式 2
     [-m <val>]  电机索引 (1-based, 默认=全部)

   beep3         发送蜂鸣模式 3
     [-m <val>]  电机索引 (1-based, 默认=全部)

   beep4         发送蜂鸣模式 4
     [-m <val>]  电机索引 (1-based, 默认=全部)

   beep5         发送蜂鸣模式 5
     [-m <val>]  电机索引 (1-based, 默认=全部)

   stop

   status        打印状态信息
```

## fake_gps

源代码: [examples/fake_gps](https://github.com/PX4/PX4-Autopilot/tree/main/src/examples/fake_gps)

### 描述

### 用法 {#fake_gps_usage}

```
fake_gps <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## fake_imu

源代码: [examples/fake_imu](https://github.com/PX4/PX4-Autopilot/tree/main/src/examples/fake_imu)

### 描述

### 用法 {#fake_imu_usage}

```
fake_imu <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## fake_magnetometer

源代码: [examples/fake_magnetometer](https://github.com/PX4/PX4-Autopilot/tree/main/src/examples/fake_magnetometer)

### 描述

将地磁场发布为假磁力计 (sensor_mag)。
需要 vehicle_attitude 和 vehicle_gps_position。

### 用法 {#fake_magnetometer_usage}

```
fake_magnetometer <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## ft_technologies_serial

源代码: [drivers/wind_sensor/ft_technologies](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/wind_sensor/ft_technologies)

### 描述

FT Technologies 数字风传感器 FT742 的串行总线驱动程序。此驱动程序需要与
RS485 到 UART 信号转换模块一起运行。

大多数板子都配置为使用 SENS_FTX_CFG 参数在指定的 UART 上启用/启动驱动程序。

### 示例

尝试在指定的串行设备上启动驱动程序。

```
ft_technologies_serial start -d /dev/ttyS1
```

停止驱动程序

```
ft_technologies_serial stop
```

### 用法 {#ft_technologies_serial_usage}

```
ft_technologies_serial <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备

   stop          停止驱动程序
```

## gimbal

源代码: [modules/gimbal](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/gimbal)

### 描述

云台/万向节控制驱动程序。它将多种不同的输入方法（例如 RC 或 MAVLink）映射到配置的
输出（例如 AUX 通道或 MAVLink）。

使用方法的文档在 [gimbal_control](https://docs.px4.io/main/en/advanced/gimbal_control.html) 页面。

### 示例

通过设置角度测试输出（所有省略的轴设置为 0）：

```
gimbal test pitch -45 yaw 30
```

### 用法 {#gimbal_usage}

```
gimbal <command> [arguments...]
 Commands:
   start

   status

   primary-control 设置谁控制云台
     <sysid> <compid> MAVLink 系统 ID 和 MAVLink 组件 ID

   test          测试输出：为一个或多个轴设置固定角度
                 (云台必须正在运行)
     roll|pitch|yaw <angle> 指定轴和以度为单位的角度
     rollrate|pitchrate|yawrate <angle rate> 指定轴和以度/秒为单位的角度速率

   stop

   status        打印状态信息
```

## gps

源代码: [drivers/gps](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/gps)

### 描述

GPS 驱动程序模块，处理与设备的通信并通过 uORB 发布位置。
它支持多种协议（设备供应商），默认自动选择正确的协议。

该模块支持通过 `-e` 参数指定的第二个 GPS 设备。位置将发布
在第二个 uORB 主题实例上，但目前系统其他部分不使用（但是
数据将被记录，因此可用于比较）。

### 实现

每个设备都有一个轮询数据的线程。GPS 协议类使用回调实现
因此它们也可以在其他项目中使用（例如 QGroundControl 也使用它们）。

### 示例

启动 2 个 GPS 设备（主 GPS 在 /dev/ttyS3，次级在 /dev/ttyS4）：

```
gps start -d /dev/ttyS3 -e /dev/ttyS4
```

初始化 GPS 设备的热重启

```
gps reset warm
```

### 用法 {#gps_usage}

```
gps <command> [arguments...]
 Commands:
   start
     [-d <val>]  GPS 设备
                 值: <file:dev>, 默认: /dev/ttyS3
     [-b <val>]  波特率 (也可以是 p:<param_name>)
                 默认: 0
     [-e <val>]  可选的次级 GPS 设备
                 值: <file:dev>
     [-g <val>]  波特率 (次级 GPS, 也可以是 p:<param_name>)
                 默认: 0
     [-i <val>]  GPS 接口
                 值: spi|uart, 默认: uart
     [-j <val>]  次级 GPS 接口
                 值: spi|uart, 默认: uart
     [-p <val>]  GPS 协议 (默认=自动选择)
                 值: ubx|mtk|ash|eml|fem|nmea

   stop

   status        打印状态信息

   reset         重置 GPS 设备
     cold|warm|hot 指定重置类型
```

## gz_bridge

源代码: [modules/simulation/gz_bridge](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/gz_bridge)

### 描述

### 用法 {#gz_bridge_usage}

```
gz_bridge <command> [arguments...]
 Commands:
   start
     [-w <val>]  世界名称
     -n <val>    模型名称

   stop

   status        打印状态信息
```

## ina220

源代码: [drivers/power_monitor/ina220](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/power_monitor/ina220)

### 描述

INA220 电源监视器驱动程序。

此驱动程序的多个实例可以同时运行，如果每个实例都有独立的总线或 I2C 地址。

例如，一个实例可以在总线 2，地址 0x41 上运行，另一个可以在总线 2，地址 0x43 上运行。

如果 INA220 模块未通电，则默认情况下驱动程序初始化将失败。要更改此设置，请使用
-f 标志。如果设置了此标志，则如果初始化失败，驱动程序将继续尝试重新初始化
每 0.5 秒一次。设置此标志后，您可以在驱动程序启动后插入电池，它将正常工作。没有
设置此标志，电池必须在启动驱动程序之前插入。

### 用法 {#ina220_usage}

```
ina220 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 65
     [-k]        如果初始化 (探测) 失败，则定期继续重试
     [-t <val>]  用于校准值的电池索引 (1 或 3)
                 默认: 1
     [-T <val>]  类型
                 值: VBATT|VREG, 默认: VBATT

   stop

   status        打印状态信息
```

## ina226

源代码: [drivers/power_monitor/ina226](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/power_monitor/ina226)

### 描述

INA226 电源监视器驱动程序。

此驱动程序的多个实例可以同时运行，如果每个实例都有独立的总线或 I2C 地址。

例如，一个实例可以在总线 2，地址 0x41 上运行，另一个可以在总线 2，地址 0x43 上运行。

如果 INA226 模块未通电，则默认情况下驱动程序初始化将失败。要更改此设置，请使用
-f 标志。如果设置了此标志，则如果初始化失败，驱动程序将继续尝试重新初始化
每 0.5 秒一次。设置此标志后，您可以在驱动程序启动后插入电池，它将正常工作。没有
设置此标志，电池必须在启动驱动程序之前插入。

### 用法 {#ina226_usage}

```
ina226 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 65
     [-k]        如果初始化 (探测) 失败，则定期继续重试
     [-t <val>]  用于校准值的电池索引 (1 或 3)
                 默认: 1

   stop

   status        打印状态信息
```

## ina228

源代码: [drivers/power_monitor/ina228](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/power_monitor/ina228)

### 描述

INA228 电源监视器驱动程序。

此驱动程序的多个实例可以同时运行，如果每个实例都有独立的总线或 I2C 地址。

例如，一个实例可以在总线 2，地址 0x45 上运行，另一个可以在总线 2，地址 0x45 上运行。

如果 INA228 模块未通电，则默认情况下驱动程序初始化将失败。要更改此设置，请使用
-f 标志。如果设置了此标志，则如果初始化失败，驱动程序将继续尝试重新初始化
每 0.5 秒一次。设置此标志后，您可以在驱动程序启动后插入电池，它将正常工作。没有
设置此标志，电池必须在启动驱动程序之前插入。

### 用法 {#ina228_usage}

```
ina228 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 69
     [-k]        如果初始化 (探测) 失败，则定期继续重试
     [-t <val>]  用于校准值的电池索引 (1 或 3)
                 默认: 1

   stop

   status        打印状态信息
```

## ina238

源代码: [drivers/power_monitor/ina238](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/power_monitor/ina238)

### 描述

INA238 电源监视器驱动程序。

此驱动程序的多个实例可以同时运行，如果每个实例都有独立的总线或 I2C 地址。

例如，一个实例可以在总线 2，地址 0x45 上运行，另一个可以在总线 2，地址 0x45 上运行。

如果 INA238 模块未通电，则默认情况下驱动程序初始化将失败。要更改此设置，请使用
-f 标志。如果设置了此标志，则如果初始化失败，驱动程序将继续尝试重新初始化
每 0.5 秒一次。设置此标志后，您可以在驱动程序启动后插入电池，它将正常工作。没有
设置此标志，电池必须在启动驱动程序之前插入。

### 用法 {#ina238_usage}

```
ina238 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 69
     [-k]        如果初始化 (探测) 失败，则定期继续重试
     [-t <val>]  用于校准值的电池索引 (1 或 3)
                 默认: 1

   stop

   status        打印状态信息
```

## iridiumsbd

源代码: [drivers/telemetry/iridiumsbd](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/telemetry/iridiumsbd)

### 描述

IridiumSBD 驱动程序。

创建另一个模块可以用于通信的虚拟串行端口（例如 mavlink）。

### 用法 {#iridiumsbd_usage}

```
iridiumsbd <command> [arguments...]
 Commands:
   start
     -d <val>    串行设备
                 值: <file:dev>
     [-v]        启用详细输出

   test
     [s|read|AT <cmd>] 测试命令

   stop

   status        打印状态信息
```

## irlock

源代码: [drivers/irlock](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/irlock)

### 用法 {#irlock_usage}

```
irlock <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 84

   stop

   status        打印状态信息
```

## linux_pwm_out

源代码: [drivers/linux_pwm_out](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/linux_pwm_out)

### 描述

具有板级特定后端实现的 Linux PWM 输出驱动程序。

### 用法 {#linux_pwm_out_usage}

```
linux_pwm_out <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## lsm303agr

源代码: [drivers/magnetometer/lsm303agr](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/lsm303agr)

### 用法 {#lsm303agr_usage}

```
lsm303agr <command> [arguments...]
 Commands:
   start
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## msp_osd

源代码: [drivers/osd/msp_osd](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/osd/msp_osd)

### 描述

MSP 遥测流

### 实现

将 uORB 消息转换为 MSP 遥测包

### 示例

CLI 使用示例：

```
msp_osd
```

### 用法 {#msp_osd_usage}

```
msp_osd <command> [arguments...]
 Commands:
   stop

   status        打印状态信息

   channel       更改 VTX 通道
```

## newpixel

源代码: [drivers/lights/neopixel](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/lights/neopixel)

### 描述

此模块负责驱动 Neopixel 串行 LED 的接口

### 示例

通常以以下方式启动：

```
neopixel -n 8
```

驱动所有可用的 LED。

### 用法 {#newpixel_usage}

```
newpixel <command> [arguments...]
 Commands:
   stop

   status        打印状态信息
```

## paa3905

源代码: [drivers/optical_flow/paa3905](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/optical_flow/paa3905)

### 用法 {#paa3905_usage}

```
paa3905 <command> [arguments...]
 Commands:
   start
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-Y <val>]  自定义偏航旋转 (度)
                 默认: 0

   stop

   status        打印状态信息
```

## paw3902

源代码: [drivers/optical_flow/paw3902](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/optical_flow/paw3902)

### 用法 {#paw3902_usage}

```
paw3902 <command> [arguments...]
 Commands:
   start
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-Y <val>]  自定义偏航旋转 (度)
                 默认: 0

   stop

   status        打印状态信息
```

## pca9685_pwm_out

源代码: [drivers/pca9685_pwm_out](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/pca9685_pwm_out)

### 描述

这是一个 PCA9685 PWM 输出驱动程序。

它在 I2C 工作队列上运行，与 FC 控制环异步，
获取最新的混合结果并在其调度 tick 时将它们写入 PCA9685。

它可以执行完整的 12 位输出作为占空比模式，同时也能输出精确的脉冲宽度
大多数 ESC 和舵机都能接受。

### 示例

通常以以下方式启动：

```
pca9685_pwm_out start -a 0x40 -b 1
```

### 用法 {#pca9685_pwm_out_usage}

```
pca9685_pwm_out <command> [arguments...]
 Commands:
   start         启动任务
     [-a <val>]  PCA9685 的 7 位 I2C 地址
                 值: <addr>, 默认: 0x40
     [-b <val>]  pca9685 连接的总线
                 默认: 1

   stop

   status        打印状态信息
```

## pm_selector_auterion

源代码: [drivers/power_monitor/pm_selector_auterion](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/power_monitor/pm_selector_auterion)

### 描述

用于启动和自动检测不同电源监视器的驱动程序。

### 用法 {#pm_selector_auterion_usage}

```
pm_selector_auterion <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## pmw3901

源代码: [drivers/optical_flow/pmw3901](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/optical_flow/pmw3901)

### 用法 {#pmw3901_usage}

```
pmw3901 <command> [arguments...]
 Commands:
   start
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## pps_capture

源代码: [drivers/pps_capture](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/pps_capture)

### 描述

这实现了从 GNSS 模块捕获 PPS 信息，并计算 PPS 和实时时钟之间的漂移。

### 用法 {#pps_capture_usage}

```
pps_capture <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## pwm_out

源代码: [drivers/pwm_out](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/pwm_out)

### 描述

此模块负责驱动输出引脚。对于没有独立 IO 芯片的板子
(例如 Pixracer)，它使用主通道。在有 IO 芯片的板子上(例如 Pixhawk)，它使用 AUX 通道，而
px4io 驱动程序用于主通道。

### 用法 {#pwm_out_usage}

```
pwm_out <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## pwm_out_sim

源代码: [modules/simulation/pwm_out_sim](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/pwm_out_sim)

### 描述

模拟 PWM 输出驱动程序。

其唯一功能是获取 `actuator_control` uORB 消息，
将它们与任何加载的混合器混合，并将结果输出到
`actuator_output` uORB 主题。

它用于 SITL 和 HITL。

### 用法 {#pwm_out_sim_usage}

```
pwm_out_sim <command> [arguments...]
 Commands:
   start         启动模块
     [-m <val>]  模式
                 值: hil|sim, 默认: sim

   stop

   status        打印状态信息
```

## px4flow

源代码: [drivers/optical_flow/px4flow](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/optical_flow/px4flow)

### 用法 {#px4flow_usage}

```
px4flow <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 66

   stop

   status        打印状态信息
```

## px4io

源代码: [drivers/px4io](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/px4io)

### 描述

与 IO 协处理器通信的输出驱动程序。

### 用法 {#px4io_usage}

```
px4io <command> [arguments...]
 Commands:
   start

   checkcrc      检查固件文件的 CRC 与 IO 上的当前代码
     <filename>  固件文件

   update        更新 IO 固件
     [<filename>] 固件文件

   debug         设置 IO 调试级别
     <debug_level> 0=禁用, 9=最大详细程度

   bind          DSM 绑定
     dsm2|dsmx|dsmx8 协议

   sbus1_out     启用 sbus1 输出

   sbus2_out     启用 sbus2 输出

   supported     如果支持 px4io 则返回 0

   test_fmu_fail 测试: 关闭 IO 更新

   test_fmu_ok   重新启用 IO 更新

   stop

   status        打印状态信息
```

## rgbled

源代码: [drivers/lights/rgbled_ncp5623c](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/lights/rgbled_ncp5623c)

### 用法 {#rgbled_usage}

```
rgbled <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 57
     [-o <val>]  RGB PWM 分配
                 默认: 123

   stop

   status        打印状态信息
```

## rgbled_aw2023

源代码: [drivers/lights/rgbled_aw2023](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/lights/rgbled_aw2023)

### 用法 {#rgbled_aw2023_usage}

```
rgbled_aw2023 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 69

   stop

   status        打印状态信息
```

## rgbled_is31fl3195

源代码: [drivers/lights/rgbled_is31fl3195](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/lights/rgbled_is31fl3195)

### 用法 {#rgbled_is31fl3195_usage}

```
rgbled_is31fl3195 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 84
     [-o <val>]  RGB PWM 分配
                 默认: 123
     [-i <val>]  电流带
                 默认: 0.5

   stop

   status        打印状态信息
```

## rgbled_lp5562

源代码: [drivers/lights/rgbled_lp5562](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/lights/rgbled_lp5562)

### 描述

通过 I2C 连接的 [LP5562](https://www.ti.com/product/LP5562) LED 驱动程序。

这在一些 Holybro 的 GPS 模块中用于 [PX4 状态通知](../getting_started/led_meanings.md)

该驱动程序默认包含在固件中（KConfig 密钥 DRIVERS_LIGHTS_RGBLED_LP5562）并且始终启用。

### 用法 {#rgbled_lp5562_usage}

```
rgbled_lp5562 <command> [arguments...]
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
     [-u <val>]  电流 mA
                 默认: 17.5

   stop

   status        打印状态信息
```

## roboclaw

源代码: [drivers/roboclaw](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/roboclaw)

### 描述

此驱动程序通过 UART 与 [Roboclaw 电机驱动器](https://www.basicmicro.com/motor-controller) 通信。
它执行两个任务：

- 基于 OutputModuleInterface 控制电机。
- 读取轮子编码器并将原始数据发布在 `wheel_encoders` uORB 主题中

为了使用此驱动程序，Roboclaw 应该置于数据包串行模式（参见链接的文档），并且
您的飞控的 UART 端口应该按照文档所示连接到 Roboclaw。
需要使用参数 `RBCLW_SER_CFG` 启用驱动程序，波特率需要设置正确，
地址 `RBCLW_ADDRESS` 需要与 ESC 配置匹配。

启动此驱动程序的命令是：`$ roboclaw start <UART device> <baud rate>`

### 用法 {#roboclaw_usage}

```
roboclaw <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## rpm_capture

源代码: [drivers/rpm_capture](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/rpm_capture)

### 用法 {#rpm_capture_usage}

```
rpm_capture <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## safety_button

源代码: [drivers/safety_button](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/safety_button)

### 描述

此模块负责安全按钮。
快速按下安全按钮 3 次将触发 GCS 配对请求。

### 用法 {#safety_button_usage}

```
safety_button <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## septentrio

源代码: [drivers/gnss/septentrio](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/gnss/septentrio)

### 描述

Septentrio GNSS 接收器驱动程序。
它可以自动配置它们并使输出对系统其他部分可用。
支持次级接收器以实现冗余、日志记录和双接收器航向。
支持 Septentrio 接收器的波特率从 57600 到 1500000。
如果使用其他波特率，驱动程序将使用 230400 并给出警告。

### 示例

在端口 `/dev/ttyS0` 上使用一个接收器并自动配置它使用波特率 230400：

```
septentrio start -d /dev/ttyS0 -b 230400
```

使用两个接收器，主接收器在端口 `/dev/ttyS3` 上，次级接收器在 `/dev/ttyS4` 上，
自动检测波特率并保持它们：

```
septentrio start -d /dev/ttyS3 -e /dev/ttyS4
```

执行接收器的热重启：

```
gps reset warm
```

### 用法 {#septentrio_usage}

```
septentrio <command> [arguments...]
 Commands:
   start
     -d <val>    主接收器端口
                 值: <file:dev>
     [-b <val>]  主接收器波特率
                 默认: 0
     [-e <val>]  次级接收器端口
                 值: <file:dev>
     [-g <val>]  次级接收器波特率
                 默认: 0

   stop

   status        打印状态信息

   reset         重置连接的接收器
     cold|warm|hot 指定重置类型
```

## sht3x

源代码: [drivers/hygrometer/sht3x](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/hygrometer/sht3x)

### 描述

由 Senserion 生产的 SHT3x 温度和湿度传感器驱动程序。

### 示例

CLI 使用示例：

```
sht3x start -X
```

在外部总线上启动传感器驱动程序

```
sht3x status
```

打印驱动程序状态

```
sht3x values
```

打印最后测量的值

```
sht3x reset
```

重新初始化传感器，重置标志

### 用法 {#sht3x_usage}

```
sht3x <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 68
     [-k]        如果初始化 (探测) 失败，则定期继续重试

   stop

   status        打印状态信息

   values        打印实际数据

   reset         重新初始化传感器
```

## tap_esc

源代码: [drivers/tap_esc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/tap_esc)

### 描述

此模块通过 UART 控制 TAP_ESC 硬件。它监听
执行器控制主题，进行混合并写入 PWM 输出。

### 实现

目前该模块仅以线程版本实现，这意味着它
在自己的线程中运行而不是在工作队列上。

### 示例

该模块通常以以下方式启动：

```
tap_esc start -d /dev/ttyS2 -n <1-8>
```

### 用法 {#tap_esc_usage}

```
tap_esc <command> [arguments...]
 Commands:
   start         启动任务
     [-d <val>]  用于与 ESC 通信的设备
                 值: <device>
     [-n <val>]  ESC 数量
                 默认: 4
```

## tone_alarm

源代码: [drivers/tone_alarm](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/tone_alarm)

### 描述

此模块负责蜂鸣报警。

### 用法 {#tone_alarm_usage}

```
tone_alarm <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## uwb

源代码: [drivers/uwb/uwb_sr150](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/uwb/uwb_sr150)

### 描述

NXP UWB_SR150 UWB 定位系统驱动程序。此驱动程序发布 `uwb_distance` 消息
每当 UWB_SR150 有位置测量可用时。

### 示例

使用给定设备启动驱动程序：

```
uwb start -d /dev/ttyS2
```

### 用法 {#uwb_usage}

```
uwb <command> [arguments...]
 Commands:
   start
     -d <val>    用于与 UWB 串行通信的设备名称
                 值: <file:dev>
     -b <val>    串行通信的波特率
                 值: <int>

   stop

   status
```

## vertiq_io

源代码: [drivers/actuators/vertiq_io](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/actuators/vertiq_io)

### 用法 {#vertiq_io_usage}

```
vertiq_io <command> [arguments...]
 Commands:
   start
     <device>    UART 设备

   stop

   status        打印状态信息
```

## voxl2_io

源代码: [drivers/voxl2_io](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/voxl2_io)

### 描述

此模块负责驱动输出引脚。对于没有独立 IO 芯片的板子
(例如 Pixracer)，它使用主通道。在有 IO 芯片的板子上(例如 Pixhawk)，它使用 AUX 通道，而
px4io 驱动程序用于主通道。

### 用法 {#voxl2_io_usage}

```
voxl2_io <command> [arguments...]
 Commands:
   start         启动任务
     -v          详细消息
     -d          禁用 PWM
     -e          禁用 RC
     -p <val>    UART 端口

   calibrate_escs 校准 ESC 最小/最大范围

   enable_debug  启用驱动程序调试

   stop

   status        打印状态信息
```

## voxl_esc

源代码: [drivers/actuators/voxl_esc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/actuators/voxl_esc)

### 描述

此模块负责...

### 实现

默认情况下，该模块在 uORB 执行器控制主题的工作队列上运行回调。

### 示例

通常以以下方式启动：

```
todo
```

### 用法 {#voxl_esc_usage}

```
voxl_esc <command> [arguments...]
 Commands:
   start         启动任务

   reset         向 ESC 发送重置请求
     -i <val>    ESC ID, 0-3

   version       向 ESC 发送版本请求
     -i <val>    ESC ID, 0-3

   version-ext   向 ESC 发送扩展版本请求
     -i <val>    ESC ID, 0-3

   rpm           闭环 RPM 测试控制请求
     -i <val>    ESC ID, 0-3
     -r <val>    RPM, -32,768 到 32,768
     -n <val>    命令重复次数, 0 到 INT_MAX
     -t <val>    重复命令之间的延迟 (微秒), 0 到 INT_MAX

   pwm           开环 PWM 测试控制请求
     -i <val>    ESC ID, 0-3
     -r <val>    占空比值, 0 到 800
     -n <val>    命令重复次数, 0 到 INT_MAX
     -t <val>    重复命令之间的延迟 (微秒), 0 到 INT_MAX

   tone          向 ESC 发送音调生成请求
     -i <val>    ESC ID, 0-3
     -p <val>    声音周期，反向频率，0-255
     -d <val>    声音持续时间，0-255，1LSB = 13ms
     -v <val>    声音功率 (音量)，0-100

   led           发送 LED 控制请求
     -l <val>    位掩码 0x0FFF (12 位) - ESC0 (RGB) ESC1 (RGB) ESC2 (RGB)
                 ESC3 (RGB)

   stop

   status        打印状态信息
```

## voxlpm

源代码: [drivers/power_monitor/voxlpm](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/power_monitor/voxlpm)

### 用法 {#voxlpm_usage}

```
voxlpm [arguments...]
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 68
     [-T <val>]  类型
                 值: VBATT|P5VDC|P12VDC, 默认: VBATT
     [-k]        如果初始化 (探测) 失败，则定期继续重试

   stop

   status        打印状态信息
```

## zenoh

源代码: [modules/zenoh](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/zenoh)

### 描述

Zenoh 演示桥接

### 用法 {#zenoh_usage}

```
zenoh <command> [arguments...]
 Commands:
   start

   stop

   status

   config
```