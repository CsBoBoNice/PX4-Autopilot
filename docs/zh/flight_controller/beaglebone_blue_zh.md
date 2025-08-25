# BeagleBone Blue

<LinkedBadge type="warning" text="实验性" url="../flight_controller/autopilot_experimental.md"/>

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://beagleboard.org/blue)。
:::

[BeagleBone Blue](https://beagleboard.org/blue) 是一台多合一的基于 Linux 的计算机。
虽然它针对机器人技术进行了优化，但这个紧凑且价格低廉的板卡具有飞行控制器所需的所有必要传感器和外设。
本主题展示如何设置板卡以使用 [librobotcontrol](https://github.com/beagleboard/librobotcontrol) 机器人包运行 PX4。

![BeagleBone - labelled diagram](../../assets/hardware/BeagleBone_Blue_balloons.jpg)

## 操作系统镜像

_BeagleBone Blue_ 镜像可以在这里找到：

- [最新稳定操作系统镜像](https://beagleboard.org/latest-images)。
- [测试版操作系统镜像](https://rcn-ee.net/rootfs/bb.org/testing/)（更新频繁）。

关于刷写操作系统镜像的信息可以在[此页面](https://github.com/beagleboard/beaglebone-blue/wiki/Flashing-firmware)找到。
其他有用信息可以在 [FAQ](<https://github.com/beagleboard/beaglebone-blue/wiki/Frequently-Asked-Questions-(FAQ)>) 中找到。

:::tip
您可以选择更新到实时内核，如果这样做，请重新检查 _librobotcontrol_ 是否能与实时内核正常工作。
:::

更新本文档时的最新操作系统镜像是 [AM3358 Debian 10.3 2020-04-06 4GB SD IoT](https://www.beagleboard.org/distros/am3358-debian-10-3-2020-04-06-4gb-sd-iot)。

## 交叉编译构建（推荐）

为 _BeagleBone Blue_ 构建 PX4 的推荐方法是在开发计算机上编译，然后将 PX4 可执行二进制文件直接上传到 BeagleBone Blue。

:::tip
相比[本地构建](#native_builds)，推荐使用此方法，因为部署速度更快且易于使用。
:::

::: info
PX4 构建需要 [librobotcontrol](http://strawsondesign.com/docs/librobotcontrol/)，它会自动包含在构建中（但如果需要，可以独立安装和测试）。
:::

### Beaglebone Blue WIFI 设置

为了便于访问您的板卡，您可以通过 wifi 将其连接到您的家庭网络。

步骤如下（在板卡上执行）：

```sh
sudo su
connmanctl
connmanctl>scan wifi
connmanctl>services
#(此时您应该看到您的网络 SSID 出现。)
connmanctl>agent on
connmanctl>connect <SSID>
	输入密码
connmanctl>quit
```

::: info
上面 `<SSID>` 的格式通常是文本 'wifi' 后跟其他字符串。
输入命令后，系统会提示您输入 wifi 密码。
:::

### BeagleBone 上的 SSH root 登录

可以在板卡上启用 root 登录：

```sh
sudo su
echo "PermitRootLogin yes" >>  /etc/ssh/sshd_config && systemctl restart sshd
```

### 交叉编译器设置

1. 首先设置 _rsync_（这用于通过网络 - WiFi 或以太网将文件从开发计算机传输到目标板卡）。
   对于通过 SSH 使用密钥身份验证的 _rsync_，请按照以下步骤操作（在开发机器上）：
   1. 如果您以前没有生成过 SSH 密钥，请生成一个：

      ```
      ssh-keygen -t rsa
      ```

      1. ENTER //无密码短语
      1. ENTER
      1. ENTER

   1. 在 **/etc/hosts** 中将 BeagleBone Blue 板卡定义为 `beaglebone`，并将公共 SSH 密钥复制到板卡以实现无密码 SSH 访问：

      ```
      ssh-copy-id debian@beaglebone
      ```

   1. 或者您可以直接使用 beaglebone 的 IP：

      ```
      ssh-copy-id debian@<IP>
      ```

   1. 当提示是否信任时：yes
   1. 输入 root 密码

1. 交叉编译设置
   1. 工具链下载
      1. 首先将工具链安装到 _/opt/bbblue_toolchain/gcc-arm-linux-gnueabihf_。
         以下是使用软链接选择要使用的工具链版本的示例：

         ```sh
         mkdir -p /opt/bbblue_toolchain/gcc-arm-linux-gnueabihf
         chmod -R 777 /opt/bbblue_toolchain
         cd /opt/bbblue_toolchain/gcc-arm-linux-gnueabihf
         ```

         _BeagleBone Blue_ 的 ARM 交叉编译器可以在 [Linaro Toolchain Binaries 站点](https://www.linaro.org/downloads/#gnu_and_llvm)找到。

         :::tip
         工具链中的 GCC 应该与 _BeagleBone Blue_ 中的内核兼容。
         一般经验法则是选择 GCC 版本不高于 _BeagleBone Blue_ 操作系统镜像中 GCC 版本的工具链。
         :::

         下载并解压 [gcc-linaro-13.0.0-2022.06-x86_64_arm-linux-gnueabihf.tar.xz](https://snapshots.linaro.org/gnu-toolchain/13.0-2022.06-1/arm-linux-gnueabihf/gcc-linaro-13.0.0-2022.06-x86_64_arm-linux-gnueabihf.tar.xz) 到 bbblue_toolchain 文件夹。

         _BeagleBone Blue_ 的不同 ARM 交叉编译器版本可以在 [Linaro Toolchain Binaries 站点](https://www.linaro.org/downloads/)找到。

         ```sh
         wget https://snapshots.linaro.org/gnu-toolchain/13.0-2022.06-1/arm-linux-gnueabihf/gcc-linaro-13.0.0-2022.06-x86_64_arm-linux-gnueabihf.tar.xz
         tar -xf gcc-linaro-13.0.0-2022.06-x86_64_arm-linux-gnueabihf.tar.xz
         ```

         :::tip
         工具链的 GCC 版本应该与 _BeagleBone Blue_ 中的内核兼容。
         :::

         一般经验法则是选择 GCC 版本不高于 _BeagleBone Blue_ 操作系统镜像中 GCC 版本的工具链。

      1. 将其添加到 ~/.profile 中的 PATH，如下所示

         ```sh
         export PATH=$PATH:/opt/bbblue_toolchain/gcc-arm-linux-gnueabihf/gcc-linaro-13.0.0-2022.06-x86_64_arm-linux-gnueabihf/bin
         ```

         ::: info
         注销并登录以应用更改，或在当前 shell 中执行相同的行。
         :::

      1. 通过下载 PX4 源代码然后运行设置脚本来设置其他依赖项：

         ````
         git clone https://github.com/PX4/PX4-Autopilot.git --recursive
         cd PX4-Autopilot
         bash ./Tools/setup/ubuntu.sh
         ```

         您可能需要编辑上传目标以匹配您的设置：

         ```sh
         nano PX4-Autopilot/boards/beaglebone/blue/cmake/upload.cmake

         # 在第 37 行将 debian@beaglebone.lan 更改为 root@beaglebone（或 root@<IP>）
         ````

         有关附加信息，请参阅[开发环境设置](../dev_setup/dev_env_linux_ubuntu.md)说明。

### 交叉编译和上传

编译和上传

```
make beaglebone_blue_default upload
```

::: info
如果没有上传，文件存储在本地构建文件夹中。
:::

要测试上传的文件，在 _BeagleBone Blue_ 板卡上运行以下命令：

```sh
cd /home/debian/px4
sudo ./bin/px4 -s px4.config
```

::: info
目前 _librobotcontrol_ 需要 root 访问权限。
:::

<a id="native_builds"></a>

## 本地构建（可选）

您也可以直接在 BeagleBone Blue 上本地构建 PX4。

获得预构建库后，

1. 选择 _librobotcontrol_ 安装目录，并在 `LIBROBOTCONTROL_INSTALL_DIR` 环境变量中设置，以便不包含其他不需要的头文件
1. 将 **robotcontrol.h** 和 **rc/\*** 安装到 `$LIBROBOTCONTROL_INSTALL_DIR/include`
1. 将预构建的本地（ARM）版本的 librobotcontrol.\* 安装到 `$LIBROBOTCONTROL_INSTALL_DIR/lib`

在 BeagleBone Blue 上运行以下命令（即通过 SSH）：

1. 安装依赖项：

   ```sh
   sudo apt-get update
   sudo apt-get install cmake python3-empy=3.3.4-2
   ```

1. 直接在 BeagleBone Blue 上克隆 PX4 固件。
1. 继续[标准构建系统安装](../dev_setup/dev_env_linux.md)。

## 配置更改

所有更改都可以直接在 beaglebone 上的 px4.config 文件中进行。
例如，您可以将 WIFI 更改为 wlan。

::: info
如果您想永久更改，必须在构建之前在构建机器上更改 **PX4-Autopilot/posix-configs/bbblue/px4.config**。
:::

## 启动时自动启动

这是一个 [/etc/rc.local] 示例：

```sh
#!/bin/sh -e
#
# rc.local
#
# 此脚本在每个多用户运行级别结束时执行。
# 确保脚本在成功时 "exit 0"，在错误时返回任何其他值。
#
# 要启用或禁用此脚本，只需更改执行位。
#
# 默认情况下，此脚本什么都不做。

# 等待服务启动
/bin/sleep 25

cd /home/debian/px4

/home/debian/px4/bin/px4 -d -s /home/debian/px4/px4.config > /home/debian/px4/PX4.log &

exit 0
```

下面是一个 _systemd_ 服务示例 [/lib/systemd/system/px4-quad-copter.service]：

```sh
[Unit]
Description=PX4 Quadcopter Service
After=networking.service network-online.target
StartLimitIntervalSec=0
Conflicts=px4-fixed-wing.service

[Service]
WorkingDirectory=/home/debian/px4
User=root
ExecStart=/home/debian/px4/bin/px4 -d -s /home/debian/px4/px4.config

Restart=on-failure
RestartSec=1

[Install]
WantedBy=multi-user.target
```

### 杂项

#### 电源舵机导轨

当 PX4 启动时，它会自动向舵机供电。

#### 独特功能

BeagleBone Blue 具有一些独特功能，如 WiFi 接口和电源的多种选择。
有关这些功能的使用，请参阅 **/home/debian/px4/px4.config** 中的注释。

#### SBUS 信号转换器

接收器（例如 FrSky X8R）的 SBUS 信号是反相信号。
BeagleBone Blue 上的 UART 只能使用非反相的 3.3V 电平信号。
[本教程](../tutorials/linux_sbus.md)包含 SBUS 信号反相器电路。

#### 典型连接

对于带有 GPS 和 SBUS 接收器的四旋翼，以下是典型连接：

1. 将电机 1、2、3 和 4 的 ESC 分别连接到 BeagleBone Blue 舵机输出的通道 1、2、3 和 4。
   如果您的 ESC 连接器包含电源输出引脚，请将其移除并且不要将其连接到 BeagleBone Blue 舵机通道的电源输出引脚。

1. 将上述转换后的 SBUS 信号连接到 dsm2 端口（如果您有 dsm2 的匹配连接器），否则将其连接到任何其他可用的 UART 端口，并相应地更改 **/home/debian/px4/px4.config** 中的相应端口。

1. 将 GPS 模块的信号连接到 BeagleBone Blue 上的 GPS 端口。
   注意，BeagleBone Blue 上 GPS 端口的信号引脚仅能耐受 3.3V，因此请相应地选择您的 GPS 模块。
