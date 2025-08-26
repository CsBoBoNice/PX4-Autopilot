# ModalAI Starling (PX4 自主开发套件)

[Starlings](https://www.modalai.com/pages/starlings) 是由 [VOXL 2](../flight_controller/modalai_voxl_2.md) 和 PX4 增强的 SLAM 开发无人机，配备了针对室内和室外自主导航优化的 SWAP 传感器和载荷。
由 Blue UAS Framework 自动驾驶仪、VOXL 2 驱动，Starling 重量仅 275g，拥有令人印象深刻的 30 分钟自主室内飞行时间。

![概述](../../assets/hardware/complete_vehicles/modalai_starling/starling_front_hero.jpg)

ModalAI PX4 自主开发套件是基于 Starling 的开发无人机。
它包含一个 [VOXL 2](../flight_controller/modalai_voxl_2.md)，这是一个功能强大的伴随计算机和 PX4 飞控二合一小型封装，还包括图像传感器、GPS 和连接调制解调器，开箱即飞。
Starling 配备了 ModalAI 的 [开放 SDK](https://docs.modalai.com/voxl-developer-bootcamp/)，该 SDK 具有用于计算机视觉辅助飞行的预配置自主模型。
这款开发无人机旨在帮助您更快地推向市场并加速您的应用程序开发和原型制作。

本指南解释了使无人机准备飞行所需的最少额外设置。
它还涵盖硬件概述、首次飞行、设置 WiFi 等内容。

::: info
有关完整和定期更新的文档，请访问 <https://docs.modalai.com/starling-v2>。
:::

::: info
如果您是 VOXL 的新手，请务必通过查看 [VOXL Bootcamp](https://docs.modalai.com/voxl-developer-bootcamp/) 来熟悉 VOXL 硬件和软件的核心功能。
:::

## 购买渠道

[ModalAI PX4 自主开发套件](https://www.modalai.com/products/px4-autonomy-developer-kit?variant=46969885950256)

## 硬件概述

![硬件概述](../../assets/hardware/complete_vehicles/modalai_starling/mrb_d0005_4_v2_c6_m22__callouts_a.jpg)

| 标注 | 描述                           | 型号              |
| ------- | ------------------------------------- | ---------------- |
| A       | VOXL 2                                | MDK-M0054-1      |
| B       | VOXL 四合一 ESC                       | MDK-M0117-1      |
| C       | 气压计保护帽                  | M10000533        |
| D       | ToF 图像传感器 (PMD)                | MDK-M0040        |
| E       | 跟踪图像传感器 (OV7251)        | M0014            |
| F       | 高分辨率图像传感器 (IMX214)           | M0025-2          |
| G       | AC600 WiFi 适配器                     | AWUS036EACS      |
| H       | GNSS GPS 模块和指南针             | M10-5883         |
| I       | 915MHz ELRS 接收机                  | BetaFPV Nano RX  |
| J       | VOXL 2 上的 USB C 连接器（未显示） |                  |
| K       | VOXL 电源模块                     | MCCA-M0041-5-B-T |
| L       | 4726FM 螺旋桨                      | M10000302        |
| M       | 1504 电机                            |                  |
| N       | XT30 电源连接器                  |                  |

## 规格书

### 规格参数

| 组件       | 规格参数                                                     |
| --------------- | ----------------------------------------------------------------- |
| 自动驾驶仪       | VOXL2                                                             |
| 起飞重量 | 275g（不含电池 172g）                                       |
| 对角尺寸   | 211mm                                                             |
| 飞行时间     | >30 分钟                                                       |
| 电机          | 1504                                                              |
| 螺旋桨      | 120mm                                                             |
| 机架           | 3mm 碳纤维                                                  |
| ESC             | ModalAI VOXL 四合一 ESC V2                                        |
| GPS             | UBlox M10                                                         |
| 遥控接收机     | 915mhz ELRS                                                       |
| 电源模块    | ModalAI 电源模块 v3 - 5V/6A                                   |
| 电池         | Sony VTC6 3000mah 2S，或任何带 XT30 连接器的 2S 18650 电池 |
| 高度          | 83mm                                                              |
| 宽度           | 187mm（折叠螺旋桨）                                              |
| 长度          | 142mm（折叠螺旋桨）                                              |

### 硬件接线图

![硬件概述](../../assets/hardware/complete_vehicles/modalai_starling/d0005_compute_wiring_d.jpg)

## 教程

### ELRS 设置

将您的 ELRS (ExpressLRS) 接收机绑定到发射机是准备您的基于 VOXL 2 的 ModalAI PX4 自主开发套件进行飞行的关键步骤。
此过程确保您的无人机与其控制系统之间的安全和响应连接。

按照本指南将您的 ELRS 接收机绑定到您的发射机。

#### 设置接收机

1. **启动接收机**：一旦您的无人机通电，您会注意到 ELRS 接收机的蓝色 LED 闪烁。
   这表示接收机已开启但尚未与发射机建立连接。

   ![Starling 接收机](../../assets/hardware/complete_vehicles/modalai_starling/starling-photo.png)

2. **进入绑定模式**：要启动绑定，打开终端并执行 `adb shell` 和 `voxl-elrs -bind` 命令。
   您会观察到接收机的 LED 切换到心跳模式闪烁，表示它现在处于绑定模式。

   ![启动截图](../../assets/hardware/complete_vehicles/modalai_starling/screenshot-boot.png)

#### 设置发射机

1. **访问菜单**：在套件中包含的 Commando 8 无线电发射机上，按左模式按钮打开菜单系统。

   ![在遥控器上按菜单](../../assets/hardware/complete_vehicles/modalai_starling/radio-1.png)

2. **导航到 ExpressLRS**：使用右按钮选择第一个菜单条目，应该是"ExpressLRS"。
3. **找到绑定选项**：选中"ExpressLRS"选项后，向下滚动到菜单底部找到"Bind"部分。可以通过向下按右按钮直到到达"Bind"选项来完成。

   ![在遥控器上按绑定](../../assets/hardware/complete_vehicles/modalai_starling/radio-2.png)

4. **启动绑定**：选择"Bind"将发射机置于绑定模式。当发射机发出蜂鸣声时，您就知道过程成功了，表示绑定成功。

#### 完成绑定过程

一旦发射机设置为绑定模式，无人机上的 ELRS 接收机将其 LED 从闪烁变为常亮，表示接收机和发射机之间的连接成功。

- **电源循环**：绑定过程完成后，在尝试飞行之前对 VOXL 2 进行电源循环是必要的。
  这意味着关闭 VOXL 2 然后重新打开。
  此步骤确保所有设置都正确应用，并且系统识别新建立的连接。

您现在应该已成功将 ELRS 接收机绑定到您的发射机，准备与 ModalAI 的 PX4 自主套件一起使用。
安全连接对于无人机的可靠运行至关重要，因此在飞行前务必确认绑定状态。

### 视频

- [VOXL 2 Starling 硬件概述](https://youtu.be/M9OiMpbEYOg)
- [VOXL 2 Starling 首次飞行教程](https://youtu.be/Cpbbye3Z6co)
- [VOXL 2 Starling ELRS 设置](https://youtu.be/7OwGS-kcFVg)

<!--  @katzfey - ModalAI reviewer -->
