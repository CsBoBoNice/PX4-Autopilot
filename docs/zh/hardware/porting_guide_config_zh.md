# PX4 板载配置（Kconfig）

PX4 自动驾驶仪固件可以在构建时配置，以适应专门的应用（固定翼、多旋翼、地面车辆或更多），启用新的和实验性功能（如 Cyphal）或通过禁用某些驱动程序和子系统来节省闪存和内存使用。
此配置通过 _Kconfig_ 处理，这是 [NuttX 使用的相同配置系统](../hardware/porting_guide_nuttx.md#nuttx-menuconfig-setup)。

配置选项（通常被 _kconfig_ 语言称为"符号"）在 **/src** 目录下的 `Kconfig` 文件中定义。

## PX4 Kconfig 符号命名约定

按照惯例，模块/驱动程序的符号根据模块文件夹路径命名。
例如，位于 `src/drivers/adc/board_adc` 的 ADC 驱动程序的符号必须命名为 `DRIVERS_ADC_BOARD_ADC`。

要为驱动程序/模块特定选项添加符号，命名约定是模块名称后跟选项名称。
例如 `UAVCAN_V1_GNSS_PUBLISHER`，这是 `UAVCAN_V1` 模块的选项 `GNSS_PUBLISHER`。
选项必须在 `if` 语句后面保护，以确保只有在模块本身启用时选项才可见。

完整示例：

```
menuconfig DRIVERS_UAVCAN_V1
    bool "UAVCANv1"
    default n
    ---help---
        Enable support for UAVCANv1

if DRIVERS_UAVCAN_V1
    config UAVCAN_V1_GNSS_PUBLISHER
        bool "GNSS Publisher"
        default n
endif #DRIVERS_UAVCAN_V1
```

::: info
构建将静默忽略 `*.px4board` 配置文件中任何缺失或拼写错误的模块。
:::

## PX4 Kconfig 标签继承

每个 PX4 板载必须有一个 `default.px4board` 配置，并且可以有一个可选的 `bootloader.px4board` 配置。
但是，您也可以在不同标签下添加单独的配置，例如 `cyphal.px4board`。
请注意，默认情况下 `cyphal.px4board` 的配置继承 `default.px4board` 中设置的所有设置。
当更改 `cyphal.px4board` 时，它只存储与 `default.px4board` 相比不同的 Kconfig 键的增量，这对简化配置管理很有用。

::: info
当在 `default.px4board` 中修改 Kconfig 键时，同一板载的所有具有相同配置的派生配置中也会修改它。
:::

## PX4 Menuconfig 设置

[menuconfig](https://pypi.org/project/kconfiglib/#menuconfig-interfaces) 工具用于修改 PX4 板载配置，添加/删除模块、驱动程序和其他功能。

有命令行和 GUI 变体，两者都可以使用 PX4 构建快捷方式启动：

```
make px4_fmu-v5_default boardconfig
make px4_fmu-v5_default boardguiconfig
```

::: info
_Kconfiglib_ 和 _menuconfig_ 随 _kconfiglib_ python 包提供，该包由正常的 [ubuntu.sh](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/setup/ubuntu.sh) 安装脚本安装。
如果未安装 _kconfiglib_，您可以使用命令安装：`pip3 install kconfiglib`
:::

命令行和 GUI 界面如下所示。

### menuconfig GUI 界面

![menuconfig GUI interface](../../assets/hardware/kconfig-menuconfig.png)

### menuconfig 命令行界面

![menuconfig command line interface](../../assets/hardware/kconfig-guiconfig.png)
