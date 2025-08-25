# ThePeach FCC-R1

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://thepeach.kr/)获取硬件支持或合规问题。
:::

**ThePeach FCC-R1**是**ThePeach**设计和制造的高级自动驾驶仪。

它基于**Pixhawk项目FMUv3**开源硬件设计，在**Nuttx OS**上运行**PX4**。

![ThePeach_R1](../../assets/flight_controller/thepeach_r1/main.png)

## 规格

- 主处理器：STM32F427VIT6
  - 32位ARM Cortex-M4，168 MHz 256 KB RAM 2 MB闪存

- IO处理器：STM32F100C8T6
  - ARM Cortex-M3，32位ARM Cortex-M3，24 MHz，8KB SRAM

- 板载传感器
  - 加速度计/陀螺仪：ICM-20602
  - 加速度计/陀螺仪/磁力计：MPU-9250
  - 气压计：MS5611

- 接口
  - 8+6个PWM输出（IO输出8个，FMU输出6个）
  - Spektrum DSM / DSM2 / DSM-X卫星兼容输入
  - Futaba S.BUS兼容输入和输出
  - PPM和信号输入
  - 模拟/PWM RSSI输入
  - S.Bus舵机输出
  - 安全开关/LED
  - 4个UART：TELEM1、TELEM2（Raspberry Pi CM3+）、GPS、SERIAL4
  - 1个I2C端口
  - 1个CAN总线
  - 1个电池的电压/电流模拟输入

- Raspberry Pi CM3+接口
  - VBUS
  - DDR2连接器：Raspberry Pi CM3+
  - 1个UART
  - 2个USB
  - 1个Raspberry Pi摄像头

- 机械特性
  - 尺寸：49.2 x 101 x 18.2mm
  - 重量：100g

## 连接器

![pinmap_top](../../assets/flight_controller/thepeach_r1/pinmap.png)

## 串口映射

| UART   | 设备       | 端口                       |
| ------ | ---------- | -------------------------- |
| USART1 | /dev/ttyS0 | IO处理器调试               |
| USART2 | /dev/ttyS1 | TELEM1（流控制）           |
| USART3 | /dev/ttyS2 | TELEM2（Raspberry pi cm3+）|
| UART4  | /dev/ttyS3 | GPS1                       |
| USART6 | /dev/ttyS4 | PX4IO                      |
| UART7  | /dev/ttys5 | 调试控制台                 |
| UART8  | /dev/ttyS6 | TELEM4                     |

## 电压额定值

如果提供两个电源，**ThePeach FCC-R1**可以实现电源双重冗余。两个电源轨是：**POWER**和**USB**。

注意：

1. 输出电源轨**FMU PWM OUT**和**I/O PWM OUT**不为飞行控制器板供电（也不由其供电）。您必须向**POWER**或**USB**中的一个供电，否则板子将无电源。
2. USB不为**Raspberry Pi CM3+**供电。您必须向**POWER**供电，否则Raspberry Pi CM3+将无电源。

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. POWER输入（5V到5.5V）
2. USB输入（4.75V到5.25V）

**绝对最大额定值**

在这些条件下，所有电源都会对飞行控制器造成永久损坏。

1. POWER输入（5.5V以上）

2. USB输入（5.5V以上）

## 构建固件

要为此目标构建PX4：

```jsx
make thepeach_r1_default
```

## 购买地点

从[ThePeach](https://thepeach.shop/)订购
