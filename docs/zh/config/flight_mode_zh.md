# 飞行模式配置

本主题解释如何将[飞行模式](../getting_started/px4_basic_concepts.md#flight-modes)和其他功能映射到您无线电控制发射器的开关。

:::tip
为了设置飞行模式，您必须已经：
- [配置您的无线电](../config/radio.md)
- [设置您的发射器](#rc-transmitter-setup)以将模式开关的物理位置编码到单个通道中。
  我们在[下面](#taranis-setup-3-way-switch-configuration-for-single-channel-mode)为流行的*Taranis*发射器提供示例（如果您使用不同的发射器，请查看您的文档）。
:::


## 我应该设置哪些飞行模式和开关？

飞行模式提供不同类型的*自动驾驶辅助飞行*和*完全自主飞行*。
您可以设置[飞行器可用](../flight_modes/index.md#flight-modes)的任何（或无）飞行模式。

大多数用户应该设置以下模式和功能，因为这些使飞行器更容易和更安全地飞行：

- **位置模式** — 手动飞行的最简单和最安全模式。
- **返回模式** — 通过安全路径返回起飞位置并着陆。
- （仅VTOL）**VTOL过渡开关** — 在VTOL飞行器上在固定翼和多旋翼飞行配置之间切换。

通常也将开关映射到：

- **任务模式** — 此模式运行地面控制站发送的预编程任务。
- <a id="kill_switch"></a> [杀死开关](../config/safety.md#kill-switch) - 立即停止所有电机输出（飞行器将坠毁，在某些情况下这可能比允许其继续飞行更可取）。

## 飞行模式选择

PX4允许您指定一个"模式"通道并选择最多6个飞行模式，这些模式将根据通道的PWM值激活。
您还可以单独指定用于映射杀死开关、返回起飞模式和离线模式的通道。

配置单通道飞行模式选择：

1. 启动*QGroundControl*并连接飞行器。
1. 打开您的RC发射器。
1. 选择**"Q"图标 > 飞行器设置 > 飞行模式**（侧边栏）打开_飞行模式设置_。

   ![飞行模式单通道](../../assets/qgc/setup/flight_modes/flight_modes_single_channel.jpg)

1. 指定*飞行模式设置*：
   * 选择**模式通道**（上面显示为通道5，但这将取决于您的发射器配置）。
   * 移动您为模式选择设置的发射器开关（或开关）到可用位置。
     与您当前开关位置匹配的模式槽将被突出显示（上面是*飞行模式1*）。
     ::: info
     虽然您可以在任何6个槽中设置飞行模式，但只有映射到开关位置的通道才会被突出显示/使用。
     :::
   * 选择您希望为每个开关位置触发的飞行模式。
1. 指定*开关设置*：
   * 选择您想要映射到特定操作的通道 - 例如：*返回*模式、*杀死开关*、*离线*模式等（如果您的发射器上有备用开关和通道）。

1. 测试模式是否映射到正确的发射器开关：
   * 检查*通道监视器*以确认预期通道被每个开关改变。
   * 依次选择发射器上的每个模式开关，并检查所需的飞行模式是否被激活（*QGroundControl*上活动模式的文本变为黄色）。

所有值在更改时自动保存。

## RC发射器设置

本节包含taranis的少量可能设置配置。
QGroundControl _可能_在[这里有其他发射器的设置信息](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/flight_modes.html#transmitter-setup)。


<a id="taranis_setup"></a>

### Taranis设置：单通道模式的3位开关配置

如果您只需要支持在两个或三个模式之间选择，那么您可以将模式映射到单个3位开关的位置。
下面我们展示如何将Taranis 3位"SD"开关映射到通道5。

::: info
此示例显示如何设置流行的*FrSky Taranis*发射器。
其他发射器的发射器设置会有所不同。
:::

打开Taranis UI **MIXER**页面并向下滚动到**CH5**，如下所示：

![Taranis - 将通道映射到开关](../../assets/qgc/setup/flight_modes/single_channel_mode_selection_1.png)

按**ENT(ER)**编辑**CH5**配置，然后将**Source**更改为*SD*按钮。

![Taranis - 配置通道](../../assets/qgc/setup/flight_modes/single_channel_mode_selection_2.png)

就是这样！
通道5现在将为三个不同的**SD**开关位置输出3个不同的PWM值。

然后*QGroundControl*配置如前一节所述。


### Taranis设置：单通道模式的多开关配置

大多数发射器没有6位开关，因此如果您需要能够支持比可用开关位置数量更多的模式（最多6个），那么您必须使用多个开关来表示它们。
通常这是通过将2位和3位开关的位置编码到单个通道中来完成的，因此每个开关位置导致不同的PWM值。

在FrSky Taranis上，此过程涉及为两个真实开关的每个位置组合分配一个"逻辑开关"。
然后每个逻辑开关在同一通道上分配给不同的PWM值。

下面的视频显示了如何使用*FrSky Taranis*发射器完成此操作。

<!-- [youtube](https://youtu.be/scqO7vbH2jo) Video has gone private and is no longer available -->
<!-- @[youtube](https://youtu.be/BNzeVGD8IZI?t=427) - video showing how to set the QGC side - at about 7mins and 3 secs -->

<lite-youtube videoid="TFEjEQZqdVA" title="Taranis模式开关"/>

然后*QGroundControl*配置如[上面描述](#flight-mode-selection)。


## 更多信息

* [飞行模式概述](../flight_modes/index.md)
* [QGroundControl > 飞行模式](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/flight_modes.html#px4-pro-flight-mode-setup)
* [PX4设置视频 - @6m53s](https://youtu.be/91VGmdSlbo4?t=6m53s) (Youtube)
* [无线电开关参数](../advanced_config/parameter_reference.md#radio-switches) - 可用于通过参数设置映射
