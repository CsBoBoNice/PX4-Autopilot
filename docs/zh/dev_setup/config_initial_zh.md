# 初始设置与配置

我们建议开发者获取以下所述的基本设备和软件（或类似设备）

## 基本设备

:::tip
PX4 可以与比此处描述的更广泛的设备一起使用，但新开发者将受益于选择标准设置之一。
一个 Taranis RC 和一个中端 Android 平板电脑可以组成一个非常便宜的野外工具包。
:::

强烈推荐以下设备：

- **用于安全飞行员的 RC 控制器**
  - [Taranis Plus](https://www.frsky-rc.com/product/taranis-x9d-plus-2/) RC 控制器（或等效产品）
- **开发计算机**

  ::: info
  所列计算机的性能是可以接受的，但建议使用更现代、更强大的计算机。
  :::

  - 运行 Windows 11 的联想 Thinkpad i5 核心
  - 2015 年初及以后的 MacBook Pro，搭载 macOS 10.15 或更高版本
  - 搭载 Ubuntu Linux 20.04 或更高版本的联想 Thinkpad i5

- **地面控制站**（计算机或平板电脑）：
  - iPad（可能需要 Wifi 数传适配器）
  - 任何 MacBook 或 Ubuntu Linux 笔记本电脑（可以是开发计算机）
  - 最近的中端 Android 平板电脑或手机，屏幕足够大以有效运行 _QGroundControl_（6 英寸）。
- **能够运行 PX4 的载具**：
  - [购买预构建载具](../complete_vehicles_mc/index.md)
  - [自己组装](../frames_multicopter/kits.md)
- **护目镜**
- **系留绳**（仅限多旋翼 - 用于更高风险的测试）

## 载具配置

为 **桌面操作系统** 安装 [QGroundControl 每日构建版](../dev_setup/qgc_daily_build.md)。

配置载具：

1. [安装 PX4 固件](../config/firmware.md#installing-px4-main-beta-or-custom-firmware)（包括包含您自己更改的“自定义”固件）。
1. 从 [机型参考](../airframes/airframe_reference.md) 中选择最匹配您载具的 [机型](../config/airframe.md)。
1. [基本配置](../config/index.md) 解释了如何执行基本配置。
1. [参数配置](../advanced_config/parameters.md) 解释了如何查找和修改单个参数。

::: info

- _QGroundControl_ 移动版变体不支持载具配置。
- _每日构建版_ 包含在官方发布版本中不可用的开发工具和新功能。
- 机型参考中的配置已在真实载具上飞行过，是“起飞”的良好起点。

:::