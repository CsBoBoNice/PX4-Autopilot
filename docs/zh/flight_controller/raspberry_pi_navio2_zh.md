# Raspberry Pi 2/3/4 Navio2 自动驾驶仪

<LinkedBadge type="warning" text="实验性" url="../flight_controller/autopilot_experimental.html"/>

:::warning
PX4不制造此飞控（或任何其他自动驾驶仪）。
如需硬件支持或合规问题，请联系[制造商](https://emlid.com/)。
:::

这是 Raspberry Pi 2/3/4 Navio2 自动驾驶仪的开发者"快速入门"。它允许您构建 PX4 并传输到 RPi，或本地构建。

![Ra Pi 图片](../../assets/hardware/hardware-rpi2.jpg)

## 操作系统镜像

使用预配置的 [Emlid Raspberry Pi OS 镜像用于 Navio 2](https://docs.emlid.com/navio2/configuring-raspberry-pi/)。默认镜像将已经完成了下面显示的大部分设置程序。

:::warning
确保不要升级系统（更具体地说是内核）。通过升级，可能会安装新的内核，缺少必要的硬件支持（您可以用 `ls /sys/class/pwm` 检查，该目录不应为空）。
:::

## 设置访问

Raspberry Pi OS 镜像已经设置了 SSH。用户名是"pi"，密码是"raspberry"。为了本指南的目的，我们假设用户名和密码保持默认值。

要设置 Pi 加入您的本地 wifi，请遵循[此指南](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md)，或通过以太网电缆连接。

要通过 SSH 连接到您的 Pi，请使用默认用户名（`pi`）和主机名（`navio`）。或者（如果这不起作用），您可以找到 RPi 的 IP 地址并指定它。

```sh
ssh pi@navio.local
```

或

```sh
ssh pi@<IP-ADDRESS>
```

## 扩展文件系统

通过运行以下命令扩展文件系统以利用整个 SD 卡：

```sh
sudo raspi-config --expand-rootfs
```

## 禁用 Navio RGB 覆层

现有的 Navio RGB 覆层占用了 PX4 用于 RGB LED 的 GPIO。通过注释启用 `navio-rgb` 覆层的行来编辑 `/boot/config.txt`。

```
#dtoverlay=navio-rgb
```

## 测试文件传输

我们使用 SCP 通过网络（WiFi 或以太网）将文件从开发计算机传输到目标板。

要测试您的设置，请尝试现在通过网络从开发 PC 推送文件到 Pi。确保 Pi 具有网络访问权限，并且您可以 SSH 到它。

```sh
echo "Hello" > hello.txt
scp hello.txt pi@navio.local:/home/pi/
rm hello.txt
```

这应该将一个"hello.txt"文件复制到您的 Pi 的家目录中。验证文件确实被复制了，您可以继续下一步。

## PX4 开发环境

这些说明解释了如何在 Ubuntu 18.04 上安装用于构建 RPi 的 PX4 开发环境。

::: warning
Navio 2 的 PX4 二进制文件只能在 Ubuntu 18.04 上运行。

您可以在 Ubuntu 20.04 上使用 GCC 工具链构建 PX4，但生成的二进制文件太新而无法在实际的 Pi 上运行（截至 2023 年 9 月）。有关更多信息，请参阅 [PilotPi with Raspberry Pi OS Developer Quick Start > Alternative build method using docker](../flight_controller/raspberry_pi_pilotpi_rpios.md#alternative-build-method-using-docker)。
:::

### 安装通用依赖项

要获取 Raspberry Pi 的通用依赖项：

1. 从 PX4 源代码库（**/Tools/setup/**）下载 [ubuntu.sh](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/setup/ubuntu.sh) <!-- NEED px4_version --> 和 [requirements.txt](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/setup/requirements.txt)： <!-- NEED px4_version -->

   ```sh
   wget https://raw.githubusercontent.com/PX4/PX4-Autopilot/main/Tools/setup/ubuntu.sh
   wget https://raw.githubusercontent.com/PX4/PX4-Autopilot/main/Tools/setup/requirements.txt
   ```

1. 在终端中运行 **ubuntu.sh** 仅获取通用依赖项：

   ```sh
   bash ubuntu.sh --no-nuttx --no-sim-tools
   ```

1. 然后设置交叉编译器（GCC 或 clang），如以下部分所述。

### GCC (armhf)

Ubuntu 软件存储库提供一组预编译的工具链。请注意，Ubuntu Focal 默认安装 `gcc-9-arm-linux-gnueabihf`，这不完全受支持，因此我们必须手动安装 `gcc-8-arm-linux-gnueabihf` 并将其设置为默认工具链。本指南也适用于较早的 Ubuntu 版本（Bionic）。以下说明假设您尚未安装任何版本的 arm-linux-gnueabihf，并将使用 `update-alternatives` 设置默认可执行文件。使用终端命令安装它们：

```sh
sudo apt-get install -y gcc-8-arm-linux-gnueabihf g++-8-arm-linux-gnueabihf
```

将它们设置为默认值：

```sh
sudo update-alternatives --install /usr/bin/arm-linux-gnueabihf-gcc arm-linux-gnueabihf-gcc /usr/bin/arm-linux-gnueabihf-gcc-8 100 --slave /usr/bin/arm-linux-gnueabihf-g++ arm-linux-gnueabihf-g++ /usr/bin/arm-linux-gnueabihf-g++-8
sudo update-alternatives --config arm-linux-gnueabihf-gcc
```

### GCC (aarch64)

如果您想为 ARM64 设备构建 PX4，则需要此部分。

```sh
sudo apt-get install -y gcc-8-aarch64-linux-gnu g++-8-aarch64-linux-gnu
sudo update-alternatives --install /usr/bin/aarch64-linux-gnu-gcc aarch64-linux-gnu-gcc /usr/bin/aarch64-linux-gnu-gcc-8 100 --slave /usr/bin/aarch64-linux-gnu-g++ aarch64-linux-gnu-g++ /usr/bin/aarch64-linux-gnu-g++-8
sudo update-alternatives --config aarch64-linux-gnu-gcc
```

### Clang（可选）

首先安装 GCC（使用 clang 需要）。

我们建议您从 Ubuntu 软件存储库获取 clang，如下所示：

```sh
sudo apt-get install clang
```

下面是使用 _CMake_ 构建 PX4 固件的树外示例。

```sh
cd <PATH-TO-PX4-SRC>
mkdir build/px4_raspberrypi_default_clang
cd build/px4_raspberrypi_default_clang
cmake \
-G"Unix Makefiles" \
-DCONFIG=px4_raspberrypi_default \
-UCMAKE_C_COMPILER \
-DCMAKE_C_COMPILER=clang \
-UCMAKE_CXX_COMPILER \
-DCMAKE_CXX_COMPILER=clang++ \
../..
make
```

## 构建代码

使用以下命令指定您的 Pi 的 IP（或主机名）：

```sh
export AUTOPILOT_HOST=navio.local
```

或

```sh
export AUTOPILOT_HOST=192.168.X.X
```

::: info
环境变量的值应在构建前设置，否则 `make upload` 将找不到您的 Pi。
:::

在您的开发机器上构建可执行文件：

```sh
cd PX4-Autopilot
make emlid_navio2
```

"px4"可执行文件位于目录 **build/emlid_navio2_default/** 中。确保您可以通过 SSH 连接到您的 Pi，请参阅[如何访问您的 Pi 的说明](#setting-up-access)，按照 Raspberry Pi 下 armhf 的说明。

然后上传它：

```sh
cd PX4-Autopilot
make emlid_navio2 upload
```

然后，通过 ssh 连接并在 Pi 上运行它（作为 root）：

```sh
cd ~/px4
sudo ./bin/px4 -s px4.config
```

成功构建后执行 PX4 将给您类似这样的结果：

```sh

______  __   __    ___
| ___ \ \ \ / /   /   |
| |_/ /  \ V /   / /| |
|  __/   /   \  / /_| |
| |     / /^\ \ \___  |
\_|     \/   \/     |_/

px4 starting.


pxh>
```

## 自动启动

要自动启动 px4，请将以下内容添加到文件 **/etc/rc.local**（如果您使用本机构建，请相应调整），就在 `exit 0` 行之前：

```sh
cd /home/pi && ./bin/px4 -d -s px4.config > px4.log
```
