# 串口映射

本主题展示如何确定 USART/UART 串口设备名称（例如"ttyS0"）与飞行控制器上相关端口（如 `TELEM1`、`TELEM2`、`GPS1`、`RC SBUS`、`Debug console`）之间的映射。

这些说明用于在飞行控制器文档中生成串口映射表。
例如：[Pixhawk 4 > 串口映射](../flight_controller/pixhawk4.md#serial-port-mapping)。

::: info
分配给每个端口的功能不一定要与名称匹配（在大多数情况下），并且使用[串口配置](../peripherals/serial_configuration.md)设置。
通常端口功能被配置为与名称匹配，这就是为什么标记为 `GPS1` 的端口可以开箱即用 GPS。
:::

## STMxxyyy 上的 NuttX

<!-- instructions from DavidS here: https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

本节展示如何通过检查板载配置文件获得 STMxxyyy 架构上 NuttX 构建的映射。
说明使用 FMUv5，但类似地可以扩展到其他 FMU 版本/NuttX 板载。

### default.px4board

**default.px4board** 列出了许多串口映射（搜索文本"SERIAL_PORTS"）。

来自 [/boards/px4/fmu-v5/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/default.px4board)：

```
CONFIG_BOARD_SERIAL_GPS1="/dev/ttyS0"
CONFIG_BOARD_SERIAL_TEL1="/dev/ttyS1"
CONFIG_BOARD_SERIAL_TEL2="/dev/ttyS2"
CONFIG_BOARD_SERIAL_TEL4="/dev/ttyS3"
```

或者，您可以使用 `make px4_fmu-v5 boardconfig` 启动 boardconfig 并访问串口菜单

```
    Serial ports  --->
        (/dev/ttyS0) GPS1 tty port
        ()  GPS2 tty port
        ()  GPS3 tty port
        ()  GPS4 tty port
        ()  GPS5 tty port
        (/dev/ttyS1) TEL1 tty port
        (/dev/ttyS2) TEL2 tty port
        ()  TEL3 tty port
        (/dev/ttyS3) TEL4 tty port
        ()  TEL5 tty port
```

### nsh/defconfig

_nsh/defconfig_ 允许您确定定义了哪些端口，它们是 UART 还是 USART，以及 USART/UART 与设备之间的映射。
您还可以确定哪个端口用于[串口/调试控制台](../debug/system_console.md)。

打开板载的 defconfig 文件，例如：[/boards/px4/fmu-v5/nuttx-config/nsh/defconfig](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/nuttx-config/nsh/defconfig#L215-L221)

搜索文本"ART"，直到找到格式为 `CONFIG_STM32xx_USARTn=y`（其中 `xx` 是处理器类型，`n` 是端口号）的条目部分。
例如：

```
CONFIG_STM32F7_UART4=y
CONFIG_STM32F7_UART7=y
CONFIG_STM32F7_UART8=y
CONFIG_STM32F7_USART1=y
CONFIG_STM32F7_USART2=y
CONFIG_STM32F7_USART3=y
CONFIG_STM32F7_USART6=y
```

这些条目告诉您定义了哪些端口，以及它们是 UART 还是 USART。

复制上面的部分并按"n"数字重新排序。
同时递增设备号 _ttyS**n**_（从零开始）以获得设备到串口的映射。

```
ttyS0 CONFIG_STM32F7_USART1=y
ttyS1 CONFIG_STM32F7_USART2=y
ttyS2 CONFIG_STM32F7_USART3=y
ttyS3 CONFIG_STM32F7_UART4=y
ttyS4 CONFIG_STM32F7_USART6=y
ttyS5 CONFIG_STM32F7_UART7=y
ttyS6 CONFIG_STM32F7_UART8=y
```

要获得 DEBUG 控制台映射，我们在 [defconfig 文件](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/nuttx-config/nsh/defconfig#L212)中搜索 `SERIAL_CONSOLE`。
下面我们看到控制台在 UART7 上：

```
CONFIG_UART7_SERIAL_CONSOLE=y
```

### board_config.h

对于有 IO 板载的飞行控制器，通过搜索 `PX4IO_SERIAL_DEVICE` 从 **board_config.h** 确定 PX4IO 连接。

例如，[/boards/px4/fmu-v5/src/board_config.h](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/src/board_config.h#L59)：

```
#define PX4IO_SERIAL_DEVICE            "/dev/ttyS6"
#define PX4IO_SERIAL_TX_GPIO           GPIO_UART8_TX
#define PX4IO_SERIAL_RX_GPIO           GPIO_UART8_RX
#define PX4IO_SERIAL_BASE              STM32_UART8_BASE
```

所以 PX4IO 在 `ttyS6` 上（我们也可以看到这映射到 UART8，我们在前面的部分已经知道了）。

### 汇总

最终映射是：

```
ttyS0 CONFIG_STM32F7_USART1=y GPS1
ttyS1 CONFIG_STM32F7_USART2=y TEL1
ttyS2 CONFIG_STM32F7_USART3=y TEL2
ttyS3 CONFIG_STM32F7_UART4=y TEL4
ttyS4 CONFIG_STM32F7_USART6=y
ttyS5 CONFIG_STM32F7_UART7=y DEBUG
ttyS6 CONFIG_STM32F7_UART8=y PX4IO
```

在[飞行控制器文档](../flight_controller/pixhawk4.md#serial-port-mapping)中，结果表是：

| UART   | Device     | Port                  |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | GPS                   |
| USART2 | /dev/ttyS1 | TELEM1 (flow control) |
| USART3 | /dev/ttyS2 | TELEM2 (flow control) |
| UART4  | /dev/ttyS3 | TELEM4                |
| USART6 | /dev/ttyS4 | RC SBUS               |
| UART7  | /dev/ttyS5 | Debug Console         |
| UART8  | /dev/ttyS6 | PX4IO                 |

## 其他架构

::: info
欢迎贡献！
:::

## 另请参阅

- [串口配置](../peripherals/serial_configuration.md)
- [MAVLink 遥测（OSD/GCS）](../peripherals/mavlink_peripherals.md)
