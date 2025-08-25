# 模块参考: 惯性测量单元 (驱动程序)

## adis16448

源代码: [drivers/imu/analog_devices/adis16448](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/analog_devices/adis16448)

### 用法 {#adis16448_usage}

```
adis16448 <command> [arguments...]
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

## adis16470

源代码: [drivers/imu/analog_devices/adis16470](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/analog_devices/adis16470)

### 用法 {#adis16470_usage}

```
adis16470 <command> [arguments...]
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

## adis16477

源代码: [drivers/imu/analog_devices/adis16477](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/analog_devices/adis16477)

### 用法 {#adis16477_usage}

```
adis16477 <command> [arguments...]
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

## adis16497

源代码: [drivers/imu/analog_devices/adis16497](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/analog_devices/adis16497)

### 用法 {#adis16497_usage}

```
adis16497 <command> [arguments...]
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

## adis16507

源代码: [drivers/imu/analog_devices/adis16507](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/analog_devices/adis16507)

### 用法 {#adis16507_usage}

```
adis16507 <command> [arguments...]
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

## bmi055

源代码: [drivers/imu/bosch/bmi055](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/bosch/bmi055)

### 用法 {#bmi055_usage}

```
bmi055 <command> [arguments...]
 Commands:
   start
     [-A]        加速度计
     [-G]        陀螺仪
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

## bmi085

源代码: [drivers/imu/bosch/bmi085](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/bosch/bmi085)

### 用法 {#bmi085_usage}

```
bmi085 <command> [arguments...]
 Commands:
   start
     [-A]        加速度计
     [-G]        陀螺仪
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

## bmi088

源代码: [drivers/imu/bosch/bmi088](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/bosch/bmi088)

### 用法 {#bmi088_usage}

```
bmi088 <command> [arguments...]
 Commands:
   start
     [-A]        加速度计
     [-G]        陀螺仪
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

## bmi088_i2c

源代码: [drivers/imu/bosch/bmi088_i2c](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/bosch/bmi088_i2c)

### 用法 {#bmi088_i2c_usage}

```
bmi088_i2c <command> [arguments...]
 Commands:
   start
     [-A]        加速度计
     [-G]        陀螺仪
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 24
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## bmi270

源代码: [drivers/imu/bosch/bmi270](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/bosch/bmi270)

### 用法 {#bmi270_usage}

```
bmi270 <command> [arguments...]
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

## fxas21002c

源代码: [drivers/imu/nxp/fxas21002c](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/nxp/fxas21002c)

### 用法 {#fxas21002c_usage}

```
fxas21002c <command> [arguments...]
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
                 默认: 32
     [-R <val>]  旋转
                 默认: 0

   regdump

   testerror

   stop

   status        打印状态信息
```

## fxos8701cq

源代码: [drivers/imu/nxp/fxos8701cq](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/nxp/fxos8701cq)

### 用法 {#fxos8701cq_usage}

```
fxos8701cq <command> [arguments...]
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

   regdump

   testerror

   stop

   status        打印状态信息
```

## iam20680hp

源代码: [drivers/imu/invensense/iam20680hp](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/iam20680hp)

### 用法 {#iam20680hp_usage}

```
iam20680hp <command> [arguments...]
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

## icm20602

源代码: [drivers/imu/invensense/icm20602](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm20602)

### 用法 {#icm20602_usage}

```
icm20602 <command> [arguments...]
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

## icm20608g

源代码: [drivers/imu/invensense/icm20608g](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm20608g)

### 用法 {#icm20608g_usage}

```
icm20608g <command> [arguments...]
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

## icm20649

源代码: [drivers/imu/invensense/icm20649](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm20649)

### 用法 {#icm20649_usage}

```
icm20649 <command> [arguments...]
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

## icm20689

源代码: [drivers/imu/invensense/icm20689](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm20689)

### 用法 {#icm20689_usage}

