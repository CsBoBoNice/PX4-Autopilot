# Holybro Durandal

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://holybro.com/)获取硬件支持或合规问题。
:::

_Durandal_<sup>&reg;</sup>是Holybro飞行控制器成功系列的最新更新。
它由Holybro设计和开发。

![Durandal](../../assets/flight_controller/durandal/durandal_hero.jpg)

在高层次上，一些关键特性包括：

- 集成的传感器温度控制。
- 强大的STM32H7微控制器，运行在480MHz。
  2MB闪存和1MB内存。
- 具有更高温度稳定性的新传感器。
- 内部振动隔离系统。
- 板载双高性能、低噪音IMU，专为苛刻的稳定应用而设计。

关键特性的摘要、[组装](../assembly/quick_start_durandal.md)和[购买](#purchase)链接可在下面找到。

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 快速摘要

#### 技术规格

- 主FMU处理器：STM32H743
  - 32位Arm® Cortex®-M7，480MHz，2MB内存，1MB RAM
- IO处理器：STM32F100
  - 32位Arm® Cortex®-M3，24MHz，8KB SRAM
- 板载传感器
  - 加速度计/陀螺仪：ICM-20689
  - 加速度计/陀螺仪：BMI088或ICM20602
  - 磁力计：IST8310
  - 气压计：MS5611
- GPS：u-blox Neo-M8N GPS/GLONASS接收器；集成磁力计IST8310

#### 接口

- 8-13个PWM舵机输出（IO输出8个，FMU输出5个）
- FMU上6个专用PWM/捕获输入
- Spektrum/DSM专用R/C输入
- CPPM和S.Bus专用R/C输入
- 专用S.Bus舵机输出和模拟/PWM RSSI输入
- 5个通用串口
  - 3个带完整流控制
  - 1个带独立1.5A电流限制
- 3个I2C端口
- 4个SPI总线
  - 1个内部高速SPI传感器总线，带4个片选和6个DRDY
  - 1个内部低噪音SPI总线，专用于XXX
  - 气压计，带2个片选，无DRDY
  - 1个内部SPI总线，专用于FRAM
  - 支持位于传感器模块上的温度控制
  - 1个外部SPI总线
- 最多2个CANBus用于双CAN
  - 每个CANBus都有独立的静音控制或ESC RX-MUX控制
- 2个电池的电压/电流模拟输入
- 2个额外的模拟输入

#### 电气数据

- 电源模块输出：4.9~5.5V
- 最大输入电压：6V
- 最大电流检测：120A
- USB电源输入：4.75~5.25V
- 舵机轨输入：0~36V

#### 机械数据

- 尺寸：80x45x20.5mm
- 重量：68.8g

#### 其他特性

- 工作温度：~40~85°C
- 存储温度：-40~85°C
- CE
- FCC
- RoHS合规（无铅）

更多信息请参见：[Durandal技术数据表](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Durandal_technical_data_sheet_90f8875d-8035-4632-a936-a0d178062077.pdf)。

<a id="purchase"></a>

## 购买地点

从[Holybro](https://holybro.com/products/durandal)订购。

## 连接

端口/连接的位置如图所示（以及下面的[引脚图部分](#pinouts)）。

### 顶部

![Durandal - 顶部引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_top.jpg)

### 前部

![Durandal - 前部引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_front.jpg)

### 后部

![Durandal - 后部引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_back.jpg)

### 右侧

![Durandal - 右侧引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_right.jpg)

### 左侧

![Durandal - 左侧引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_left.jpg)

## 尺寸

所有尺寸均以毫米为单位。

![Durandal尺寸](../../assets/flight_controller/durandal/durandal_dimensions.jpg)

<!--
## 电压额定值

*Pixhawk 4*如果提供三个电源，可以实现电源三重冗余。三个电源轨是：**POWER1**、**POWER2**和**USB**。

::: info
输出电源轨**FMU PWM OUT**和**I/O PWM OUT**（0V到36V）不为飞行控制器板供电（也不由其供电）。
您必须向**POWER1**、**POWER2**或**USB**中的一个供电，否则板子将无电源。
:::

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：
1. **POWER1**和**POWER2**输入（4.9V到5.5V）
1. **USB**输入（4.75V到5.25V）
-->

<!--
**绝对最大额定值**

在这些条件下，系统将不消耗任何电力（将不可操作），但将保持完整。
1. **POWER1**和**POWER2**输入（操作范围4.1V到5.7V，0V到10V不受损）
1. **USB**输入（操作范围4.1V到5.7V，0V到6V不受损）
1. 舵机输入：**FMU PWM OUT**和**I/O PWM OUT**的VDD_SERVO引脚（0V到42V不受损）

-->

## 组装/设置

[Durandal接线快速入门](../assembly/quick_start_durandal.md)提供了如何组装所需/重要外设（包括GPS、电源管理板等）的说明。

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make holybro_durandal-v1_default
```

## 串口映射

| UART   | 设备       | 端口          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS1          |
| USART2 | /dev/ttyS1 | TELEM1        |
| USART3 | /dev/ttyS2 | TELEM2        |
| UART4  | /dev/ttyS3 | TELEM4/GPS2   |
| USART6 | /dev/ttyS4 | TELEM3        |
| UART7  | /dev/ttyS5 | 调试控制台     |
| UART8  | /dev/ttyS6 | PX4IO         |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 调试端口 {#debug_port}

[PX4系统控制台](../debug/system_console.md)和[SWD接口](../debug/swd_debug.md)在_调试端口_上运行。

引脚排列和连接器符合[Pixhawk连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)中定义的[Pixhawk调试迷你](../debug/swd_debug.md#pixhawk-debug-mini)接口。

有关接线和调试信息，请参见上述链接。

::: info
I/O板没有暴露调试端口。
:::

## 外设

- [数字空速传感器](https://store-drotek.com/793-digital-differential-airspeed-sensor-kit-.html)
- [遥测无线电模块](../telemetry/index.md)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通RC舵机或Futaba S-Bus舵机控制的多旋翼/飞机/漫游车或船只。

完整的支持配置集可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 引脚图

_Durandal_引脚图如下所示。
这些也可以从[这里](https://cdn.shopifycdn.net/s/files/1/0604/5905/7341/files/Durandal_Pinouts_v1.0.pdf?v=1693983344)下载。

### 顶部引脚图

![Durandal - 顶部引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_top.jpg)

### 前部引脚图

![Durandal - 前部引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_front.jpg)

#### SBUS输出端口

| 引脚       | 信号             | 电压  |
| ---------- | ---------------- | ----- |
| 1（红色）  | -                | -     |
| 2（黄色）  | SBUS_OUT/RSSI_IN | +3.3V |
| 3（黑色）  | GND              | GND   |

#### DSM RC端口

| 引脚       | 信号    | 电压  |
| ---------- | ------- | ----- |
| 1（红色）  | VDD_3V3 | +3.3V |
| 2（黄色）  | DSM_IN  | +3.3V |
| 3（黑色）  | GND     | GND   |

#### I2C A端口

| 引脚      | 信号 | 电压  |
| --------- | ---- | ----- |
| 1（红色） | VCC  | +5V   |
| 2（黑色） | SCL4 | +3.3V |
| 3（黑色） | SDA4 | +3.3V |
| 4（黑色） | GND  | GND   |

#### CAN1端口

| 引脚      | 信号  | 电压  |
| --------- | ----- | ----- |
| 1（红色） | VCC   | +5V   |
| 2（黑色） | CAN H | +3.3V |
| 3（黑色） | CAN L | +3.3V |
| 4（黑色） | GND   | GND   |

<a id="gps"></a>

#### GPS端口

| 引脚       | 信号              | 电压  |
| ---------- | ----------------- | ----- |
| 1（红色）  | VCC               | +5V   |
| 2（黑色）  | TX（输出）        | +3.3V |
| 3（黑色）  | RX（输入）        | +3.3V |
| 4（黑色）  | SCL1              | +3.3V |
| 5（黑色）  | SDA1              | +3.3V |
| 6（黑色）  | SAFETY_SWITCH     | +3.3V |
| 7（黑色）  | SAFETY_SWITCH_LED | +3.3V |
| 8（黑色）  | VDD_3V3           | +3.3V |
| 9（黑色）  | BUZZER            | +5V   |
| 10（黑色） | GND               | GND   |

<a id="telem4_i2cb"></a>

#### TELEM4 I2CB端口

| 引脚      | 信号     | 电压  |
| --------- | -------- | ----- |
| 1（红色） | VCC      | +5V   |
| 2（黑色） | TX（输出）| +3.3V |
| 3（黑色） | RX（输入）| -     |
| 4（黑色） | SCL2     | -     |
| 5（黑色） | SDA2     | +3.3V |
| 6（黑色） | GND      | GND   |

<a id="telem1_2_3"></a>

#### TELEM3、TELEM2、TELEM1端口

| 引脚      | 信号      | 电压  |
| --------- | --------- | ----- |
| 1（红色） | VCC       | +5V   |
| 2（黑色） | TX（输出）| +3.3V |
| 3（黑色） | RX（输入）| +3.3V |
| 4（黑色） | CTS（输入）| +3.3V |
| 5（黑色） | RTS（输出）| +3.3V |
| 6（黑色） | GND       | GND   |

<a id="power"></a>

#### POWER端口

| 引脚      | 信号    | 电压  |
| --------- | ------- | ----- |
| 1（红色） | VCC     | +5V   |
| 2（黑色） | VCC     | +5V   |
| 3（黑色） | CURRENT | +3.3V |
| 4（黑色） | VOLTAGE | +3.3V |
| 5（黑色） | GND     | GND   |
| 6（黑色） | GND     | GND   |

### 后部引脚图

![Durandal - 后部引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_back.jpg)

#### MAIN输出

| 引脚 | 信号   | 电压  | +         | -   |
| ---- | ------ | ----- | --------- | --- |
| 1    | IO_CH1 | +3.3V | VDD_SERVO | GND |
| 2    | IO_CH2 | +3.3V | VDD_SERVO | GND |
| 3    | IO_CH3 | +3.3V | VDD_SERVO | GND |
| 4    | IO_CH4 | +3.3V | VDD_SERVO | GND |
| 5    | IO_CH5 | +3.3V | VDD_SERVO | GND |
| 6    | IO_CH6 | +3.3V | VDD_SERVO | GND |
| 7    | IO_CH7 | +3.3V | VDD_SERVO | GND |
| 8    | IO_CH8 | +3.3V | VDD_SERVO | GND |

#### AUX输出

| 引脚 | 信号    | 电压  | +         | -   |
| ---- | ------- | ----- | --------- | --- |
| 1    | FMU_CH1 | +3.3V | VDD_SERVO | GND |
| 2    | FMU_CH2 | +3.3V | VDD_SERVO | GND |
| 3    | FMU_CH3 | +3.3V | VDD_SERVO | GND |
| 4    | FMU_CH4 | +3.3V | VDD_SERVO | GND |
| 5    | FMU_CH5 | +3.3V | VDD_SERVO | GND |

#### RC输入

| 引脚 | 信号           | 电压  |
| ---- | -------------- | ----- |
| S    | SBUS_IN/PPM_IN | +3.3V |
| +    | VCC            | +5V   |
| -    | GND            | GND   |

### 右侧引脚图

![Durandal - 右侧引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_right.jpg)

#### CAN2端口

| 引脚      | 信号  | 电压  |
| --------- | ----- | ----- |
| 1（红色） | VCC   | +5V   |
| 2（黑色） | CAN H | +3.3V |
| 3（黑色） | CAN L | +3.3V |
| 4（黑色） | GND   | GND   |

#### CAP & ADC输入端口

| 引脚       | 信号         | 电压                     |
| ---------- | ------------ | ------------------------ |
| 1（红色）  | VCC          | +5V                      |
| 2（黑色）  | FMU_CAP6     | +3.3V                    |
| 3（黑色）  | FMU_CAP5     | +3.3V                    |
| 4（黑色）  | FMU_CAP4     | +3.3V                    |
| 5（黑色）  | FMU_CAP3     | +3.3V                    |
| 6（黑色）  | FMU_CAP2     | +3.3V                    |
| 7（黑色）  | FMU_CAP1     | +3.3V                    |
| 8（黑色）  | ADC1_SPARE_1 | +3.3V [++](#warn_sensor) |
| 9（黑色）  | ADC1_SPARE_2 | +6.6V [++](#warn_sensor) |
| 10（黑色） | GND          | GND                      |

<a id="warn_sensor"></a>

:::warning
++ 连接到引脚8、9的传感器发送的信号不得超过指示电压。
:::

### 左侧引脚图

![Durandal - 左侧引脚图（原理图）](../../assets/flight_controller/durandal/durandal_pinouts_left.jpg)

<a id="debug_port"></a>

#### DEBUG端口

| 引脚      | 信号  | 电压  |
| --------- | ----- | ----- |
| 1（红色） | VT    | +3.3V |
| 2（黑色） | TX    | +3.3V |
| 3（黑色） | RX    | +3.3V |
| 4（黑色） | SWDIO | +3.3V |
| 5（黑色） | SWCLK | +3.3V |
| 6（黑色） | GND   | GND   |

#### SPI端口

| 引脚      | 信号 | 电压  |
| --------- | ---- | ----- |
| 1（红色） | VCC  | +5V   |
| 2（黑色） | SCK  | +3.3V |
| 3（黑色） | MISO | +3.3V |
| 4（黑色） | MOSI | +3.3V |
| 5（黑色） | CS1  | +3.3V |
| 6（黑色） | CS2  | +3.3V |
| 7（黑色） | GND  | GND   |

#### USB端口

| 引脚      | 信号 | 电压  |
| --------- | ---- | ----- |
| 1（红色） | VBUS | +5V   |
| 2（黑色） | DM   | +3.3V |
| 3（黑色） | DP   | +3.3V |
| 4（黑色） | GND  | GND   |

## 更多信息

- [Durandal接线快速入门](../assembly/quick_start_durandal.md)
- [Durandal技术数据表](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Durandal_technical_data_sheet_90f8875d-8035-4632-a936-a0d178062077.pdf)
- [Durandal引脚图](https://cdn.shopifycdn.net/s/files/1/0604/5905/7341/files/Durandal_Pinouts_v1.0.pdf?v=1693983344)（Holybro）
