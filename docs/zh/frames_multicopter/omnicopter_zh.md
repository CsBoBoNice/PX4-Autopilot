# 全向飞行器

全向飞行器是一种可以在所有方向提供推力的多旋翼飞行器（6个自由度）。
这使得它可以在任何方向移动而不必倾斜，并且可以以任意倾斜角度悬停。
所有这些都是通过以特定方式安排电机位置和推力轴来实现的：

![全向飞行器](../../assets/airframes/multicopter/omnicopter/frame.jpg)

这个构建遵循了[Brescianini, Dario, and Raffaello D'Andrea](https://www.youtube.com/watch?v=sIi80LMLJSY)的原始设计。

## 物料清单

这个构建需要的组件有：

- 电子设备：
  - 飞行控制器：[Holybro KakuteH7](../flight_controller/kakuteh7.md)
  - 配合2个 [Tekko32 F4 4in1 电调](https://holybro.com/products/tekko32-f4-4in1-50a-esc)
    ::: info
    您可以选择自己喜欢的飞行控制器，只需要支持8个DShot输出即可。
    :::
  - GPS：[ZED-F9P](https://gnss.store/zed-f9p-gnss-modules/105-elt0092.html)
  - [GPS螺旋天线](https://gnss.store/gnss-rtk-multiband-antennas/28-elt0014.html)
    ::: info
    任何其他GPS也可以工作，但是螺旋天线预计在倒飞时性能更好。
    :::
  - 任何遥控接收器
  - 外部磁力计。我们使用了[RM-3100](https://store-drotek.com/893-professional-grade-magnetometer-rm3100.html)。
  - 数传链路，例如[WiFi](../telemetry/telemetry_wifi.md)
- 推进系统：
  - 电机：8个 [BrotherHobby LPD 2306.5 2000KV/2450KV/2650KV](https://www.getfpv.com/brotherhobby-lpd-2306-5-2000kv-2450kv-2650kv-motor.html)
  - 3D螺旋桨：2个 [HQProp 3D 5X3.5X3 3叶螺旋桨（4个装）](https://www.getfpv.com/hqprop-3d-5x3-5x3-3-blade-propeller-set-of-4.html) 或 2个 [Gemfan 513D 3叶3D螺旋桨（4个装）](https://www.getfpv.com/gemfan-513d-durable-3-blade-propeller-set-of-4.html)
  - 电池：我们使用了6S 3300mAh锂电池。确保检查尺寸以便适合机架。
  - 电池绑带
- 机架：
  - 碳纤维方管 R 8mm X 7mm X 1000mm，例如[这里在shop.swiss-composite.ch](https://shop.swiss-composite.ch/pi.php/Halbfabrikate/Rohre/Vierkant-Rohre/CFK-Vierkantrohr-8x8-7x7mm.html)
  - 碳纤维杆 R 3mm X 2mm X 1000mm，例如[这里在shop.swiss-composite.ch](https://shop.swiss-composite.ch/pi.php/Halbfabrikate/Rohre/CFK-Rohre-pultrudiert-pullwinding/Carbon-Microtubes-100cm-x-20-3mm.html)
  - 所需长度：
    - 方管：8根248mm长度
    - 杆：12根328mm，6根465mm
  - 螺丝：
    - 电机和支柱：40个 M3x12mm
  - 飞控安装：4个 M3x35mm，4个 M3螺母
  - 支柱：4个 40mm
- [3D模型](https://cad.onshape.com/documents/eaff30985f1298dc6ce8ce13/w/2f662e604240c4082682e5e3/e/ad2b2245b73393cf369132f7)

![零件清单](../../assets/airframes/multicopter/omnicopter/parts_list.jpg)

## 组装

### 机架

- 打印3D零件
  ::: info
  角件的方向很重要。
  如果方向错误，您会注意到杆的角度不正确。
  :::
- 切割杆
- 通过将机架零件连接在一起来测试一切是否正常：

  ![机架](../../assets/airframes/multicopter/omnicopter/frame_only.jpg)

- 将电机尽可能远地放置，确保螺旋桨不会碰到杆。

### 电子设备

将外设焊接到飞行控制器。我们使用了以下分配：

- 电调：2个电调可以直接连接到KakuteH7的两个连接器。
  为了避免冲突，我们从其中一个连接器上移除了电源引脚（最右边的引脚）。
- 数传到UART1
- GPS到UART4
- 遥控到UART6
  ![飞控特写](../../assets/airframes/multicopter/omnicopter/fc_closeup.jpg)

备注：

- 确保磁力计远离电源。
  我们最终将其放置在中心件的底部，用4cm厚的泡沫填充。
- 在气压计上贴一些胶带（不要封住开口！）以避免光线的影响。
- 我们没有粘合机架。
  在初始试飞后这样做当然是明智的，但也可能在不粘合的情况下工作。

## 软件配置

### 电调

首先，将电调配置为3D模式（双向）。
我们在3D模式下使用原始电调设置时遇到了问题：当尝试切换方向时，电机有时不再启动，直到电调重启。
所以我们必须更改电调设置。

为此，您可以在飞行控制器上使用Betaflight，然后使用直通模式和BL Heli套件（确保在Betaflight中配置了具有8个电机的机架）。
这些是设置：

![电调设置](../../assets/airframes/multicopter/omnicopter/esc_settings.png)

特别是：

- 将电机方向设置为**双向软件**
- 将启动功率增加到**100%**（这是保守的，可能会降低效率）

::: info
确保电机在更改设置后不会过热。
:::

### PX4

- 选择通用多旋翼机架
- 使用[解锁开关](../advanced_config/prearm_arm_disarm.md#arming-button-switch)，不要使用摇杆解锁
- [选择DShot](../config/actuators.md)作为所有八个输出的输出协议
- 根据以下方式配置电机：
  ![电机配置](../../assets/airframes/multicopter/omnicopter/motors_configuration.png)
  我们使用了以下约定：电机面向轴指向的方向。
  旋转方向与正推力方向匹配（向上移动电机滑块）。
  确保使用正确的螺旋桨，因为有CCW和CW版本。
- 参数：
  - 更改去饱和逻辑以实现更好的姿态跟踪：将[CA_METHOD](../advanced_config/parameter_reference.md#CA_METHOD)设置为0。
  - 禁用故障检测：将[FD_FAIL_P](../advanced_config/parameter_reference.md#FD_FAIL_P)和[FD_FAIL_R](../advanced_config/parameter_reference.md#FD_FAIL_R)设置为0。
- [此文件](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/airframes/multicopter/omnicopter/omnicopter.params)包含所有相关参数。

## 视频

<lite-youtube videoid="nsPkQYugfzs" title="PX4 Based Omnicopter Using the New Dynamic Control Allocation in v1.13"/>

## 仿真

Gazebo Classic中有一个全向飞行器仿真目标：

```sh
make px4_sitl gazebo-classic_omnicopter
```

![Gazebo仿真](../../assets/airframes/multicopter/omnicopter/gazebo.png)

## 备注

一些一般性备注：

- 悬停油门约为30%。
- 飞行时间约为4-5分钟。通过使用更大的螺旋桨可能可以稍微改善这一点。
