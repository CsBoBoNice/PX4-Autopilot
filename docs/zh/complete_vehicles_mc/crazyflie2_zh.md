# Crazyflie 2.0 (已停产)

<Badge type="info" text="已停产" />

:::warning
_Crazyflie 2.0_ 已经 [停产/替代](../flight_controller/autopilot_experimental.md)。
请尝试使用 [Bitcraze Crazyflie 2.1](../complete_vehicles_mc/crazyflie21.md)！
:::

:::warning

- PX4 不生产这个（或任何）自动驾驶仪。
  如有硬件支持或合规问题，请联系 [制造商](https://www.bitcraze.io/)。
- PX4 对此飞控的支持是 [实验性的](../flight_controller/autopilot_experimental.md)。
  :::

Crazyflie 微型四轴飞行器系列由 Bitcraze AB 公司创造。
Crazyflie 2.0 的概述可以在 [这里找到](https://www.bitcraze.io/crazyflie-2/)。

![Crazyflie2 图片](../../assets/flight_controller/crazyflie/crazyflie2_hero.png)

## 快速总结

::: info
主要硬件文档在这里：https://wiki.bitcraze.io/projects:crazyflie2:index
:::

- 主系统芯片：STM32F405RG
  - CPU：168 MHz ARM Cortex M4 带单精度 FPU
  - RAM：192 KB SRAM
- nRF51822 无线电和电源管理 MCU
- MPU9250 加速度计/陀螺仪/磁力计
- LPS25H 气压计

## 购买渠道

- [Crazyflie 2.0](https://store.bitcraze.io/collections/kits/products/crazyflie-2-0)。
- [Crazyradio PA 2.4 GHz USB 适配器](https://store.bitcraze.io/products/crazyradio-pa)：用于 _QGroundControl_ 和 Crazyflie 2.0 之间的无线通信。
- [Breakout 扩展板](https://store.bitcraze.io/collections/decks/products/breakout-deck)：用于连接新外设的扩展板。
- [Flow 扩展板](https://store.bitcraze.io/products/flow-deck)：包含光流传感器来测量地面运动和距离传感器来测量到地面的距离。
  这对于精确的高度和位置控制非常有用。
- [Z-ranger 扩展板](https://store.bitcraze.io/collections/decks/products/z-ranger-deck) 具有与 Flow 扩展板相同的距离传感器来测量到地面的距离。
  这对于精确的高度控制非常有用。
- [SD卡扩展板](https://store.bitcraze.io/collections/decks/products/sd-card-deck)：用于高速机载日志记录到 micro SD 卡。
- [罗技操纵杆](https://support.logi.com/hc/en-us/articles/360024326793--Getting-Started-Gamepad-F310)。

## 刷写 PX4

设置好 PX4 开发环境后，请按照以下步骤在 Crazyflie 2.0 上安装 PX4 自动驾驶仪：

1. 下载 PX4 Bootloader 的源代码：

   ```sh
   git clone https://github.com/PX4/PX4-Bootloader.git
   ```

1. 进入源代码顶层目录并使用以下命令编译：

   ```sh
   make crazyflie_bl
   ```

1. 按照以下步骤将 Crazyflie 2.0 置于 DFU 模式：
   - 确保它最初未通电。
   - 按住复位按钮（见下图...）。
     ![Crazyflie2 复位按钮](../../assets/flight_controller/crazyflie/crazyflie_reset_button.jpg)
   - 插入计算机的 USB 端口。
   - 一秒后，蓝色 LED 应该开始闪烁，5 秒后应该开始闪烁得更快。
   - 释放按钮。
1. 安装 _dfu-util_：

   ```sh
   sudo apt-get update
   sudo apt-get install dfu-util
   ```

1. 使用 _dfu-util_ 刷写 bootloader，完成后拔掉 Crazyflie 2.0：

   ```sh
   sudo dfu-util -d 0483:df11 -a 0 -s 0x08000000 -D ./build/crazyflie_bl/crazyflie_bl.bin
   ```

   启动 Crazyflie 2.0 时，黄色 LED 应该闪烁。

1. 下载 PX4 自动驾驶仪的源代码：

   ```sh
   git clone https://github.com/PX4/PX4-Autopilot.git
   ```

1. 进入源代码顶层目录并使用以下命令编译：

   ```sh
   make bitcraze_crazyflie_default upload
   ```

1. 当提示插入设备时，插入 Crazyflie 2.0。
   黄色 LED 应该开始闪烁，表示引导加载程序模式。
   然后红色 LED 应该点亮，表示刷写过程已开始。
1. 等待完成。
1. 完成！使用 [QGroundControl](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors.html) 校准传感器。

::: info
如果 QGroundControl 无法连接到飞行器，请确保在 crazyflie 的 [nuttx-config](https://github.com/PX4/PX4-Autopilot/blob/main/boards/bitcraze/crazyflie/nuttx-config/nsh/defconfig) 中将 `# CONFIG_DEV_LOWCONSOLE is not set` 替换为 `CONFIG_DEV_LOWCONSOLE=y`。
这应该使用 _menuconfig_ 来完成：

```sh
make bitcraze_crazyflie_default menuconfig
```

或 _qconfig_（在 GUI 中的 _Serial Driver Support_ 下检查 _Low-level console support_）：

```sh
make bitcraze_crazyflie_default qconfig
```

:::

## 无线设置说明

机载 nRF 模块允许通过蓝牙或专有的 2.4GHz Nordic ESB 协议连接到板子。

- 推荐使用 [Crazyradio PA](https://www.bitcraze.io/crazyradio-pa/)。
- 要立即飞行 Crazyflie 2.0，支持通过蓝牙使用 Crazyflie 手机应用程序。

使用官方 Bitcraze **Crazyflie 手机应用程序**：

- 通过蓝牙连接。
- 在设置中将模式更改为 1 或 2。
- 通过 QGroundControl 校准。

通过 **MAVLink** 连接：

- 使用 Crazyradio PA 与兼容的 GCS。
- 下载 _crazyflie-lib-python_ 源代码：

  ```sh
  git clone https://github.com/bitcraze/crazyflie-lib-python.git
  ```

::: info
我们将使用 [cfbridge.py](https://github.com/bitcraze/crazyflie-lib-python/blob/master/examples/cfbridge.py) 来设置 Crazyflie 2.0（刷写了 PX4）和 QGroundControl 之间的无线 MAVlink 通信链路。_Cfbridge_ 使 QGroundControl 能够与 crazyradio PA 通信。
[基于 C 的 cfbridge](https://github.com/dennisss/cfbridge) 目前存在数据丢失问题，这就是我们选择使用 **cfbridge.py** 的原因。
:::

- 确保您已设置 udev 权限以使用 USB 无线电。为此，请按照 [此处](https://www.bitcraze.io/documentation/repository/crazyflie-lib-python/master/installation/usb_permissions/) 列出的步骤进行操作，并 **重启** 您的计算机。
- 通过 USB 连接 Crazyradio PA。
- 使用以下方法构建带有包依赖项的 [虚拟环境（本地 python 环境）](https://virtualenv.pypa.io/en/latest/)：

  ```sh
  pip install tox --user
  ```

- 导航到 crazyflie-lib-python 文件夹并输入：

  ```sh
  make venv
  ```

- 激活虚拟环境：

  ```sh
  source venv-cflib/bin/activate
  ```

- 安装所需依赖项：

  ```sh
  pip install -r requirements.txt --user
  ```

要使用 crazyradio 连接 Crazyflie 2.0，请按照以下步骤 **启动 cfbridge**：

- 关闭并重新开启 Crazyflie 2.0 并等待其启动。
- 通过 USB 连接 Crazyflie 无线电设备。
- 导航到 crazyflie-lib-python 文件夹。
- 激活环境：

  ```sh
  source venv-cflib/bin/activate
  ```

- 导航到 examples 文件夹：

  ```sh
  cd examples
  ```

- 启动 cfbridge：

```sh
python cfbridge.py
```

::: info
_Cfbridge_ 默认尝试在通道 80 上启动无线电链路通信，crazyflie 地址为 0xE7E7E7E7E7。
如果您在同一房间内使用 [多个 crazyflies 和/或 crazyradios](https://github.com/dennisss/cfbridge/blob/master/README.md#advanced-swarming) 并希望为每个使用不同的通道和/或地址，请首先通过 USB 电缆将 crazyflie 与 QGroundControl 连接，并在 QGroundControl 中更改 syslink 参数（通道、地址）。
接下来，通过给出相同的通道和地址作为第一个和第二个参数来启动 cfbridge，例如：`python cfbridge.py 90 0x0202020202`
:::

- 打开 QGroundControl。
- 使用 _cfbridge_ 后，如果您激活了 virtualenv，可以按 `CTRL+z` 来停用它。
  大多数情况下，从同一终端再次启动 _cfbridge_ 不会连接到 crazyflie，这可以通过关闭终端并在新终端中重新启动 _cfbridge_ 来解决。

:::tip
如果您更改了 [crazyflie-lib-python](https://github.com/bitcraze/crazyflie-lib-python) 中的任何驱动程序，或者在新终端中启动 _cfbridge_ 找不到 crazyflie，您可以尝试导航到 crazyflie-lib-python 文件夹并运行下面的脚本来重新构建 cflib。

```sh
make venv
```

:::

::: info
要使用操纵杆，在 QGroundControl 中将 `COM_RC_IN_MODE` 设置为"Joystick/No RC Checks"。
校准操纵杆并将 QGroundControl 中的操纵杆消息频率设置为 5 到 14 Hz 之间的任何值（推荐 10 Hz）。
要能够设置频率，应启用高级选项。
这是操纵杆命令从 QGroundControl 发送到 Crazyflie 2.0 的速率（为此，您需要按照 [此处](https://github.com/mavlink/qgroundcontrol) 的说明获取最新的 QGroundControl 源代码（master）并构建它）。
:::

![](../../assets/hardware/joystick-message-frequency.png)

## 硬件设置

Crazyflie 2.0 能够在 [稳定模式](../flight_modes_mc/manual_stabilized.md)、[高度模式](../flight_modes_mc/altitude.md) 和 [位置模式](../flight_modes_mc/position.md) 中精确控制飞行。

- 您需要 [Z-ranger 扩展板](https://store.bitcraze.io/collections/decks/products/z-ranger-deck) 来在 _高度_ 模式下飞行。
  如果您还想在 _位置_ 模式下飞行，建议您购买 [Flow 扩展板](https://store.bitcraze.io/products/flow-deck)，它也集成了 Z-ranger 传感器。
- 机载气压计对包括 Crazyflie 自己的螺旋桨产生的外部风干扰非常敏感。因此，我们用一块泡沫隔离气压计，然后将距离传感器安装在其顶部，如下所示：

![Crazyflie 气压计](../../assets/flight_controller/crazyflie/crazyflie_barometer.jpg)

![Crazyflie 气压计泡沫](../../assets/flight_controller/crazyflie/crazyflie_baro_foam.jpg)

![Crazyflie 光流](../../assets/flight_controller/crazyflie/crazyflie_opticalflow.jpg)

为了记录飞行详细信息，您可以将 SD 卡扩展板安装在 crazyflie 顶部，如下所示：

![Crazyflie SD卡](../../assets/flight_controller/crazyflie/crazyflie_sdcard.jpg)

然后，您需要使用双面胶带将电池粘贴在 SD 卡扩展板顶部：

![Crazyflie 电池设置](../../assets/flight_controller/crazyflie/crazyflie_battery_setup.jpg)

## 高度控制

如果您使用 [Z-ranger 扩展板](https://store.bitcraze.io/collections/decks/products/z-ranger-deck)，Crazyflie 能够在 _高度_ 模式下飞行。
根据数据手册，测距仪能够感应的最大高度（地面以上）为 2 米。但是，在深色表面上测试时，该值降至 0.5 米。在浅色地板上，最高可达 1.3 米。这意味着您无法在 _高度_ 或 _位置_ 飞行模式中保持高于此值的高度。

:::tip
如果 Crazyflie 2.0 在 _高度模式_ 或 _位置模式_ 中以中等油门指令出现高度漂移，请先尝试重启飞行器。如果这不能解决问题，请重新校准加速度计和磁力计（指南针）。
:::

::: info
由于机载气压计对 Crazyflie 自己的螺旋桨产生的风干扰非常敏感，您无法依靠它来保持高度。
:::

## 位置控制

使用 [Flow 扩展板](https://store.bitcraze.io/products/flow-deck)，您可以在 _位置模式_ 下飞行 Crazyflie 2.0。
与 [PX4FLOW](../sensor/px4flow.md) 不同，flow 扩展板不包含陀螺仪，因此使用机载陀螺仪进行流融合以找到本地位置估计。
此外，flow 扩展板与 SD 卡扩展板共享同一 SPI 总线，因此在 _位置模式_ 下飞行时不建议在 SD 卡上进行高速率日志记录。

## 使用 FrSky Taranis 遥控发射机作为操纵杆

如果您已经拥有 Taranis 遥控发射机并希望将其用作控制器，可以将其配置为 USB 操纵杆：

- 在 Taranis 中创建新模型。

  ![Taranis - 新模型](../../assets/flight_controller/crazyflie/taranis_model.jpg)

- 在 _MODEL SETUP_ 菜单页面中，关闭内部和外部 TX 模块。

  ![Taranis - 模型设置](../../assets/flight_controller/crazyflie/taranis_model_setup.jpg)

- 在 _OUTPUTS_ 菜单页面（在某些 Taranis 发射机中也称为"SERVOS"页面）中，反转油门（CH1）和副翼（CH3）。

  ![Taranis - 输出](../../assets/flight_controller/crazyflie/taranis_outputs.jpg)

要使用 Taranis 开关进行解锁/锁定和切换到不同的飞行模式：

- 在 Taranis UI _MIXER_ 菜单页面中，您可以将开关分配给通道 9-16 范围内的任何通道，这些通道映射到 QGroundControl 操纵杆设置中的按钮 0-7。例如，Taranis "SD" 开关可以在 Taranis UI 中设置为通道 9：

  ![Taranis 开关设置](../../assets/flight_controller/crazyflie/taranis_switch_setup.jpg)

- 使用 USB 电缆将 Taranis 连接到 PC 并打开 QGroundControl。
- 在 QGroundControl 操纵杆设置中，当您打开开关时，您可以看到按钮变黄。例如，Taranis 中的通道 9 映射到 QGroundControl 操纵杆设置中的按钮 0。您可以为此按钮分配任何模式，例如 _高度_ 模式。现在当您将开关"SD"置于低位时，飞行模式将切换到 _高度_。

  ![操纵杆设置](../../assets/flight_controller/crazyflie/crazyflie_QGCjoystick_setup.png)

### ROS

要通过 MAVROS 连接到 Crazyflie 2.0：

- 使用上述说明启动 _cfbridge_。
- 更改 QGroundControl 监听的 UDP 端口：
  - 在 QGroundControl 中，导航到 **Application Settings > General** 并取消选中 _Autoconnect to the following devices_ 下的所有框。
  - 在 **Comm Links** 中添加一个类型为 _UDP_ 的链接，选中 _Automatically Connect on Start_ 选项，将 _Listening Port_ 更改为 14557，添加 Target Hosts: 127.0.0.1，然后按 **OK**。
- 确保您已安装 [MAVROS](https://github.com/mavlink/mavros/tree/master/mavros#installation)。
- 使用命令启动 MAVROS：

  ```sh
  roslaunch mavros px4.launch fcu_url:="udp://:14550@127.0.0.1:14551" gcs_url:="udp://@127.0.0.1:14557"
  ```

- 如果不连接，请重启 QGroundControl。
