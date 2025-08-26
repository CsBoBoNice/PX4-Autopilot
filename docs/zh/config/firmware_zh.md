# 加载固件

_QGroundControl_ **桌面**版本可用于将PX4固件安装到[Pixhawk系列](../getting_started/flight_controller_selection.md)飞行控制器板上。

:::warning
**在开始安装固件之前**，所有连接到飞行器的USB连接都必须_断开_（直接连接或通过数传电台连接）。
飞行器_不能_由电池供电。
:::

## 安装稳定版PX4

通常您应该使用最新_发布_版本的PX4，以便从错误修复中受益并获得最新和最棒的功能。

:::tip
这是默认安装的版本。
:::

安装PX4：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 选择**"Q"图标 > 飞行器设置 > 固件**（侧边栏）打开_固件设置_。

   ![固件断开连接](../../assets/qgc/setup/firmware/firmware_disconnected.png)

1. 通过USB将飞行控制器直接连接到您的计算机。

   ::: info
   直接连接到机器上有电源的USB端口（不要通过USB集线器连接）。
   :::

1. 选择**PX4 Pro稳定版本 vX.x.x**选项来安装最新稳定版本的PX4_为您的飞行控制器_（自动检测）。

   ![安装PX4默认版本](../../assets/qgc/setup/firmware/firmware_connected_default_px4.png)

1. 点击**确定**按钮开始更新。

   固件将继续执行许多升级步骤（下载新固件、擦除旧固件等）。
   每个步骤都会打印到屏幕上，整体进度显示在进度条上。

   ![固件升级完成](../../assets/qgc/setup/firmware/firmware_upgrade_complete.png)

   固件加载完成后，设备/飞行器将重启并重新连接。

   :::tip
   如果 _QGroundControl_ 安装FMUv2目标（在安装过程中查看控制台）并且您有较新的板，您可能需要[更新引导加载程序](#bootloader)以访问飞行控制器上的所有内存。
   :::

接下来您需要指定[飞行器机架](../config/airframe.md)（然后是传感器、无线电等）

<a id="custom"></a>

## 安装PX4主分支、测试版或自定义固件

安装不同版本的PX4：

1. 如上所述连接飞行器，并选择**PX4 Pro稳定版本 vX.x.x**。
   ![安装PX4版本](../../assets/qgc/setup/firmware/qgc_choose_firmware.png)
1. 选中**高级设置**并从下拉列表中选择版本：
   - **标准版本（稳定）：** 默认版本（即无需使用高级设置来安装此版本！）
   - **测试版（测试）：** 测试版/候选版本。
     仅在准备新版本时可用。
   - **开发者构建（主分支）：** PX4/PX4-Autopilot _主_分支的最新构建。
   - **自定义固件文件...：** 自定义固件文件（例如[您在本地构建的](../dev_setup/building_px4.md)）。
     如果您选择此选项，您将需要在下一步中从文件系统选择自定义固件。

然后固件更新继续如前所述。

<a id="bootloader"></a>

## 引导加载程序更新

Pixhawk硬件通常预装适当的引导加载程序版本。

您可能需要更新的情况是安装FMUv2固件的较新Pixhawk板。
如果 _QGroundControl_ 安装FMUv2目标（在安装过程中查看控制台），并且您有较新的板，您可能需要更新引导加载程序以访问飞行控制器上的所有内存。

![FMUv2更新](../../assets/qgc/setup/firmware/bootloader_update.jpg)

您可以按照[引导加载程序更新 > FMUv2引导加载程序更新](../advanced_config/bootloader_update.md#fmuv2-bootloader-update)中的说明进行更新。

## 更多信息

- [QGroundControl用户指南 > 固件](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/firmware.html)。
- [PX4设置视频](https://youtu.be/91VGmdSlbo4) (Youtube)