```
icm20689 <command> [arguments...]
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

## icm20948

源代码: [drivers/imu/invensense/icm20948](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm20948)

### 用法 {#icm20948_usage}

```
icm20948 <command> [arguments...]
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
     [-M]        启用磁力计 (AK8963)
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## icm20948_i2c_passthrough

源代码: [drivers/imu/invensense/icm20948](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm20948)

### 用法 {#icm20948_i2c_passthrough_usage}

```
icm20948_i2c_passthrough <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 105

   stop

   status        打印状态信息
```

## icm40609d

源代码: [drivers/imu/invensense/icm40609d](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm40609d)

### 用法 {#icm40609d_usage}

```
icm40609d <command> [arguments...]
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

## icm42605

源代码: [drivers/imu/invensense/icm42605](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm42605)

### 用法 {#icm42605_usage}

```
icm42605 <command> [arguments...]
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

## icm42670p

源代码: [drivers/imu/invensense/icm42670p](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm42670p)

### 用法 {#icm42670p_usage}

```
icm42670p <command> [arguments...]
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

## icm42688p

源代码: [drivers/imu/invensense/icm42688p](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm42688p)

### 用法 {#icm42688p_usage}

```
icm42688p <command> [arguments...]
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
     [-C <val>]  输入时钟频率 (Hz)
                 默认: 0
     [-6]        驱动 ICM-42686

   stop

   status        打印状态信息
```

## icm45686

源代码: [drivers/imu/invensense/icm45686](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm45686)

### 用法 {#icm45686_usage}

```
icm45686 <command> [arguments...]
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
     [-C <val>]  输入时钟频率 (Hz)
                 默认: 0

   stop

   status        打印状态信息
```

## iim42652

源代码: [drivers/imu/invensense/iim42652](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/iim42652)

### 用法 {#iim42652_usage}

```
iim42652 <command> [arguments...]
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
     [-C <val>]  输入时钟频率 (Hz)
                 默认: 0

   stop

   status        打印状态信息
```

## iim42653

源代码: [drivers/imu/invensense/iim42653](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/iim42653)

### 用法 {#iim42653_usage}

```
iim42653 <command> [arguments...]
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
     [-C <val>]  输入时钟频率 (Hz)
                 默认: 0

   stop

   status        打印状态信息
```

## l3gd20

源代码: [drivers/imu/st/l3gd20](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/st/l3gd20)

### 用法 {#l3gd20_usage}

```
l3gd20 <command> [arguments...]
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

   regdump

   testerror

   stop

   status        打印状态信息
```

## lsm303d

源代码: [drivers/imu/st/lsm303d](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/st/lsm303d)

### 用法 {#lsm303d_usage}

```
lsm303d <command> [arguments...]
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

## lsm9ds1

源代码: [drivers/imu/st/lsm9ds1](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/st/lsm9ds1)

### 用法 {#lsm9ds1_usage}

```
lsm9ds1 <command> [arguments...]
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

## mpu6000

源代码: [drivers/imu/invensense/mpu6000](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/mpu6000)

### 用法 {#mpu6000_usage}

```
mpu6000 <command> [arguments...]
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

## mpu9250

源代码: [drivers/imu/invensense/mpu9250](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/mpu9250)

### 用法 {#mpu9250_usage}

```
mpu9250 <command> [arguments...]
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
     [-M]        启用磁力计 (AK8963)
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## mpu9250_i2c

源代码: [drivers/imu/invensense/mpu9250](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/mpu9250)

### 用法 {#mpu9250_i2c_usage}

```
mpu9250_i2c <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 104
     [-R <val>]  旋转
                 默认: 0

   stop

   status        打印状态信息
```

## mpu9520

源代码: [drivers/imu/invensense/mpu6500](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/mpu6500)

### 用法 {#mpu9520_usage}

```
mpu9520 <command> [arguments...]
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

## sch16t

源代码: [drivers/imu/murata/sch16t](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/murata/sch16t)

### 用法 {#sch16t_usage}

```
sch16t <command> [arguments...]
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