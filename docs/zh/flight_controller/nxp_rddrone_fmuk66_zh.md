# NXP RDDRONE-FMUK66 FMU（已停产）

<Badge type="info" text="已停产" />

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://www.nxp.com/)获取硬件支持或合规问题。
:::

RDDRONE-FMUK66 FMU是使用NXP半导体组件的参考设计，严格遵循Pixhawk FMUv4规范，同时增加了双线汽车以太网100BASET1和安全元件A71CH（RevC）或SE050（RevD）。
NXP提供原理图、Gerber文件、BOM和源文件，任何人都可以复制、更改或重新设计此设计。

这是与[HoverGames](https://www.hovergames.com/)一起使用的官方FMU。

![RDDRONE-FMUK66 FMU主图1](../../assets/flight_controller/nxp_rddrone_fmuk66/HoverGamesDrone_14042019_XL_020.jpg)

![RDDRONE-FMUK66 FMU主图2](../../assets/flight_controller/nxp_rddrone_fmuk66/HoverGamesDrone_14042019_XL_021.jpg)

NXP FMU和包含的外设已经过测试，符合FCC/CE/RoHs/REACH指令。

::: info
这些飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 快速摘要

- **主FMU处理器：**
  - Kinetis K66 MK66FN2MOVLQ18微控制器，运行在180MHz Cortex-M4F MCU，2MB闪存，256KB SRAM，双USB（FS + HS），以太网，144-LQFP。
- **板载传感器：**
  - 加速度计/陀螺仪：BMI088/ICM42688（RevD）...
  - 加速度计/磁力计：FXOS8700CQ
  - 陀螺仪：FXAS21002CQ
  - 磁力计：BMM150
  - 气压计：ML3115A2
  - 气压计：BMP280
- **GPS：**
  - u-blox Neo-M8N GPS/GLONASS接收器；集成磁力计IST8310

此FMU仅以套件形式提供，包括[Segger Jlink EDU mini调试器](https://www.segger.com/products/debug-probes/j-link/models/j-link-edu-mini/)、DCD-LZ调试器适配器、USB-TTL-3V3控制台线缆、HolyBro GPS模块、电池电源模块、SD卡和外壳、螺丝和贴纸。
遥测无线电（[HGD-TELEM433](https://www.nxp.com/part/HGD-TELEM433)和[HGD-TELEM915](https://www.nxp.com/part/HGD-TELEM915)）必须单独购买，以匹配您所在国家使用的ISM频段。

![RDDRONE-FMUK66 FMU套件](../../assets/flight_controller/nxp_rddrone_fmuk66/rddrone_fmu66_kit_img_contents.jpg)

还提供"精简"版本RDDRONE-FMUK66L，不包括电源模块、GPS、Jlink或USB-TTL-3V3控制台线缆或SD卡。[向下滚动查看FMUK66购买页面购买部分中的FMUK66L](https://www.nxp.com/design/design-center/development-boards-and-designs/px4-robotic-drone-vehicle-flight-management-unit-vmu-fmu-rddrone-fmuk66:RDDRONE-FMUK66#buy)

其他信息可以在[技术数据表](https://www.nxp.com/design/design-center/development-boards-and-designs/px4-robotic-drone-vehicle-flight-management-unit-vmu-fmu-rddrone-fmuk66:RDDRONE-FMUK66)中找到。<!-- www.nxp.com/rddrone-fmuk66 -->

## 购买地点

**RDDRONE-FMUK66**参考设计套件可直接从NXP或NXP授权的全球[电子分销商网络](https://www.nxp.com/support/sample-and-buy/distributor-network:DISTRIBUTORS)购买。

- [购买链接](https://www.nxp.com/design/design-center/development-boards-and-designs/px4-robotic-drone-vehicle-flight-management-unit-vmu-fmu-rddrone-fmuk66:RDDRONE-FMUK66#buy)（www.nxp.com）
- 遥测无线电根据频段单独购买：
  - [HGD-TELEM433](https://www.nxp.com/part/HGD-TELEM433)
  - [HGD-TELEM915](https://www.nxp.com/part/HGD-TELEM915)

::: info
_RDDRONE-FMUK66_ FMU也包含在完整的HoverGames无人机套件中：[KIT-HGDRONEK66](https://www.nxp.com/design/design-center/development-boards-and-designs/nxp-hovergames-drone-kit-including-flight-controller-and-peripherals:KIT-HGDRONEK66#buy)
:::

<!--
## 连接器

[连接器图]

## 引脚图

[引脚图列表或链接]

## 尺寸

[尺寸]

-->

## 组装/设置

https://nxp.gitbook.io/hovergames

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make nxp_fmuk66-v3_default
```

## 调试端口

[PX4系统控制台](../debug/system_console.md)和[SWD接口](../debug/swd_debug.md)在[DCD-LZ FMU调试](https://nxp.gitbook.io/hovergames/rddrone-fmuk66/connectors/debug-interface-dcd-lz)端口上运行。

NXP的DCD-LZ是一个7引脚JST-GH连接器，在[Pixhawk 6引脚标准调试端口](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)的基础上增加了nRST/MCU_RESET引脚。

DCD-LZ分线适配器允许使用标准10引脚JTAG/SWD接口（即使用Segger Jlink）和标准5引脚FTDI USB-TTL-3V3类型线缆。

<!--

## 外设

* [人们应该与此硬件一起使用的任何东西的列表]

-->

## 支持的平台/机架

任何可以用普通RC舵机或Futaba S-Bus舵机控制的多旋翼/飞机/漫游车或船只。
完整的支持配置集可以在[机架参考](../airframes/airframe_reference.md)中看到。

![HoverGames无人机套件](../../assets/flight_controller/nxp_rddrone_fmuk66/hovergames_drone_14042019_xl001.jpg)

:::tip
NXP [HoverGames无人机套件](https://www.nxp.com/kit-hgdronek66)（如上所示）是一个完整的无人机开发套件，包括构建四轴飞行器所需的一切。
您只需要提供3S/4S LiPo电池。
:::

## 更多信息

- [HoverGames在线文档](https://nxp.gitbook.io/hovergames) PX4用户和编程指南，具体组装、构造、调试、编程说明。

- 支持HoverGames和RDDRONE-FMUK66的3D模型可以在_Thingiverse_的这些搜索链接中找到：[fmuk66](https://www.thingiverse.com/search?q=fmuk66&type=things&sort=relevant)，[hovergames](https://www.thingiverse.com/search?q=hovergames&type=things&sort=relevant)。

![HoverGamesDronelogo](../../assets/flight_controller/nxp_rddrone_fmuk66/hovergames_colored_small.png)
