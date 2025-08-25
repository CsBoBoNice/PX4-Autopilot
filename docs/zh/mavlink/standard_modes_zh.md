# 标准模式协议 (MAVLink)

<Badge type="tip" text="PX4 v1.15" />

PX4 从 v1.15 版本开始实现 MAVLink [标准模式协议](https://mavlink.io/en/services/standard_modes.md)，QGroundControl 的每日构建版本（和未来的发布版本）中有相应的实现。

该协议允许您发现飞行器可用的所有飞行模式，包括使用 [PX4 ROS 2 控制接口](../ros2/px4_ros2_control_interface.md) 创建的 PX4 外部模式，并获取或设置当前模式。

## 消息和命令概述

[标准模式](https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE) 是大多数飞行栈中常见的具有基本相同行为的模式，而自定义模式是特定于飞行栈的。

该协议允许：

- 从 PX4 和 ROS 2 发现系统支持的所有模式 ([MAV_CMD_REQUEST_MESSAGE](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_MESSAGE) 和 [AVAILABLE_MODES](https://mavlink.io/en/messages/common.html#AVAILABLE_MODES))。
- 发现当前模式 ([CURRENT_MODE](https://mavlink.io/en/messages/common.html#CURRENT_MODE))。
- 使用 [MAV_CMD_DO_SET_STANDARD_MODE](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_SET_STANDARD_MODE) 设置标准模式 ([MAV_STANDARD_MODE](https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE))（推荐）。
- 当模式集发生变化时通知 ([AVAILABLE_MODES_MONITOR](https://mavlink.io/en/messages/common.html#AVAILABLE_MODES_MONITOR))

您也可以使用 [SET_MODE](https://mavlink.io/en/messages/common.html#SET_MODE) 和来自 `AVAILABLE_MODES` 的自定义模式信息来设置自定义模式。
在撰写本文时，[MAV_CMD_DO_SET_MODE](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_SET_MODE) 不受支持。

## 支持的标准模式

PX4 宣布支持以下标准飞行模式，这意味着您可以通过调用 [MAV_CMD_DO_SET_STANDARD_MODE](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_SET_STANDARD_MODE) 与适当的 [MAV_STANDARD_MODE](https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE) 枚举值来启动它们。

### 多旋翼标准模式

MC 飞行器支持以下标准模式（其中一些被所有飞行器支持）：

| 标准模式                                                      | PX4 模式                                           | 内部模式 |
| ------------------------------------------------------------------ | -------------------------------------------------- | ------------- |
| [MAV_STANDARD_MODE_POSITION_HOLD][MAV_STANDARD_MODE_POSITION_HOLD] | [MC 位置模式](../flight_modes_mc/position.md) | POSCTL        |
| [MAV_STANDARD_MODE_ALTITUDE_HOLD][MAV_STANDARD_MODE_ALTITUDE_HOLD] | [MC 高度模式](../flight_modes_mc/altitude.md) | ALTCTL        |
| [MAV_STANDARD_MODE_ORBIT][MAV_STANDARD_MODE_ORBIT]                 | [FW 轨道模式](../flight_modes_mc/orbit.md)       | POSCTL        |
| [MAV_STANDARD_MODE_SAFE_RECOVERY][MAV_STANDARD_MODE_SAFE_RECOVERY] | [返航模式](../flight_modes/return.md)           | AUTO_RTL      |
| [MAV_STANDARD_MODE_MISSION][MAV_STANDARD_MODE_MISSION]             | [任务模式](../flight_modes_mc/mission.md)      | AUTO_MISSION  |
| [MAV_STANDARD_MODE_LAND][MAV_STANDARD_MODE_LAND]                   | [降落模式](../flight_modes_mc/land.md)            | AUTO_LAND     |
| [MAV_STANDARD_MODE_TAKEOFF][MAV_STANDARD_MODE_TAKEOFF]             | [起飞模式](../flight_modes_mc/takeoff.md)      | AUTO_TAKEOFF  |

[MAV_STANDARD_MODE_POSITION_HOLD]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_POSITION_HOLD
[MAV_STANDARD_MODE_ORBIT]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_ORBIT
[MAV_STANDARD_MODE_ALTITUDE_HOLD]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_ALTITUDE_HOLD

### 固定翼标准模式

FW 飞行器支持以下标准模式（其中一些被所有飞行器支持）：

| 标准模式                                                      | PX4 模式                                           | 内部模式 |
| ------------------------------------------------------------------ | -------------------------------------------------- | ------------- |
| [MAV_STANDARD_MODE_CRUISE][MAV_STANDARD_MODE_CRUISE]               | [FW 位置模式](../flight_modes_fw/position.md) | POSCTL        |
| [MAV_STANDARD_MODE_ALTITUDE_HOLD][MAV_STANDARD_MODE_ALTITUDE_HOLD] | [FW 高度模式](../flight_modes_fw/altitude.md) | ALTCTL        |
| [MAV_STANDARD_MODE_ORBIT][MAV_STANDARD_MODE_ORBIT]                 | [FW 保持模式](../flight_modes_fw/hold.md)         | AUTO_LOITER   |
| [MAV_STANDARD_MODE_SAFE_RECOVERY][MAV_STANDARD_MODE_SAFE_RECOVERY] | [返航模式](../flight_modes/return.md)           | AUTO_RTL      |
| [MAV_STANDARD_MODE_MISSION][MAV_STANDARD_MODE_MISSION]             | [任务模式](../flight_modes_fw/mission.md)      | AUTO_MISSION  |
| [MAV_STANDARD_MODE_LAND][MAV_STANDARD_MODE_LAND]                   | [降落模式](../flight_modes_fw/land.md)            | AUTO_LAND     |
| [MAV_STANDARD_MODE_TAKEOFF][MAV_STANDARD_MODE_TAKEOFF]             | [起飞模式](../flight_modes_fw/takeoff.md)      | AUTO_TAKEOFF  |

[MAV_STANDARD_MODE_CRUISE]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_CRUISE

### VTOL 标准模式

VTOL 飞行器支持以下标准模式（其中一些被所有飞行器支持）。
请注意，飞行器的行为取决于它是作为多旋翼还是固定翼飞行器飞行。

| 标准模式                                                      | PX4 模式                                           | 内部模式 |
| ------------------------------------------------------------------ | -------------------------------------------------- | ------------- |
| [MAV_STANDARD_MODE_ALTITUDE_HOLD][MAV_STANDARD_MODE_ALTITUDE_HOLD] | [FW 高度模式](../flight_modes_fw/altitude.md) | ALTCTL        |
| [MAV_STANDARD_MODE_SAFE_RECOVERY][MAV_STANDARD_MODE_SAFE_RECOVERY] | [返航模式](../flight_modes/return.md)           | AUTO_RTL      |
| [MAV_STANDARD_MODE_MISSION][MAV_STANDARD_MODE_MISSION]             | [任务模式](../flight_modes_mc/mission.md)      | AUTO_MISSION  |
| [MAV_STANDARD_MODE_LAND][MAV_STANDARD_MODE_LAND]                   | [降落模式](../flight_modes_mc/land.md)            | AUTO_LAND     |
| [MAV_STANDARD_MODE_TAKEOFF][MAV_STANDARD_MODE_TAKEOFF]             | [起飞模式](../flight_modes_mc/takeoff.md)      | AUTO_TAKEOFF  |

::: info
请注意，VTOL 飞行器也可能在相应模式中支持 `MAV_STANDARD_MODE_CRUISE`（FW）或 `MAV_STANDARD_MODE_POSITION_HOLD`（MC）和 `MAV_STANDARD_MODE_ORBIT`，但这尚未实现。
:::

### 所有飞行器模式

这些标准模式映射到所有飞行器类型。

| 标准模式                                                      | PX4 模式                                      | 内部模式 |
| ------------------------------------------------------------------ | --------------------------------------------- | ------------- |
| [MAV_STANDARD_MODE_SAFE_RECOVERY][MAV_STANDARD_MODE_SAFE_RECOVERY] | [返航模式](../flight_modes/return.md)      | AUTO_RTL      |
| [MAV_STANDARD_MODE_MISSION][MAV_STANDARD_MODE_MISSION]             | [任务模式](../flight_modes_mc/mission.md) | AUTO_MISSION  |
| [MAV_STANDARD_MODE_LAND][MAV_STANDARD_MODE_LAND]                   | [降落模式](../flight_modes_mc/land.md)       | AUTO_LAND     |
| [MAV_STANDARD_MODE_TAKEOFF][MAV_STANDARD_MODE_TAKEOFF]             | [起飞模式](../flight_modes_mc/takeoff.md) | AUTO_TAKEOFF  |

[MAV_STANDARD_MODE_SAFE_RECOVERY]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_SAFE_RECOVERY
[MAV_STANDARD_MODE_MISSION]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_MISSION
[MAV_STANDARD_MODE_LAND]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_LAND
[MAV_STANDARD_MODE_TAKEOFF]: https://mavlink.io/en/messages/common.html#MAV_STANDARD_MODE_TAKEOFF

## 标准模式实现

PX4 在适当时将其自己的自定义模式呈现为标准模式。

实现到标准模式的映射时，请参见 [src/lib/modes/standard_modes.hpp](https://github.com/PX4/PX4-Autopilot/blob/main/src/lib/modes/standard_modes.hpp)，特别是 `getNavStateFromStandardMode()` 的实现。

请注意，使用 [PX4 ROS 2 控制接口](../ros2/px4_ros2_control_interface.md) 创建的 PX4 外部模式也通过此接口公开。

<!--
- How are modes added to available modes - does a developer need to do anything particular when defining a new mode?
- How are their characteristics set?
- How do I notify when the set of modes changes? Do I need to do anything when I create a new mode?

- [PX4-Autopilot#24011: standard_modes: add vehicle-type specific standard modes](https://github.com/PX4/PX4-Autopilot/pull/24011)

-->

## 其他 MAVLink 模式更改命令

一些模式，包括标准和自定义的，也可以使用特定的命令和消息来设置。
这比仅仅启动模式更方便，特别是当消息允许配置额外设置时。

PX4 在某些飞行器类型上支持这些更改模式的命令：

- [MAV_CMD_NAV_TAKEOFF](https://mavlink.io/en/messages/common.html#MAV_CMD_NAV_TAKEOFF) — 起飞模式
- [MAV_CMD_NAV_RETURN_TO_LAUNCH](https://mavlink.io/en/messages/common.html#MAV_CMD_NAV_RETURN_TO_LAUNCH) — 返航模式
- [MAV_CMD_NAV_LAND](https://mavlink.io/en/messages/common.html#MAV_CMD_NAV_LAND) — 降落模式
- [MAV_CMD_DO_FOLLOW](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_FOLLOW) — MC 跟随模式
- [MAV_CMD_DO_FOLLOW_REPOSITION](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_FOLLOW_REPOSITION) — 跟随模式（从新位置）
- [MAV_CMD_DO_ORBIT](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_ORBIT) — MC 轨道模式
- [MAV_CMD_NAV_VTOL_TAKEOFF](https://mavlink.io/en/messages/common.html#MAV_CMD_NAV_VTOL_TAKEOFF) — VTOL 特定起飞模式
- [MAV_CMD_DO_REPOSITION](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_REPOSITION)
- [MAV_CMD_DO_PAUSE_CONTINUE](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_PAUSE_CONTINUE) — 通过将飞行器置于保持/悬停状态来暂停任务
- [MAV_CMD_MISSION_START](https://mavlink.io/en/messages/common.html#MAV_CMD_MISSION_START) — 启动任务。

请注意，这些命令早于"标准模式"，并映射到特定于飞行器的自定义模式。
这意味着即使标准模式可能适用于多种飞行器类型，该模式也可能只适用于特定飞行器。
例如，轨道标准模式在 MC 上映射到轨道模式，在 FW 上映射到保持/悬停：但在撰写本文时，`MAV_CMD_DO_ORBIT` 将在 MC 中启动轨道模式，在 FW 中被忽略。
