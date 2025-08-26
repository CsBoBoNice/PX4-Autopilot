# 安全（故障安全）配置

PX4有许多安全功能来保护和恢复您的载具，如果出现问题：

- _故障安全_允许您指定可以安全飞行的区域和条件，以及如果触发故障安全将执行的[动作](#failsafe-actions)（例如，着陆、保持位置或返回到指定点）。
  最重要的故障安全设置在_QGroundControl_ [安全设置](#qgroundcontrol-safety-setup)页面中配置。
  其他必须通过[参数](../advanced_config/parameters.md)配置。
- 遥控器上的[安全开关](#emergency-switches)可用于在出现问题时立即停止电机或返回载具。

## QGroundControl安全设置

_QGroundControl_安全设置页面通过单击_QGroundControl_图标、**载具设置**，然后在侧边栏中选择**安全**来访问。
这包括许多最重要的故障安全设置（电池、遥控丢失等）以及触发动作_返回_和_着陆_的设置。

![安全设置(QGC)](../../assets/qgc/setup/safety/safety_setup.png)

## 故障安全动作

当触发故障安全时，默认行为（对于大多数故障安全）是在执行相关故障安全动作之前进入保持模式[COM_FAIL_ACT_T](../advanced_config/parameter_reference.md#COM_FAIL_ACT_T)秒。
这给用户时间注意到正在发生的事情，并在需要时覆盖故障安全。
在大多数情况下，这可以通过使用遥控或地面站切换模式来完成（注意在故障安全保持期间，移动遥控杆不会触发覆盖）。

下面的列表显示了所有故障安全动作的集合，按严重性递增排序。
注意不同类型的故障安全可能不支持所有这些动作。

| 动作                                                 | 描述                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a id="act_none"></a>无/禁用                     | 无动作。故障安全将被忽略。                                                                                                                                                                                                                                                                                               |
| <a id="act_warn"></a>警告                           | 将发送警告消息（即到_QGroundControl_）。                                                                                                                                                                                                                                                                             |
| <a id="act_hold"></a>保持模式                         | 载具将进入[保持模式（多旋翼）](../flight_modes_mc/hold.md)或[保持模式（固定翼）](../flight_modes_fw/hold.md)并分别悬停或盘旋。VTOL载具将根据其当前模式（多旋翼/固定翼）保持。                                                                                                                |
| <a id="act_return"></a>[返回模式][return]           | 载具将进入_返回模式_。返回行为可以在[返回主页设置](#return-mode-settings)（下面）中设置。                                                                                                                                                                                                                        |
| <a id="act_land"></a>着陆模式                         | 载具将进入[着陆模式（多旋翼）](../flight_modes_mc/land.md)或[着陆模式（固定翼）](../flight_modes_fw/land.md)，并着陆。VTOL将首先过渡到多旋翼模式。                                                                                                                                                                                |
| <a id="act_disarm"></a>解除武装                          | 立即停止电机。                                                                                                                                                                                                                                                                                                          |
| <a id="act_term"></a>[飞行终止][flight_term] | 关闭所有控制器并将所有PWM输出设置为其故障安全值（例如[PWM_MAIN_FAILn][pwm_main_failn]、[PWM_AUX_FAILn][pwm_main_failn]）。故障安全输出可用于部署降落伞、起落架或执行其他操作。对于固定翼载具，这可能允许您将载具滑翔到安全地点。 |

[flight_term]: ../advanced_config/flight_termination.md
[return]: ../flight_modes/return.md
[pwm_main_failn]: ../advanced_config/parameter_reference.md#PWM_MAIN_FAIL1
[pwm_aux_failn]: ../advanced_config/parameter_reference.md#PWM_AUX_FAIL1

如果触发多个故障安全，将采取更严重的动作。
例如，如果遥控和GPS都丢失，手动控制丢失设置为[返回模式](#act_return)，地面站链路丢失设置为[着陆](#act_land)，则执行着陆。

:::tip
可以使用[故障安全状态机仿真](safety_simulation.md)测试触发不同故障安全时的确切行为。
:::

### 返回模式设置

<!-- 建议用摘要和链接替换此部分 - 返回模式很复杂 -->

_返回_是一个常见的[故障安全动作](#failsafe-actions)，它启用[返回模式](../flight_modes/return.md)将载具返回到起始位置。
每个载具的默认设置通常是合适的，但对于固定翼载具，您通常需要定义任务着陆。

::: tip
如果您想更改配置，应该仔细阅读_适用于您的载具类型_的[返回模式](../flight_modes/return.md)文档以了解选项。
:::

QGC允许用户设置返回模式和着陆行为的某些方面，例如飞回的高度和如果需要部署起落架的悬停时间。

![安全 - 返回主页设置(QGC)](../../assets/qgc/setup/safety/safety_return_home.png)

### 着陆模式设置

_在当前位置着陆_是一个常见的[故障安全动作](#failsafe-actions)（特别是对于多旋翼），启用[着陆模式](../flight_modes_mc/land.md)。
每个载具的默认设置通常是合适的。

::: tip
如果您想更改配置，应该仔细阅读_适用于您的载具类型_的[着陆模式](../flight_modes_fw/land.md)文档以了解选项。
:::

QGC允许用户设置着陆行为的某些方面，例如着陆后解除武装的时间和下降速率（仅适用于多旋翼）。

![安全 - 着陆模式设置(QGC)](../../assets/qgc/setup/safety/safety_land_mode.png)

## 电池故障安全

### 电池电量故障安全

当电池容量下降到电池故障安全电量值以下时，触发低电池故障安全。
您可以在QGroundControl中配置每个级别的电量和故障安全动作。

![安全 - 电池(QGC)](../../assets/qgc/setup/safety/safety_battery.png)

最常见的配置是将值和动作设置如上（`警告 > 故障安全 > 紧急`），并将[故障安全动作](#COM_LOW_BAT_ACT)设置为在"警告级别"警告，在"故障安全级别"触发返回模式，在"紧急级别"立即着陆。

设置和基础参数如下所示。

| 设置                                             | 参数                                                                    | 描述                                                                           |
| --------------------------------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| <a id="COM_LOW_BAT_ACT"></a>故障安全动作         | [COM_LOW_BAT_ACT](../advanced_config/parameter_reference.md#COM_LOW_BAT_ACT) | 当容量下降到触发级别以下时警告、返回或着陆。             |
| <a id="BAT_LOW_THR"></a>电池警告级别          | [BAT_LOW_THR](../advanced_config/parameter_reference.md#BAT_LOW_THR)         | 警告（或其他动作）的百分比容量。                                  |
| <a id="BAT_CRIT_THR"></a>电池故障安全级别     | [BAT_CRIT_THR](../advanced_config/parameter_reference.md#BAT_CRIT_THR)       | 返回动作的百分比容量（或如果选择单一动作则为其他动作）。 |
| <a id="BAT_EMERGEN_THR"></a>电池紧急级别 | [BAT_EMERGEN_THR](../advanced_config/parameter_reference.md#BAT_EMERGEN_THR) | 触发着陆（立即）动作的百分比容量。                         |

### 飞行时间故障安全

还有几个其他"电池相关"故障安全机制可以使用参数配置：

- "安全返回剩余飞行时间"故障安全（[COM_FLTT_LOW_ACT](#COM_FLTT_LOW_ACT)）在PX4估计载具刚好有足够的电池剩余用于返回模式着陆时启用。
  您可以配置此项忽略故障安全、警告或启用返回模式。
- "最大飞行时间故障安全"（[COM_FLT_TIME_MAX](#COM_FLT_TIME_MAX)）允许您设置起飞后的最大飞行时间，届时载具将自动进入返回模式（它也会在此时间的90%"警告"）。这就像电池中总飞行时间的"硬编码"估计。该功能默认禁用。
- 武装的"最小电池"参数（[COM_ARM_BAT_MIN](#COM_ARM_BAT_MIN)）如果电池电量低于指定值，则首先阻止武装。

设置和基础参数如下所示。

| 设置                                                              | 参数                                                                      | 描述                                                                                                                     |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| <a id="COM_FLTT_LOW_ACT"></a>安全返回低飞行时间动作 | [COM_FLTT_LOW_ACT](../advanced_config/parameter_reference.md#COM_FLTT_LOW_ACT) | 当返回模式只能刚好到达安全点时的动作。`0`：无，`1`：警告，`3`：返回模式（默认）。 |
| <a id="COM_FLT_TIME_MAX"></a>最大飞行时间故障安全级别     | [COM_FLT_TIME_MAX](../advanced_config/parameter_reference.md#COM_FLT_TIME_MAX) | 返回模式将启用前的最大允许飞行时间，以秒为单位。`-1`：禁用（默认）。                           |

## 手动控制丢失故障安全

如果与[遥控发射机](../getting_started/rc_transmitter_receiver.md)或[操纵杆](../config/joystick.md)的连接丢失，并且没有备用，则可能触发手动控制丢失故障安全。
如果使用[遥控发射机](../getting_started/rc_transmitter_receiver.md)，如果遥控[发射机链路丢失](../getting_started/rc_transmitter_receiver.md#set-signal-loss-behaviour)，则触发此功能。
如果使用通过MAVLink数据链路连接的[操纵杆](../config/joystick.md)，如果操纵杆断开连接或数据链路丢失，则触发此功能。

::: info
PX4和接收机可能还需要配置以_检测遥控丢失_：[遥控设置 > 遥控丢失检测](../config/radio.md#rc-loss-detection)。
:::

![安全 - 遥控丢失(QGC)](../../assets/qgc/setup/safety/safety_rc_loss.png)

QGroundControl安全UI允许您设置[故障安全动作](#failsafe-actions)和[遥控丢失超时](#COM_RC_LOSS_T)。
想要在特定自动模式（任务、保持、离板）中禁用遥控丢失故障安全的用户可以使用参数[COM_RCL_EXCEPT](#COM_RCL_EXCEPT)。

其他（和基础）参数设置如下所示。

| 参数                                                                                             | 设置                     | 描述                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------------------------------------------------------------------------------------- | --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a id="COM_RC_LOSS_T"></a>[COM_RC_LOSS_T](../advanced_config/parameter_reference.md#COM_RC_LOSS_T)    | 手动控制丢失超时 | 在从所选手动控制源接收到最后设定点后，手动控制被认为丢失的时间。这必须保持较短，因为载具将继续使用旧的手动控制设定点飞行，直到超时触发。                                                                                                                                              |
| <a id="COM_FAIL_ACT_T"></a>[COM_FAIL_ACT_T](../advanced_config/parameter_reference.md#COM_FAIL_ACT_T) | 故障安全反应延迟     | 故障安全条件被触发（`COM_RC_LOSS_T`）和故障安全动作（RTL、着陆、保持）之间的延迟秒数。在此状态下，载具在保持模式下等待手动控制源重新连接。对于远程飞行，这可能设置得更长，以便间歇性连接丢失不会立即调用故障安全。它可以为零，以便故障安全立即触发。 |
| <a id="NAV_RCL_ACT"></a>[NAV_RCL_ACT](../advanced_config/parameter_reference.md#NAV_RCL_ACT)          | 故障安全动作             | 禁用、悬停、返回、着陆、解除武装、终止。                                                                                                                                                                                                                                                                                                                                                       |
| <a id="COM_RCL_EXCEPT"></a>[COM_RCL_EXCEPT](../advanced_config/parameter_reference.md#COM_RCL_EXCEPT) | 遥控丢失例外          | 设置忽略手动控制丢失的模式：任务、保持、离板。                                                                                                                                                                                                                                                                                                                          |

## 数据链路丢失故障安全

如果遥测链路（与地面站的连接）丢失，则触发数据链路丢失故障安全。

![安全 - 数据链路丢失(QGC)](../../assets/qgc/setup/safety/safety_data_link_loss.png)

设置和基础参数如下所示。

| 设置                | 参数                                                                | 描述                                                                       |
| ---------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------------- |
| 数据链路丢失超时 | [COM_DL_LOSS_T](../advanced_config/parameter_reference.md#COM_DL_LOSS_T) | 丢失数据连接后故障安全将触发前的时间。 |
| 故障安全动作        | [NAV_DLL_ACT](../advanced_config/parameter_reference.md#NAV_DLL_ACT)     | 禁用、保持模式、返回模式、着陆模式、解除武装、终止。                   |

以下设置也适用，但不在QGC UI中显示。

| 设置                                                     | 参数                                                                  | 描述                                          |
| ----------------------------------------------------------- | -------------------------------------------------------------------------- | ---------------------------------------------------- |
| <a id="COM_DLL_EXCEPT"></a>DLL故障安全的模式例外 | [COM_DLL_EXCEPT](../advanced_config/parameter_reference.md#COM_DLL_EXCEPT) | 设置DL丢失不会触发故障安全的模式。 |

## 地理围栏故障安全

当无人机突破"虚拟"边界时，触发_地理围栏故障安全_。
在最简单的形式中，边界设置为以起始位置为中心的圆柱体。
如果载具移动到半径之外或高于指定的_故障安全动作_将触发的高度。

![安全 - 地理围栏(QGC)](../../assets/qgc/setup/safety/safety_geofence.png)

:::tip
PX4单独支持更复杂的地理围栏几何，具有多个任意多边形和圆形包含和排除区域：[飞行 > 地理围栏](../flying/geofence.md)。
:::

设置和基础[地理围栏参数](../advanced_config/parameter_reference.md#geofence)如下所示。

| 设置          | 参数                                                                    | 描述                                                     |
| ---------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------- |
| 违反动作 | [GF_ACTION](../advanced_config/parameter_reference.md#GF_ACTION)             | 无、警告、保持模式、返回模式、终止、着陆。         |
| 最大半径       | [GF_MAX_HOR_DIST](../advanced_config/parameter_reference.md#GF_MAX_HOR_DIST) | 地理围栏圆柱体的水平半径。如果为0则禁用地理围栏。 |
| 最大高度     | [GF_MAX_VER_DIST](../advanced_config/parameter_reference.md#GF_MAX_VER_DIST) | 地理围栏圆柱体的高度。如果为0则禁用地理围栏。            |

::: info
将`GF_ACTION`设置为终止将在违反围栏时杀死载具。
由于这种固有的危险，此功能使用[CBRK_FLIGHTTERM](#CBRK_FLIGHTTERM)禁用，需要重置为0才能真正关闭系统。
:::

以下设置也适用，但不在QGC UI中显示。

| 设置                                                            | 参数                                                                    | 描述                                                                                                                                         |
| ------------------------------------------------------------------ | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a id="GF_SOURCE"></a>地理围栏源                              | [GF_SOURCE](../advanced_config/parameter_reference.md#GF_SOURCE)             | 设置位置源是估计的全球位置还是直接来自GPS设备。                                                             |
| <a id="GF_PREDICT"></a>抢占式地理围栏触发              | [GF_PREDICT](../advanced_config/parameter_reference.md#GF_PREDICT)           | （实验性）如果预测载具当前运动将触发违反，则触发地理围栏（而不是在违反后迟触发）。 |
| <a id="CBRK_FLIGHTTERM"></a>飞行终止断路器 | [CBRK_FLIGHTTERM](../advanced_config/parameter_reference.md#CBRK_FLIGHTTERM) | 启用/禁用飞行终止动作（默认禁用）。                                                                                   |

## 位置（GNSS）丢失故障安全

当PX4位置估计的质量降到可接受水平以下时（这可能由GPS丢失引起），在需要可接受位置估计的模式下，触发_位置丢失故障安全_。
下面的部分首先介绍触发器，然后是控制器采取的故障安全动作。

### 位置丢失故障安全触发器

PX4中基本上有两种机制来触发位置故障安全：

- 自上次融合提供直接速度或水平位置测量的传感器数据以来的超时。属于该类别的传感器有：GNSS、光流、空速、VIO、辅助全球位置。
- 估计的水平位置精度超过某个阈值。此检查仅在悬停系统（旋翼载具或悬停阶段的VTOL）上进行。


| 参数                                                                                                | 描述                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a id="EKF2_NOAID_TOUT"></a>[EKF2_NOAID_TOUT](../advanced_config/parameter_reference.md#EKF2_NOAID_TOUT) | 最大惯性航位推算时间，即接收到任何约束速度漂移的传感器的最后数据样本后的时间[微秒]。 |
| <a id="COM_POS_FS_EPH"></a>[COM_POS_FS_EPH](../advanced_config/parameter_reference.md#COM_POS_FS_EPH)    | 悬停载具（多旋翼和悬停中的VTOL）的水平位置误差阈值。固定翼载具将此值设置为无穷大。          |

### 位置丢失故障安全动作

故障动作由[COM_POSCTL_NAVL](../advanced_config/parameter_reference.md#COM_POSCTL_NAVL)控制，基于是否假设遥控控制可用（和高度信息）：

- `0`：遥控可用。
  如果高度估计可用，切换到_高度模式_，否则切换到_自稳模式_。
- `1`：遥控_不_可用。
  如果高度估计可用，切换到_下降模式_，否则进入飞行终止。
  _下降模式_是不需要位置估计的着陆模式。

固定翼飞机和未配置为悬停着陆的VTOL（[NAV_FORCE_VT](../advanced_config/parameter_reference.md#NAV_FORCE_VT)）有一个参数（[FW_GPSF_LT](../advanced_config/parameter_reference.md#FW_GPSF_LT)），定义它们在失去位置后尝试着陆前将悬停多长时间（以恒定滚转角（[FW_GPSF_R](../advanced_config/parameter_reference.md#FW_GPSF_R)）在当前高度盘旋）。
如果VTOL配置为切换到悬停着陆（[NAV_FORCE_VT](../advanced_config/parameter_reference.md#NAV_FORCE_VT)），那么它们将首先过渡然后下降。

所有载具的相关参数如下所示。

| 参数                                                                                                | 描述                                                                                                   |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| <a id="COM_POSCTL_NAVL"></a>[COM_POSCTL_NAVL](../advanced_config/parameter_reference.md#COM_POSCTL_NAVL) | 任务期间位置控制导航丢失响应。值：`0` - 假设使用遥控，`1` - 假设无遥控。 |

仅影响固定翼载具的参数：

| 参数                                                                                 | 描述                                                                                                 |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| <a id="FW_GPSF_LT"></a>[FW_GPSF_LT](../advanced_config/parameter_reference.md#FW_GPSF_LT) | 悬停时间（等待GPS恢复，然后进入着陆或飞行终止）。设置为0以禁用。 |
| <a id="FW_GPSF_R"></a>[FW_GPSF_R](../advanced_config/parameter_reference.md#FW_GPSF_R)    | 盘旋时的固定滚转/倾斜角。                                                                       |

## 离板丢失故障安全

当在[离板控制](../flight_modes/offboard.md)下离板链路丢失时，触发_离板丢失故障安全_。
可以根据是否还有遥控连接可用来指定不同的故障安全行为。

相关参数如下所示：

| 参数                                                                  | 描述                                                                                                       |
| -------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [COM_OF_LOSS_T](../advanced_config/parameter_reference.md#COM_OF_LOSS_T)   | 离板连接丢失后触发故障安全前的延迟。                                         |
| [COM_OBL_RC_ACT](../advanced_config/parameter_reference.md#COM_OBL_RC_ACT) | 如果遥控可用的故障安全动作：位置模式、高度模式、手动模式、返回模式、着陆模式、保持模式。 |

## 交通避让故障安全

交通避让故障安全允许PX4在任务期间响应应答器数据（例如来自[ADSB应答器](../advanced_features/traffic_avoidance_adsb.md)）。

相关参数如下所示：

| 参数                                                                    | 描述                                                      |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| [NAV_TRAFF_AVOID](../advanced_config/parameter_reference.md#NAV_TRAFF_AVOID) | 设置故障安全动作：禁用、警告、返回模式、着陆模式。 |

## 四降故障安全

VTOL载具无法再以固定翼模式飞行时的故障安全，可能由于推进电机、空速传感器或控制面故障。
如果触发故障安全，载具将立即切换到多旋翼模式并执行参数[COM_QC_ACT](#COM_QC_ACT)中定义的动作。

::: info
四降也可以通过发送MAVLINK [MAV_CMD_DO_VTOL_TRANSITION](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_VTOL_TRANSITION)消息（`param2`设置为`1`）来触发。
:::

控制四降何时触发的参数列在下表中。

| 参数                                                                                                   | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a id="COM_QC_ACT"></a>[COM_QC_ACT](../advanced_config/parameter_reference.md#COM_QC_ACT)                   | 切换到多旋翼飞行后的四降动作。可以设置为：[警告](#act_warn)、[返回](#act_return)、[着陆](#act_land)、[保持](#act_hold)。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| <a id="VT_FW_QC_HMAX"></a>[VT_FW_QC_HMAX](../advanced_config/parameter_reference.md#VT_FW_QC_HMAX)          | 最大四降高度，低于此高度四降故障安全无法触发。这可防止高空四降下降，可能会耗尽电池（本身会导致坠毁）。高度相对于地面、起始点或本地原点（按优先顺序，取决于可用内容）。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| <a id="VT_QC_ALT_LOSS"></a>[VT_QC_ALT_LOSS](../advanced_config/parameter_reference.md#VT_QC_ALT_LOSS)       | 非指令下降四降高度阈值。<br><br>在高度控制模式中，如[保持模式](../flight_modes_fw/hold.md)、[位置模式](../flight_modes_fw/position.md)、[高度模式](../flight_modes_fw/altitude.md)或[任务模式](../flight_modes_fw/mission.md)，载具应跟踪其当前"指令"高度设定点。如果载具跌落到指令设定点以下太远（由此参数定义的量），则触发四降故障安全。<br><br>注意，四降仅在载具持续丢失指令设定点以下的高度时触发；如果指令高度设定点增加得比载具能跟上的快，则不会触发。 |
| <a id="VT_QC_T_ALT_LOSS"></a>[VT_QC_T_ALT_LOSS](../advanced_config/parameter_reference.md#VT_QC_T_ALT_LOSS) | VTOL过渡到固定翼飞行期间四降触发的高度丢失阈值。如果载具在完成过渡前跌落到初始高度以下这么远，则触发四降。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| <a id="VT_FW_MIN_ALT"></a>[VT_FW_MIN_ALT](../advanced_config/parameter_reference.md#VT_FW_MIN_ALT)          | 固定翼飞行的起始点以上最小高度。当固定翼飞行中高度降到此值以下时，载具触发四降。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| <a id="VT_FW_QC_R"></a>[VT_FW_QC_R](../advanced_config/parameter_reference.md#VT_FW_QC_R)                   | 固定翼模式下四降触发的绝对滚转阈值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <a id="VT_FW_QC_P"></a>[VT_FW_QC_P](../advanced_config/parameter_reference.md#VT_FW_QC_P)                   | 固定翼模式下四降触发的绝对俯仰阈值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

## 大风故障安全

当风速超过警告和最大风速阈值时，大风故障安全可以触发警告和/或其他模式更改。
相关参数列在下表中。

| 参数                                                                                                   | 描述                                                                                                                                                                                                                                          |
| ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a id="COM_WIND_MAX"></a>[COM_WIND_MAX](../advanced_config/parameter_reference.md#COM_WIND_MAX)             | 触发故障安全动作的风速阈值，以m/s为单位（[COM_WIND_MAX_ACT](#COM_WIND_MAX_ACT)）。                                                                                                                                                                  |
| <a id="COM_WIND_MAX_ACT"></a>[COM_WIND_MAX_ACT](../advanced_config/parameter_reference.md#COM_WIND_MAX_ACT) | 大风故障安全动作（跟随[COM_WIND_MAX](#COM_WIND_MAX)触发）。可以设置为：`0`：无（默认），`1`：[警告](#act_warn)，`2`：[保持](#act_hold)，`3`：[返回](#act_return)，`4`：[终止](#act_term)，`5`：[着陆](#act_land)。 |
| <a id="COM_WIND_WARN"></a>[COM_WIND_WARN](../advanced_config/parameter_reference.md#COM_WIND_WARN)          | 触发周期性故障安全警告的风速阈值。                                                                                                                                                                                        |

## 故障检测器

故障检测器允许载具在意外翻转或被外部故障检测系统通知时采取保护动作。

在**飞行**期间，如果满足故障条件，故障检测器可用于触发[飞行终止](../advanced_config/flight_termination.md)，然后可能启动[降落伞](../peripherals/parachute.md)或执行其他动作。

::: info
飞行期间的故障检测默认停用（通过设置参数启用：[CBRK_FLIGHTTERM=0](#CBRK_FLIGHTTERM)）。
:::

在**起飞**期间，如果载具翻转，故障检测器[姿态触发器](#attitude-trigger)调用[解除武装动作](#act_disarm)（解除武装会停止电机，但与飞行终止不同，不会启动降落伞或执行其他故障动作）。
注意此检查在起飞时_始终启用_，与`CBRK_FLIGHTTERM`参数无关。

故障检测器在所有载具类型和模式中都处于活动状态，除了那些载具_预期_做翻转的模式（即[特技模式（多旋翼）](../flight_modes_mc/altitude.md)、[特技模式（固定翼）](../flight_modes_fw/altitude.md)和[手动（固定翼）](../flight_modes_fw/manual.md)）。

### 姿态触发器

故障检测器可以配置为在载具姿态超过预定义的俯仰和滚转值超过指定时间时触发。

相关参数如下所示：

| 参数                                                                                                | 描述                                                                                                                      |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| <a id="CBRK_FLIGHTTERM"></a>[CBRK_FLIGHTTERM](../advanced_config/parameter_reference.md#CBRK_FLIGHTTERM) | 飞行终止断路器。从121212（默认）取消设置以启用由于故障检测器或FMU丢失导致的飞行终止。 |
| <a id="FD_FAIL_P"></a>[FD_FAIL_P](../advanced_config/parameter_reference.md#FD_FAIL_P)                   | 最大允许俯仰（度）。                                                                                              |
| <a id="FD_FAIL_R"></a>[FD_FAIL_R](../advanced_config/parameter_reference.md#FD_FAIL_R)                   | 最大允许滚转（度）。                                                                                               |
| <a id="FD_FAIL_P_TTRI"></a>[FD_FAIL_P_TTRI](../advanced_config/parameter_reference.md#FD_FAIL_P_TTRI)    | 超过[FD_FAIL_P](#FD_FAIL_P)进行故障检测的时间（默认0.3秒）。                                                     |
| <a id="FD_FAIL_R_TTRI"></a>[FD_FAIL_R_TTRI](../advanced_config/parameter_reference.md#FD_FAIL_R_TTRI)    | 超过[FD_FAIL_R](#FD_FAIL_R)进行故障检测的时间（默认0.3秒）。                                                     |

### 外部自动触发系统（ATS）

[故障检测器](#failure-detector)如果[启用](#CBRK_FLIGHTTERM)，也可以由外部ATS系统触发。
外部触发系统必须连接到飞行控制器端口AUX5（或没有AUX端口的板上的MAIN5），并使用下面的参数配置。

::: info
外部ATS由[ASTM F3322-18](https://webstore.ansi.org/standards/astm/ASTMF332218)要求。
ATS设备的一个例子是[FruityChutes Sentinel自动触发系统（SATS-MINI）](https://fruitychutes.com/uav_rpv_drone_recovery_parachutes/sentinel-automatic-trigger-system)。
:::

| 参数                                                                                                | 描述                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| <a id="FD_EXT_ATS_EN"></a>[FD_EXT_ATS_EN](../advanced_config/parameter_reference.md#FD_EXT_ATS_EN)       | 在AUX5或MAIN5（取决于板）上启用PWM输入，用于从外部自动触发系统（ATS）启用故障安全。默认：禁用。 |
| <a id="FD_EXT_ATS_TRIG"></a>[FD_EXT_ATS_TRIG](../advanced_config/parameter_reference.md#FD_EXT_ATS_TRIG) | 来自外部自动触发系统的PWM阈值，用于启用故障安全。默认：1900毫秒。                                                |

## 任务可行性检查

运行许多检查以确保任务只有在_可行_时才能开始。
例如，检查确保第一个航点不会太远，并且任务飞行路径不会与任何地理围栏冲突。

由于这些严格来说不是"故障安全"，它们记录在[任务模式（固定翼）> 任务可行性检查](../flight_modes_fw/mission.md#mission-feasibility-checks)和[任务模式（多旋翼）> 任务可行性检查](../flight_modes_mc/mission.md#mission-feasibility-checks)中。

## 紧急开关

遥控开关可以配置（作为_QGroundControl_ [飞行模式设置](../config/flight_mode.md)的一部分），允许您在出现问题或紧急情况时采取快速纠正动作；例如，停止所有电机，或激活[返回模式](#return-switch)。

本节列出了可用的紧急开关。

### 杀死开关

杀死开关立即停止所有电机输出——如果正在飞行，载具将开始坠落！

[默认情况下](#COM_KILL_DISARM)，如果开关在5秒内恢复，电机将重新启动，之后载具将自动解除武装，您需要重新武装才能启动电机。

| 参数                                                                                                | 描述                                                                     |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| <a id="COM_KILL_DISARM"></a>[COM_KILL_DISARM](../advanced_config/parameter_reference.md#COM_KILL_DISARM) | 启用杀死开关后解除武装的超时值。默认：`5`秒。 |

::: info
还有一个[杀死手势](#kill-gesture)，无法恢复。
:::

### 武装/解除武装开关

武装/解除武装开关是默认基于摇杆的武装/解除武装机制的_直接替代品_（并具有相同的目的：确保在电机启动/停止前有一个故意的步骤）。
它可能比默认机制更受青睐，因为：

- 偏好开关胜过摇杆动作。
- 它避免了在空中意外触发武装/解除武装的某个摇杆动作。
- 没有延迟（立即反应）。

武装/解除武装开关立即解除武装（停止）那些_支持飞行中解除武装_的[飞行模式](../flight_modes/index.md#flight-modes)的电机。
这包括：

- _手动模式_
- _特技模式_
- _自稳_

对于不支持飞行中解除武装的模式，开关在飞行期间被忽略，但可以在检测到着陆后使用。
这包括_位置模式_和自主模式（例如_任务_、_着陆_等）。

::: info
[自动解除武装超时](#auto-disarming-timeouts)（例如通过[COM_DISARM_LAND](#COM_DISARM_LAND)）独立于武装/解除武装开关——即使开关武装，超时仍将工作。
:::

<!--
**Note** This can also be done by [manually setting](../advanced_config/parameters.md) the [RC_MAP_ARM_SW](../advanced_config/parameter_reference.md#RC_MAP_ARM_SW) parameter to the corresponding switch RC channel.
  If the switch positions are reversed, change the sign of the parameter [RC_ARMSWITCH_TH](../advanced_config/parameter_reference.md#RC_ARMSWITCH_TH) (or also change its value to alter the threshold value).
-->

### 返回开关

返回开关可用于立即启用[返回模式](../flight_modes/return.md)。

## 杀死手势

杀死手势立即停止所有电机输出——如果正在飞行，载具将开始坠落！

动作无法在不重启的情况下恢复（这与[杀死开关](#kill-switch)不同，后者可以在[COM_KILL_DISARM](#COM_KILL_DISARM)定义的时间段内恢复操作）。

| 参数                                                                                                | 描述                                                                                          |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| <a id="MAN_KILL_GEST_T"></a>[MAN_KILL_GEST_T](../advanced_config/parameter_reference.md#MAN_KILL_GEST_T) | 在杀死电机前保持摇杆在手势位置的时间。默认：`-1`秒（禁用）。 |

## 武装/解除武装设置

[指挥官模块](../advanced_config/parameter_reference.md#commander)有许多以`COM_ARM`为前缀的参数，配置载具是否可以武装以及在什么条件下（注意一些以`COM_ARM`为前缀命名的参数用于武装其他系统）。
以`COM_DISARM_`为前缀的参数影响解除武装行为。

### 自动解除武装超时

如果载具起飞太慢和/或着陆后，您可以设置超时以自动解除载具武装（解除载具武装会移除电机电源，因此螺旋桨不会旋转）。

[相关参数](../advanced_config/parameters.md)如下所示：

| 参数                                                                                                   | 描述                                                |
| ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| <a id="COM_DISARM_LAND"></a>[COM_DISARM_LAND](../advanced_config/parameter_reference.md#COM_DISARM_LAND)    | 着陆后自动解除武装的超时。                     |
| <a id="COM_DISARM_PRFLT"></a>[COM_DISARM_PRFLT](../advanced_config/parameter_reference.md#COM_DISARM_PRFLT) | 如果载具起飞太慢的自动解除武装超时。 |

### 武装前提条件

这些参数可用于设置阻止武装的条件。

| 参数                                                                                                   | 描述                                                                                                                                                                                                |
| ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a id="COM_ARMABLE"></a>[COM_ARMABLE](../advanced_config/parameter_reference.md#COM_ARMABLE)                | 启用武装（完全）。`0`：禁用，`1`：启用（默认）。                                                                                                                                             |
| <a id="COM_ARM_BAT_MIN"></a>[COM_ARM_BAT_MIN](../advanced_config/parameter_reference.md#COM_ARM_BAT_MIN)    | 武装的最小电池电量。`0`：禁用（默认）。值：`0`-`0.9`，                                                                                                                              |
| <a id="COM_ARM_WO_GPS"></a>[COM_ARM_WO_GPS](../advanced_config/parameter_reference.md#COM_ARM_WO_GPS)       | 启用无GPS武装。`0`：禁用，`1`：启用（默认）。                                                                                                                                          |
| <a id="COM_ARM_MIS_REQ"></a>[COM_ARM_MIS_REQ](../advanced_config/parameter_reference.md#COM_ARM_MIS_REQ)    | 需要有效任务才能武装。`0`：禁用（默认），`1`：启用。                                                                                                                                      |
| <a id="COM_ARM_SDCARD"></a>[COM_ARM_SDCARD](../advanced_config/parameter_reference.md#COM_ARM_SDCARD)       | 需要SD卡才能武装。`0`：禁用（默认），`1`：警告，`2`：启用。                                                                                                                               |
| <a id="COM_ARM_AUTH_REQ"></a>[COM_ARM_AUTH_REQ](../advanced_config/parameter_reference.md#COM_ARM_AUTH_REQ) | 需要来自外部（MAVLink）系统的武装授权。允许武装（完全）的标志。`1`：启用，`0`：禁用（默认）。相关配置参数以`COM_ARM_AUTH_`为前缀。 |
| <a id="COM_ARM_ODID"></a>[COM_ARM_ODID](../advanced_config/parameter_reference.md#COM_ARM_ODID)             | 需要健康的远程ID系统才能武装。`0`：禁用（默认），`1`：警告，`2`：启用。                                                                                                              |

此外，还有许多配置系统和传感器限制的参数，如果超过则阻止武装：[COM_CPU_MAX](../advanced_config/parameter_reference.md#COM_CPU_MAX)、[COM_ARM_IMU_ACC](../advanced_config/parameter_reference.md#COM_ARM_IMU_ACC)、[COM_ARM_IMU_GYR](../advanced_config/parameter_reference.md#COM_ARM_IMU_GYR)、[COM_ARM_MAG_ANG](../advanced_config/parameter_reference.md#COM_ARM_MAG_ANG)、[COM_ARM_MAG_STR](../advanced_config/parameter_reference.md#COM_ARM_MAG_STR)。

## 更多信息

- [QGroundControl用户指南 > 安全设置](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/safety.html)
