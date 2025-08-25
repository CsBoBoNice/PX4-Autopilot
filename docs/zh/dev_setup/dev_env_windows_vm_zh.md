# Windows 虚拟机托管工具链

:::warning
此开发环境是 [社区支持和维护的](../advanced/community_supported_dev_env.md)。
它可能适用于也可能不适用于当前版本的 PX4。

有关核心开发团队支持的环境和工具的信息，请参见 [工具链安装](../dev_setup/dev_env.md)。
:::

Windows 开发者可以在虚拟机 (VM) 中运行 PX4 工具链，以 Linux 作为客户操作系统。
设置好虚拟机后，在 VM 中安装和设置 PX4 与在原生 Linux 计算机上完全相同。

虽然使用 VM 是设置和测试构建固件环境的非常简单的方法，但用户应注意：

1. 固件构建速度将比在 Linux 上原生构建慢。
1. JMAVSim 模拟的帧率将比在原生 Linux 上慢得多。
   在某些情况下，由于 VM 资源不足，飞行器可能会崩溃。
1. 可以安装 Gazebo 和 ROS，但速度慢得无法使用。

:::tip
为 VM 分配尽可能多的 CPU 核心和内存资源。
:::

有多种方法可以在您的系统上设置能够执行 PX4 环境的 VM。
本指南将引导您完成 VMWare 设置。
最后还有一个不完整的 VirtualBox 部分（我们欢迎社区成员扩展此部分）。

## VMWare 设置

VMWare 性能对于基本使用（构建固件）是可以接受的，但对于运行 ROS 或 Gazebo Classic 则不行。

1. 下载 [VMWare Player 免费版](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html)
1. 在您的 Windows 系统上安装它
1. 下载所需版本的 [Ubuntu 桌面 ISO 镜像](https://ubuntu.com/download/desktop)。
   （请参见 [Linux 说明页面](../dev_setup/dev_env_linux.md) 了解推荐的 Ubuntu 版本）。
1. 打开 _VMWare Player_。
1. 在 VM 的设置中启用 3D 加速：**VM > Settings > Hardware > Display > Accelerate 3D graphics**

   ::: info
   此选项是正确运行 jMAVSim 和 Gazebo Classic 等 3D 模拟环境所必需的。
   我们建议在虚拟环境中安装 Linux 之前完成此操作。
   :::

1. 选择创建新虚拟机的选项。
1. 在 VM 创建向导中，选择下载的 Ubuntu ISO 镜像作为安装介质，它将自动检测您要使用的操作系统。
1. 同样在向导中，选择在 VM 运行时要分配给虚拟机的资源。
   分配尽可能多的内存和 CPU 核心，而不会使您的主机 Windows 系统无法使用。
1. 在向导结束时运行您的新 VM，并按照设置说明安装 Ubuntu。
   请记住，所有设置仅用于主机操作系统使用，因此您可以禁用任何不会增加网络攻击风险的屏幕保护程序和本地工作站安全功能。
1. 新 VM 启动后，确保在客户系统内安装 _VMWare 工具驱动程序和工具扩展_。
   这将增强 VM 使用的性能和可用性：
   - 显著增强的图形性能
   - 对硬件设备使用（如 USB 端口分配（对目标上传很重要）、正确的鼠标滚轮滚动、声音支持）的适当支持
   - 客户机显示分辨率适应窗口大小
   - 与主机系统的剪贴板共享
   - 与主机系统的文件共享

1. 继续进行 [Linux 的 PX4 环境设置](../dev_setup/dev_env_linux.md)

## VirtualBox 7 设置

VirtualBox 的设置与 VMWare 类似。
社区成员，我们欢迎在这里提供逐步指南！

### 用于 QGroundControl / 固件刷新的 USB 直通

:::tip
本节已在运行 Ubuntu 20.04 LTS 的 VirtualBox 7 和 Windows 10 主机机器上进行了测试。
:::

虚拟机的一个限制是您无法自动连接到连接到主机计算机 USB 端口的飞控，以便 [从终端构建和上传 PX4 固件](../dev_setup/building_px4.md#uploading-firmware-flashing-the-board)。
您也无法从虚拟机中的 QGroundControl 连接到飞控。

要允许这样做，您需要配置 USB 直通设置：

1. 确保已使用终端命令将用户添加到 VM 中的 dialout 组：

   ```sh
   sudo usermod -a -G dialout $USER
   ```

   然后在虚拟机中重启 Ubuntu。

1. 在 VM 中启用串行端口：**VirtualBox > Settings > Serial Ports 1/2/3/etc...**
1. 在 VM 中启用 USB 控制器：**VirtualBox > Settings > USB**
1. 在 VM 中为引导加载程序添加 USB 过滤器：**VirtualBox > Settings > USB > Add new USB filter**。
   - 打开菜单并插入连接到您的自动驾驶仪的 USB 电缆。
     当设备出现在 UI 中时选择 `...Bootloader` 设备。

     ::: info
     引导加载程序设备仅在连接 USB 后几秒钟内出现。
     如果在您选择之前它消失了，请断开连接然后重新连接 USB。
     :::

   - 当设备出现时选择 `...Autopilot` 设备（这发生在引导加载程序完成后）。

1. 在 VM 实例的下拉菜单中选择设备 **VirtualBox > Devices > your_device**

如果成功，您的设备将通过 `lsusb` 显示，并且 QGroundControl 将自动连接到设备。
您还应该能够使用如下命令构建和上传固件：

```sh
make px4_fmu-v5_default upload
```

### 用于 QGroundControl 的 WiFi 数传

如果在虚拟机内使用 _QGroundControl_，您应将 VM 网络设置设置为"桥接适配器"模式。
这使客户操作系统能够直接访问主机上的网络硬件。
如果您使用默认设置的网络地址转换 (NAT)（对于运行 Ubuntu 20.04 LTS 的 VirtualBox 7），这将阻止 QGroundControl 用于与飞行器通信的出站 UDP 数据包。