# 电池估算调节（电源设置）

本主题解释如何配置电源设置，以便PX4可以估算可用的电池容量。

::: info
这些说明要求飞行器具有[电源模块（PM）](../power_module/index.md)或其他可以测量电池电压和（可选）电流的硬件。
:::

::: tip
[智能/MAVLink电池](../smart_batteries/index.md)不需要此调节：这些电池可以提供剩余电量的可靠指示。
:::

## 概述

电池估算调节使用测量的电压和电流（如果可用）来估算剩余电池容量。
这很重要，因为它允许PX4在飞行器接近耗尽电力并坠毁时采取行动（并且还可以防止由于深度放电而造成的电池损坏）。

PX4提供了许多（逐渐更有效的）方法可用于估算容量：

1. [基本电池设置](#basic_settings)（默认）：将原始测量电压与"空"和"满"电压之间的范围进行比较。
   这会导致粗略的估算，因为测量电压（及其对应的容量）会在负载下波动。
2. [带负载补偿的基于电压的估算](#load_compensation)：抵消负载对容量计算的影响。
3. [基于电压估算与电流积分融合](#current_integration)：将可用容量的负载补偿电压估算与已消耗电量的电流估算融合。
   这产生了与智能电池相当的容量估算。

后面的方法建立在前面的方法之上。
您使用的方法取决于飞行器的电源模块是否可以测量电流。

::: info
以下说明涉及电池1校准参数：`BAT1_*`。
其他电池使用`BATx_*`参数，其中`x`是电池编号。
所有电池校准参数[在此列出](../advanced_config/parameter_reference.md#battery-calibration)。
:::

:::tip
除了这里讨论的PX4配置外，您应该确保ESC的低电压切断要么被禁用，要么设置在预期最小电压以下。
这确保电池故障安全行为由PX4管理，并且ESC不会在电池仍有电量时切断（根据您选择的"空电池"设置）。
:::

:::tip
[电池化学概述](../power_systems/battery_chemistry.md)解释了主要电池类型之间的差异，以及这如何影响电池设置。
:::

## 基本电池设置（默认） {#basic_settings}

基本电池设置配置PX4使用默认方法进行容量估算。
此方法将测量的原始电池电压与"空"和"满"电芯的电芯电压范围进行比较（按电芯数量缩放）。

::: info
由于测量电压在负载下变化时估算电量的波动，此方法导致相对粗略的估算。
:::

为电池1配置基本设置：

1. 启动_QGroundControl_并连接飞行器。
2. 选择**"Q"图标 > 飞行器设置 > 电源**（侧边栏）打开_电源设置_。

您会看到表征电池的基本设置。
以下部分解释每个字段要设置的值。

![QGC电源设置](../../assets/qgc/setup/power/qgc_setup_power_px4.png)

::: info
在撰写时，_QGroundControl_只允许您在此视图中设置电池1的值。
对于具有多个电池的飞行器，您需要直接[设置参数](../advanced_config/parameters.md)电池2（`BAT2_*`），如以下部分所述。
:::

### 电芯数量（串联）

这设置电池中串联连接的电芯数量。
通常这会写在电池上，作为一个数字后跟"S"（例如"3S"、"5S"）。

::: info
单个原电池电芯的电压取决于[电池类型的化学特性](../power_systems/battery_chemistry.md)。
锂聚合物（LiPo）电池和锂离子电池都具有相同的_标称_电芯电压3.7V。
为了获得更高的电压（这将更有效地为飞行器供电），多个电芯_串联_连接。
端子处的电池电压然后是电芯电压的倍数。
:::

如果未提供电芯数量，您可以通过将电池电压除以单个电芯的标称电压来计算。
下表显示了这些电池的电压到电芯关系：

| 电芯 | LiPo (V) | LiIon (V) |
| ---- | -------- | --------- |
| 1S   | 3.7      | 3.7       |
| 2S   | 7.4      | 7.4       |
| 3S   | 11.1     | 11.1      |
| 4S   | 14.8     | 14.8      |
| 5S   | 18.5     | 18.5      |
| 6S   | 22.2     | 22.2      |

::: info
此设置对应[参数](../advanced_config/parameters.md)：[BAT1_N_CELLS](../advanced_config/parameter_reference.md#BAT1_N_CELLS)和[BAT2_N_CELLS](../advanced_config/parameter_reference.md#BAT2_N_CELLS)。
:::

### 满电压（每个电芯）

这设置每个电芯的_标称_最大电压（电芯被认为"满"的最低电压）。

该值应设置为略低于电池的标称最大电芯电压，但不能太低，以至于飞行几分钟后估算容量仍为100%。

适当的使用值是：

- **LiPo：** 4.05V（_QGroundControl_中的默认值）
- **LiIon：** 4.05V

::: info
满电池的电压在充电后可能会随时间小幅下降。
设置略低于最大值的值可以补偿这种下降。
:::

::: info
此设置对应[参数](../advanced_config/parameters.md)：[BAT1_V_CHARGED](../advanced_config/parameter_reference.md#BAT1_V_CHARGED)和[BAT2_V_CHARGED](../advanced_config/parameter_reference.md#BAT2_V_CHARGED)。
:::

### 空电压（每个电芯）

这设置每个电芯的标称最小安全电压（使用低于此电压可能损坏电池）。

::: info
没有单一的值可以说电池是空的。
如果您选择的值太低，电池可能因深度放电而损坏（和/或飞行器可能坠毁）。
如果您选择的值太高，您可能不必要地缩短您的飞行。
:::

每个电芯最小电压的经验法则：

| 级别                             | LiPo (V) | LiIon (V) |
| -------------------------------- | -------- | --------- |
| 保守（无负载下的电压）           | 3.7      | 3         |
| "真实"最小值（负载下/飞行时电压） | 3.5      | 2.7       |
| 损坏电池（负载下的电压）         | 3.0      | 2.5       |

:::tip
低于保守范围，您越早给电池充电越好 - 它会持续更长时间并且容量损失更慢。
:::

::: info
此设置对应[参数](../advanced_config/parameters.md)：[BAT1_V_EMPTY](../advanced_config/parameter_reference.md#BAT1_V_EMPTY)和[BAT2_V_EMPTY](../advanced_config/parameter_reference.md#BAT2_V_EMPTY)。
:::

### 电压分压器

如果您有一个通过电源模块和飞行控制器的ADC测量电压的飞行器，则您应该为每个电源模块校准一次测量。
要校准，测量电池的实际电压（使用万用表）并与电源模块提供的值进行比较。
这用于计算"电压分压器"值，随后可用于将电源模块测量缩放到正确值。

执行此校准的最简单方法是使用_QGroundControl_并按照[设置 > 电源设置](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/power.html)（QGroundControl用户指南）上的分步指南进行操作。

::: info
此设置对应参数：[BAT1_V_DIV](../advanced_config/parameter_reference.md#BAT1_V_DIV)和[BAT2_V_DIV](../advanced_config/parameter_reference.md#BAT2_V_DIV)。
:::

### 每伏安培 {#current_divider}

:::tip
如果您的电源模块不提供电流测量，则不需要此校准。
:::

如果电源模块提供，电流测量（默认情况下）用于[负载补偿](#load_compensation)和[电流积分](#current_integration)。
必须校准每伏安培分压器以确保准确的电流测量。

校准分压器的最简单方法是使用_QGroundControl_并按照[设置 > 电源设置](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/power.html)（QGroundControl用户指南）上的分步指南进行操作。

::: info
此设置对应参数：[BAT1_A_PER_V](../advanced_config/parameter_reference.md#BAT1_A_PER_V)和[BAT2_A_PER_V](../advanced_config/parameter_reference.md#BAT2_A_PER_V)。
:::

## 带负载补偿的基于电压的估算 {#load_compensation}

当电流流过电池时，内阻会导致电压降，与其开路（无负载）电压相比，降低了电池的测量输出电压。
使用[基本配置](#basic_settings)时，测量输出电压用于估算可用容量，这意味着当您上下飞行或以其他方式改变电池负载时，电池电量将显示波动。

_负载补偿_使用内阻的测量值或估算值来校正负载下的变化，导致飞行时估算容量的变化要小得多。
当使用提供电流测量的电源模块时，这默认启用。

要使用负载补偿，首先设置[基本配置](#basic_settings)。
_空电压_（[BATn_V_EMPTY](../advanced_config/parameter_reference.md#BAT1_V_EMPTY)，其中`n`是电池编号）应设置得更高（比没有补偿时），因为补偿电压用于估算（通常设置为略低于使用后空电芯的预期静止电芯电压）。

然后您需要在基本设置屏幕中校准[每伏安培分压器](#current_divider)（以获得可靠的电流测量）。

PX4默认使用基于电池内阻_实时估算_的电流负载补偿（如果[BAT1_R_INTERNAL=-1](../advanced_config/parameter_reference.md#BAT1_R_INTERNAL)启用实时估算）。
使用实时估算允许补偿适应由于飞行期间温度变化以及随着时间推移电池退化而导致的电池内阻变化。

内阻也可以测量并在[BAT1_R_INTERNAL](../advanced_config/parameter_reference.md#BAT1_R_INTERNAL)中[手动设置](../advanced_config/parameters.md)。
此参数中的正值将用于内阻而不是估算值（`0`完全禁用负载补偿）。

:::info
有一些LiPo充电器可以测量您电池的内阻。
LiPo电池的典型值是每个电芯5mΩ，但这可能因放电电流额定值、电芯的年龄和健康状况而异。
:::

## 基于电压估算与电流积分融合 {#current_integration}

这是测量相对电池消耗的最准确方法。
如果在每次启动时用健康且新鲜充电的电池正确设置，那么估算质量将与智能电池相当（理论上允许准确的剩余飞行时间估算）。

该方法通过将可用容量的基于电压的估算与已消耗电量的基于电流的估算_融合_来评估剩余电池容量。
它需要能够准确测量电流的硬件。

要启用此功能：

1. 首先使用[负载补偿](#load_compensation)设置准确的电压估算。

   :::tip
   包括校准[每伏安培分压器](#current_divider)设置。
   :::

2. 将参数[BAT1_CAPACITY](../advanced_config/parameter_reference.md#BAT1_CAPACITY)设置为约为公布电池容量的90%（通常印在电池标签上）。

   ::: info
   不要将此值设置得太高，因为这可能导致估算不良或估算容量突然下降。
   :::

---

**附加信息**

随时间消耗的电量估算通过数学积分测量电流产生（此方法提供非常准确的能量消耗估算）。

在系统启动时，PX4首先使用基于电压的估算来确定初始电池电量。然后将此估算与电流积分的值融合，以提供更好的组合估算。
在融合结果中对每个估算的相对重视取决于电池状态。
电池越空，基于电压的估算融合得越多。这防止了深度放电（例如，因为它配置了错误的容量或起始值错误）。

如果您总是从健康的满电池开始，这种方法类似于智能电池使用的方法。

::: info
电流积分不能单独使用（没有基于电压的估算），因为它无法确定_初始_容量。
电压估算允许您估算初始容量并提供可能错误的持续反馈（例如，如果电池有故障，或者使用不同方法计算的容量之间存在不匹配）。
:::
