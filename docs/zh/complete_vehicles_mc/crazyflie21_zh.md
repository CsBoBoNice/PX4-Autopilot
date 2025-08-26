# Crazyflie 2.1

<LinkedBadge type="warning" text="实验性" url="../flight_controller/autopilot_experimental.html"/>

:::warning
PX4 不生产这个（或任何）自动驾驶仪。
如有硬件支持或合规问题，请联系 [制造商](https://www.bitcraze.io/)。
:::

:::warning
Crazyflie 2.1 只能在 [稳定模式](../flight_modes_mc/manual_stabilized.md) 下飞行。
:::

Crazyflie 微型四轴飞行器系列由 Bitcraze AB 公司创造。
Crazyflie 2.1 的概述可以在 [这里找到](https://www.bitcraze.io/products/crazyflie-2-1-brushless/)。

![Crazyflie2 图片](../../assets/flight_controller/crazyflie21/crazyflie_2.1.jpg)

## 快速总结

::: info
主要硬件文档在 [这里](https://wiki.bitcraze.io/projects:crazyflie2:index)
:::

- 主系统芯片：STM32F405RG
  - CPU：168 MHz ARM Cortex M4 带单精度 FPU
  - RAM：192 KB SRAM
- nRF51822 无线电和电源管理 MCU
- BMI088 3 轴加速度计/陀螺仪
- BMP388 高精度压力传感器
- uUSB 连接器
- 机载 LiPo 充电器，提供 100mA、500mA 和 980mA 模式
- 全速 USB 设备接口
- 部分 USB OTG 功能（存在 USB OTG 但无 5V 输出）
- 8KB EEPROM

## 购买渠道

飞行器可以在这里购买：[Crazyflie 2.1](https://store.bitcraze.io/products/crazyflie-2-1) (store.bitcraze.io)

有用的外设硬件包括：

- [Crazyradio PA 2.4 GHz USB 适配器](https://store.bitcraze.io/products/crazyradio-pa)：_QGroundControl_ 和 Crazyflie 2.0 之间的无线通信
- [Breakout 扩展板](https://store.bitcraze.io/collections/decks/products/breakout-deck)：用于连接新外设的扩展板。
- [Flow 扩展板 v2](https://store.bitcraze.io/products/flow-deck-v2)：用于高度和位置控制的光流传感器和距离传感器。
- [Z-ranger 扩展板 v2](https://store.bitcraze.io/collections/decks/products/z-ranger-deck-v2)：用于高度控制的距离传感器（与 Flow 扩展板相同的传感器）。
- [Multi-ranger 扩展板](https://store.bitcraze.io/collections/decks/products/multi-ranger-deck) 多方向物体检测
- [蜂鸣器扩展板](https://store.bitcraze.io/collections/decks/products/buzzer-deck) 在系统事件（如电量不足或充电完成）时提供音频反馈。
- [Breakout 扩展板](https://store.bitcraze.io/collections/decks/products/breakout-deck)：扩展板，让您能够轻松测试新硬件而无需焊接。
- [SD卡扩展板](https://store.bitcraze.io/collections/decks/products/sd-card-deck)：高速机载日志记录到 micro SD 卡
- [罗技操纵杆](https://support.logi.com/hc/en-us/articles/360024326793--Getting-Started-Gamepad-F310)

## 组装 Crazyflie 2.1

- [Bitcraze crazyflie 2.1 入门指南](https://www.bitcraze.io/documentation/tutorials/getting-started-with-crazyflie-2-x/)。

## 刷写 PX4

::: info
这些说明只在 Ubuntu 上测试过。
:::

设置好 PX4 开发环境后，请按照以下步骤在 Crazyflie 2.1 上安装 PX4 自动驾驶仪：

1. 下载 PX4 Bootloader 的源代码：

   ```sh
   git clone https://github.com/PX4/PX4-Bootloader.git --recurse-submodules
   ```

1. 进入源代码顶层目录并使用以下命令编译：

   ```sh
   make crazyflie21_bl
   ```

1. 按照以下步骤将 Crazyflie 2.1 置于 DFU 模式：
   - 确保它最初未通电。
   - 确保电池断开连接。
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

1. 使用 _dfu-util_ 刷写 bootloader，完成后拔掉 Crazyflie 2.1：

   ```sh
   sudo dfu-util -d 0483:df11 -a 0 -s 0x08000000 -D ./build/crazyflie21_bl/crazyflie21_bl.bin
   ```

   启动 Crazyflie 2.1 时，黄色 LED 应该闪烁。

1. 下载 PX4 自动驾驶仪的源代码：

   ```sh
   git clone https://github.com/PX4/PX4-Autopilot.git
   ```

1. 进入源代码顶层目录并使用以下命令编译：

   ```sh
   cd PX4-Autopilot/
   make bitcraze_crazyflie21_default upload
   ```

1. 当提示插入设备时，插入 Crazyflie 2.1。
   黄色 LED 应该开始闪烁，表示引导加载程序模式。
   然后红色 LED 应该点亮，表示刷写过程已开始。
1. 等待完成。
1. 完成！使用 [QGroundControl](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors.html) 校准传感器。

## 刷写原厂 Bitcraze 固件

1. 下载最新的 [Crazyflie 2.1 bootloader](https://github.com/bitcraze/crazyflie2-stm-bootloader/releases)
1. 按照以下步骤将 Crazyflie 2.1 置于 DFU 模式：
   - 确保它最初未通电。
   - 确保电池断开连接。
   - 按住复位按钮。
   - 插入计算机的 USB 端口。
   - 一秒后，蓝色 LED 应该开始闪烁，5 秒后应该开始闪烁得更快。
   - 释放按钮。
1. 使用 _dfu-util_ 刷写 bootloader，完成后拔掉 Crazyflie 2.1：

   ```sh
   sudo dfu-util -d 0483:df11 -a 0 -s 0x08000000 -D cf2loader-1.0.bin
   ```

   启动 Crazyflie 2.1 时，黄色 LED 应该闪烁。

1. 使用 [此](https://www.bitcraze.io/documentation/tutorials/getting-started-with-crazyflie-2-x/#update-fw) 教程安装最新的 Bitcraze Crazyflie 2.1 固件。

## 无线设置说明

机载 nRF 模块允许通过蓝牙或专有的 2.4GHz Nordic ESB 协议连接到板子。

- 推荐使用 [Crazyradio PA](https://www.bitcraze.io/crazyradio-pa/)。
- 要立即飞行 Crazyflie 2.1，支持通过蓝牙使用 Crazyflie 手机应用程序。

通过 **MAVLink** 连接：

- 使用 Crazyradio PA 与兼容的 GCS。
- 下载 _crazyflie-lib-python_ 源代码：

  ```sh
  git clone https://github.com/bitcraze/crazyflie-lib-python.git
  ```

::: info
我们将使用 [cfbridge.py](https://github.com/bitcraze/crazyflie-lib-python/blob/master/examples/cfbridge.py) 来设置 Crazyflie 2.1（刷写了 PX4）和 QGroundControl 之间的无线 MAVlink 通信链路。_Cfbridge_ 使 QGroundControl 能够与 crazyradio PA 通信。
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
  source venv/bin/activate
  ```

- 安装所需依赖项：

  ```sh
  pip install cflib
  pip install -r requirements.txt
  ```

要使用 crazyradio 连接 Crazyflie 2.1，请按照以下步骤 **启动 cfbridge**：

- 关闭并重新开启 Crazyflie 2.1 并等待其启动。
- 通过 USB 连接 Crazyflie 无线电设备。
- 导航到 crazyflie-lib-python 文件夹。
- 激活环境：

  ```sh
  source venv/bin/activate
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
QGC 中的操纵杆菜单只有在您将控制器连接到 PC 后才会出现（例如 PlayStation 3 控制器）。

![QGC 操纵杆菜单](../../assets/flight_controller/crazyflie21/joystick_menu_qgc.png)
:::

## 硬件设置

Crazyflie 2.1 只能在 [稳定模式](../flight_modes_mc/manual_stabilized.md) 下飞行。

为了记录飞行详细信息，您可以将 SD 卡扩展板安装在 crazyflie 顶部，如下所示：

![Crazyflie SD卡](../../assets/flight_controller/crazyflie21/crazyflie21_sd.jpeg)

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

要通过 MAVROS 连接到 Crazyflie 2.1：

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

## 飞行

<lite-youtube videoid="0qy7O3fVN2c" title="Crazyflie 2.1 - PX4 固件（稳定模式）"/>
