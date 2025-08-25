# MindRacer硬件

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](http://mindpx.net)获取硬件支持或合规问题。
:::

AirMind<sup>&reg;</sup> [MindRacer](http://mindpx.net)系列是微型无人机的完全可堆叠飞行_平台_。
该平台目前有两个RTF飞行器：[MindRacer 210](../complete_vehicles_mc/mindracer210.md)和[NanoMind 110](../complete_vehicles_mc/nanomind110.md)。

![MindRacer](../../assets/hardware/hardware-mindracer.png)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 快速摘要

MindRacer是微型无人机的完全可堆叠飞行平台。
基于[MindPX](../flight_controller/mindpx.md)，_MindRacer_进一步缩小了外形尺寸，同时专注于提供模块化。
MindRacer是一个_平台_而不是飞行控制器。

MindRacer实现了SEP（消除焊接端口）和WEP（消除接线协议）概念。
在SEP和WEP之前，焊接和接线一直是无人机制造和调试过程中的主要痛点和效率杀手。

::: info
主要的硬件文档在[这里](http://mindpx.net/assets/accessories/mindracer_spec_v1.2.pdf)。
:::

- 超小尺寸，重量约6g
- 高性能STM32F427 168MHz浮点处理器，超快油门响应
- 支持OneShot ESC
- 支持PPM/SBUS/DSM无线电接收器，支持D.Port/S.Port/Wifi遥测
- 板载飞行数据记录器
- 支持IMU隔离
- DroneCode<sup>&reg;</sup>标准兼容连接器

|              项目              |                       描述                        |
| :----------------------------: | :-----------------------------------------------: |
|        飞行控制器/处理器        |                     F427VIT6                     |
|              重量              |                       约6g                       |
|              尺寸              |                     35x35mm                      |
|            PWM输出             |                      最多6个                     |
|              IMU               |                      10DOF                       |
|            IMU隔离             |                   是/可选                        |
|            无线电接收器         |          S.BUS/PPM/DSM/DSM2/DSMX/SUMD           |
|             遥测               | FrSky<sup>&reg;</sup> D.Port, S.Port, Wifi, 3DR无线电 |
| 板载TF卡用于飞行数据记录       |                        是                         |
|         OneShot ESC支持        |                        是                         |
|            扩展插槽            |                   2x7(pin)x2                     |
|         板载实时时钟           |                        是                         |
|             连接器             |    JST GH（符合DroneCode标准）                    |

## 快速入门

### 引脚图

![Mindracer引脚图](../../assets/hardware/hardware-mindracer-pinout.png)

### 如何构建

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make airmind_mindpx-v2_default
```

### 伴随PC连接

MindRacer有一个附加的Adapt IO板。

![附加的Adapt IO板](../../assets/hardware/hardware-mindracer-conn.png)

MindRacer有一个内置的UART转USB转换器。
要连接伴随计算机，将MindRacer堆叠在接口板上，并将伴随计算机连接到接口板上的USB端口。

最大波特率与px4系列相同，最高可达921600。

### 用户指南

::: info
用户指南在[这里](http://mindpx.net/assets/accessories/mindracer_user_guide_v1.2.pdf)
:::

## 购买地点

MindRacer可在[AirMind商店](https://airmind.mindpx.net/catalog)购买。
您也可以在Amazon<sup>&reg;</sup>或eBay<sup>&reg;</sup>上找到MindRacer。

## 支持

请访问http://www.mindpx.org获取更多信息。
或者您可以发送电子邮件至[support@mindpx.net](mailto::support@mindpx.net)进行任何咨询或寻求帮助。
