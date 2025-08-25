# 模块参考: 气压计 (驱动程序)

## bmp280

源代码: [drivers/barometer/bmp280](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/bmp280)

### 用法 {#bmp280_usage}

```
bmp280 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 118
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

## bmp388

源代码: [drivers/barometer/bmp388](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/bmp388)

### 用法 {#bmp388_usage}

```
bmp388 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 118

   stop

   status        打印状态信息
```

## bmp581

源代码: [drivers/barometer/bmp581](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/bmp581)

### 用法 {#bmp581_usage}

```
bmp581 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 70

   stop

   status        打印状态信息
```

## dps310

源代码: [drivers/barometer/dps310](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/dps310)

### 用法 {#dps310_usage}

```
dps310 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 119
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

## icp101xx

源代码: [drivers/barometer/invensense/icp101xx](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/invensense/icp101xx)

### 用法 {#icp101xx_usage}

```
icp101xx <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 99

   stop

   status        打印状态信息
```

## icp201xx

源代码: [drivers/barometer/invensense/icp201xx](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/invensense/icp201xx)

### 用法 {#icp201xx_usage}

```
icp201xx <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 99

   stop

   status        打印状态信息
```

## lps22hb

源代码: [drivers/barometer/lps22hb](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/lps22hb)

### 用法 {#lps22hb_usage}

```
lps22hb <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
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

## lps25h

源代码: [drivers/barometer/lps25h](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/lps25h)

### 用法 {#lps25h_usage}

```
lps25h <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
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

## lps33hw

源代码: [drivers/barometer/lps33hw](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/lps33hw)

### 用法 {#lps33hw_usage}

```
lps33hw <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 93
     [-k]        如果初始化 (探测) 失败，则定期继续重试

   stop

   status        打印状态信息
```

## mpc2520

源代码: [drivers/barometer/maiertek/mpc2520](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/maiertek/mpc2520)

### 用法 {#mpc2520_usage}

```
mpc2520 <command> [arguments...]
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

## mpl3115a2

源代码: [drivers/barometer/mpl3115a2](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/mpl3115a2)

### 用法 {#mpl3115a2_usage}

```
mpl3115a2 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 96

   stop

   status        打印状态信息
```

## ms5611

源代码: [drivers/barometer/ms5611](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/ms5611)

### 用法 {#ms5611_usage}

```
ms5611 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-T <val>]  设备类型
                 值: 5607|5611, 默认: 5611

   stop

   status        打印状态信息
```

## ms5837

源代码: [drivers/barometer/ms5837](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/ms5837)

### 用法 {#ms5837_usage}

```
ms5837 <command> [arguments...]
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

## spa06

源代码: [drivers/barometer/goertek/spa06](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/goertek/spa06)

### 用法 {#spa06_usage}

```
spa06 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 118
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

## spl06

源代码: [drivers/barometer/goertek/spl06](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/barometer/goertek/spl06)

### 用法 {#spl06_usage}

```
spl06 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-s]        内部 SPI 总线
     [-S]        外部 SPI 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-c <val>]  芯片选择引脚 (用于内部 SPI) 或索引 (用于外部 SPI)
     [-m <val>]  SPI 模式
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 118
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