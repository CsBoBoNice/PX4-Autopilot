# 模块参考: 空速传感器 (驱动程序)

## asp5033

源代码: [drivers/differential_pressure/asp5033](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/differential_pressure/asp5033)


### 描述
驱动程序用于启用通过 I2C 连接的外部 [ASP5033]
(https://www.qio-tek.com/index.php/product/qiotek-asp5033-dronecan-airspeed-and-compass-module/)
TE。
默认情况下不包含在固件中。可以通过终端命令包含："make <your_board> boardconfig"
或在 default.px4board 中添加行："CONFIG_DRIVERS_DIFFERENTIAL_PRESSURE_ASP5033=y"
可以通过将 "SENS_EN_ASP5033" 参数设置为 1 来启用。

### 用法 {#asp5033_usage}

```
asp5033 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 109

   stop

   status        打印状态信息
```

## auav

源代码: [drivers/differential_pressure/auav](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/differential_pressure/auav)

### 用法 {#auav_usage}

```
auav <command> [arguments...]
 Commands:
   start
     [-D]        差压传感
     [-A]        绝对压力传感
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 38

   stop

   status        打印状态信息
```

## ets_airspeed

源代码: [drivers/differential_pressure/ets](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/differential_pressure/ets)

### 用法 {#ets_airspeed_usage}

```
ets_airspeed <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 117

   stop

   status        打印状态信息
```

## ms4515

源代码: [drivers/differential_pressure/ms4515](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/differential_pressure/ms4515)

### 用法 {#ms4515_usage}

```
ms4515 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 70

   stop

   status        打印状态信息
```

## ms4525do

源代码: [drivers/differential_pressure/ms4525do](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/differential_pressure/ms4525do)

### 用法 {#ms4525do_usage}

```
ms4525do <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 40

   stop

   status        打印状态信息
```

## ms5525dso

源代码: [drivers/differential_pressure/ms5525dso](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/differential_pressure/ms5525dso)

### 用法 {#ms5525dso_usage}

```
ms5525dso <command> [arguments...]
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

## sdp3x

源代码: [drivers/differential_pressure/sdp3x](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/differential_pressure/sdp3x)

### 用法 {#sdp3x_usage}

```
sdp3x <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 33
     [-k]        如果初始化 (探测) 失败，则定期继续重试

   stop

   status        打印状态信息
```