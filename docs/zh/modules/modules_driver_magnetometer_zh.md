# 模块参考: 磁力计 (驱动程序)

## ak09916

源代码: [drivers/magnetometer/akm/ak09916](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/akm/ak09916)

### 用法 {#ak09916_usage}

```
ak09916 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 12
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## ak8963

源代码: [drivers/magnetometer/akm/ak8963](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/akm/ak8963)

### 用法 {#ak8963_usage}

```
ak8963 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 12
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## bmm150

源代码: [drivers/magnetometer/bosch/bmm150](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/bosch/bmm150)

### 用法 {#bmm150_usage}

```
bmm150 <command> [arguments...]
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
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## bmm350

源代码: [drivers/magnetometer/bosch/bmm350](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/bosch/bmm350)

### 用法 {#bmm350_usage}

```
bmm350 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 20
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## hmc5883

源代码: [drivers/magnetometer/hmc5883](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/hmc5883)

### 用法 {#hmc5883_usage}

```
hmc5883 <command> [arguments...]
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
     [-R <val>]  旋转
                 默认: 0
     [-T]        启用温度补偿

   stop

   status        打印状态信息
```

## iis2mdc

源代码: [drivers/magnetometer/st/iis2mdc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/st/iis2mdc)

### 用法 {#iis2mdc_usage}

```
iis2mdc <command> [arguments...]
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

   stop

   status        打印状态信息
```

## ist8308

源代码: [drivers/magnetometer/isentek/ist8308](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/isentek/ist8308)

### 用法 {#ist8308_usage}

```
ist8308 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 12
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## ist8310

源代码: [drivers/magnetometer/isentek/ist8310](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/isentek/ist8310)

### 用法 {#ist8310_usage}

```
ist8310 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 14
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## lis3mdl

源代码: [drivers/magnetometer/lis3mdl](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/lis3mdl)

### 用法 {#lis3mdl_usage}

```
lis3mdl <command> [arguments...]
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
                 默认: 30
     [-R <val>]  旋转
                 默认: 0

   reset

   stop

   status        打印状态信息
```

## lsm9ds1_mag

源代码: [drivers/magnetometer/lsm9ds1_mag](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/lsm9ds1_mag)

### 用法 {#lsm9ds1_mag_usage}

```
lsm9ds1_mag <command> [arguments...]
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

## mmc5983ma

源代码: [drivers/magnetometer/memsic/mmc5983ma](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/memsic/mmc5983ma)

### 用法 {#mmc5983ma_usage}

```
mmc5983ma <command> [arguments...]
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
                 默认: 48
     [-R <val>]  旋转
                 默认: 0

   reset

   stop

   status        打印状态信息
```

## qmc5883l

源代码: [drivers/magnetometer/qmc5883l](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/qmc5883l)

### 用法 {#qmc5883l_usage}

```
qmc5883l <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 13
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## qmc5883p

源代码: [drivers/magnetometer/qmc5883p](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/qmc5883p)

### 用法 {#qmc5883p_usage}

```
qmc5883p <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 44
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## rm3100

源代码: [drivers/magnetometer/rm3100](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/rm3100)

### 用法 {#rm3100_usage}

```
rm3100 <command> [arguments...]
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
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## vcm1193l

源代码: [drivers/magnetometer/vtrantech/vcm1193l](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/magnetometer/vtrantech/vcm1193l)

### 用法 {#vcm1193l_usage}

```
vcm1193l <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```