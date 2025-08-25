# 使用 Ubuntu Server 的 PilotPi

:::warning
RPi 4B 上的 Ubuntu Server 消耗大量电流并产生大量热量。
使用此硬件时需要设计更好的散热和高功耗方案。
:::

## 开发者快速入门

### 操作系统镜像

armhf 和 arm64 架构都受支持。

#### armhf

- [Ubuntu Server 18.04.5 for RPi2](https://cdimage.ubuntu.com/releases/18.04.5/release/ubuntu-18.04.5-preinstalled-server-armhf+raspi2.img.xz)
- [Ubuntu Server 18.04.5 for RPi3](https://cdimage.ubuntu.com/releases/18.04.5/release/ubuntu-18.04.5-preinstalled-server-armhf+raspi3.img.xz)
- [Ubuntu Server 18.04.5 for RPi4](https://cdimage.ubuntu.com/releases/18.04.5/release/ubuntu-18.04.5-preinstalled-server-armhf+raspi4.img.xz)
- [Ubuntu Server 20.04.1 for RPi 2/3/4](https://cdimage.ubuntu.com/releases/20.04.1/release/ubuntu-20.04.2-preinstalled-server-arm64+raspi.img.xz)

#### arm64

- [Ubuntu Server 18.04.5 for RPi3](https://cdimage.ubuntu.com/releases/18.04.5/release/ubuntu-18.04.5-preinstalled-server-arm64+raspi3.img.xz)
- [Ubuntu Server 18.04.5 for RPi4](https://cdimage.ubuntu.com/releases/18.04.5/release/ubuntu-18.04.5-preinstalled-server-arm64+raspi4.img.xz)
- [Ubuntu Server 20.04.1 for RPi 3/4](https://cdimage.ubuntu.com/releases/20.04.1/release/ubuntu-20.04.2-preinstalled-server-arm64+raspi.img.xz)

#### 最新操作系统

请参考官方 [cdimage](https://cdimage.ubuntu.com/releases/) 页面获取任何新更新。

### 首次启动

首次设置 RPi 的 WiFi 时，我们建议在家用路由器和 RPi 之间使用有线以太网连接，以及显示器和键盘。

#### 启动前

将 SD 卡装载到您的计算机上并修改网络设置。
请按照[这里](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#3-wifi-or-ethernet)的官方说明进行操作。

现在将 SD 卡插入您的 Pi 并首次启动。
确保您对 RPi 有 shell 访问权限 - 通过有线以太网的 SSH 连接，或使用键盘和显示器直接访问。

#### WiFi 区域

首先安装所需的包：

```sh
sudo apt-get install crda
```

编辑文件 `/etc/default/crda` 以更改正确的 WiFi 区域。[参考列表](https://arubanetworking.hpe.com/techdocs/InstantWenger_Mobile/Advanced/Content/Instant%20User%20Guide%20-%20volumes/Country_Codes_List.htm)

```sh
sudo nano /etc/default/crda
```

重启后您的 Pi 将能够加入您的 WiFi 网络。

#### 主机名和 mDNS

首先设置主机名。

```sh
sudo nano /etc/hostname
```

将主机名更改为您喜欢的任何名称。
然后安装 mDNS 所需的包：

```sh
sudo apt-get update
sudo apt-get install avahi-daemon
```

执行重启。

```sh
sudo reboot
```

完成上述操作后通过 WiFi 连接重新获得访问权限。

```sh
ssh ubuntu@pi_hostname.local
```

#### 免密认证（可选）

您可能也想设置[免密认证](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md)。

### 设置操作系统

#### config.txt

Ubuntu 中对应的文件是 `/boot/firmware/usercfg.txt`。

```sh
sudo nano /boot/firmware/usercfg.txt
```

将文件替换为：

```sh
# enable sc16is752 overlay
dtoverlay=sc16is752-spi1
# enable I2C-1 and set the frequency to 400KHz
dtparam=i2c_arm=on,i2c_arm_baudrate=400000
# enable spidev0.0
dtparam=spi=on
# enable RC input
enable_uart=1
# enable I2C-0
dtparam=i2c_vc=on
# switch Bluetooth to miniuart
dtoverlay=miniuart-bt
```

#### cmdline.txt

在 Ubuntu Server 20.04 上：

```sh
sudo nano /boot/firmware/cmdline.txt
```

在 Ubuntu Server 18.04 或更早版本上，`nobtcmd.txt` 和 `btcmd.txt` 都应该被修改。

```sh
sudo nano /boot/firmware/nobtcmd.txt
```

找到 `console=/dev/ttyAMA0,115200` 并移除该部分以禁用串行接口上的登录 shell。

在最后一个单词后追加 `isolcpus=2`。
整个文件将看起来像：

```sh
net.ifnames=0 dwc_otg.lpm_enable=0 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc isolcpus=2
```

上述行告诉 Linux 内核不要在 CPU 核心 2 上调度任何进程。
我们稍后将手动在该核心上运行 PX4。

重启并 SSH 到您的 Pi。

检查 UART 接口：

```sh
ls /dev/tty*
```

应该有 `/dev/ttyAMA0`、`/dev/ttySC0` 和 `/dev/ttySC1`。

检查 I2C 接口：

```sh
ls /dev/i2c*
```

应该有 `/dev/i2c-0` 和 `/dev/i2c-1`

检查 SPI 接口：

```sh
ls /dev/spidev*
```

应该有 `/dev/spidev0.0`。

#### rc.local

在这一部分，我们将在 **rc.local** 中配置自动启动脚本。
注意我们需要创建此文件，因为它在全新的 Ubuntu 操作系统中不存在。

```sh
sudo nano /etc/rc.local
```

将以下内容追加到文件中：

```sh
#!/bin/sh

echo "25" > /sys/class/gpio/export
echo "in" > /sys/class/gpio/gpio25/direction
if [ $(cat /sys/class/gpio/gpio25/value) -eq 1 ] ; then
        echo "Launching PX4"
        cd /home/ubuntu/px4 ; nohup taskset -c 2 ./bin/px4 -d -s pilotpi_mc.config 2 &> 1 > /home/ubuntu/px4/px4.log &
fi
echo "25" > /sys/class/gpio/unexport

exit 0
```

保存并退出。
然后设置正确的权限：

```sh
sudo chmod +x /etc/rc.local
```

::: info
不需要时别忘了关闭开关！
:::

#### CSI 摄像头

:::warning
启用 CSI 摄像头将停止在 I2C-0 上工作的任何设备。
:::

```sh
sudo nano /boot/firmware/usercfg.txt
```

在文件末尾追加以下行：

```sh
start_x=1
```

### 构建代码

要将_最新_版本获取到您的计算机上，请在终端中输入以下命令：

```sh
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

::: info
这就是构建最新代码所需的全部。
:::

#### 设置 RPi 上传目标

使用以下方式设置您的 RPi 的 IP（或主机名）：

```sh
export AUTOPILOT_HOST=192.168.X.X
```

或

```sh
export AUTOPILOT_HOST=pi_hostname.local
```

另外，我们需要设置用户名：

```sh
export AUTOPILOT_USER=ubuntu
```

#### 为 armhf 目标构建

构建可执行文件：

```sh
cd Firmware
make scumaker_pilotpi_default
```

然后上传：

```sh
make scumaker_pilotpi_default upload
```

#### armhf 的替代构建方法（使用 docker）

如果您第一次使用 docker 编译，请参考[官方文档](../test_and_ci/docker.md#prerequisites)。

在固件文件夹中执行命令：

```sh
./Tools/docker_run.sh "export AUTOPILOT_HOST=192.168.X.X; export AUTOPILOT_USER=ubuntu; export NO_NINJA_BUILD=1; make scumaker_pilotpi_default upload"
```

::: info
docker 内不支持 mDNS。上传时每次都必须指定正确的 IP 地址。
:::

::: info
如果您的 IDE 不支持 ninja 构建，`NO_NINJA_BUILD=1` 选项会有帮助。
您也可以仅编译而不上传。只需移除 `upload` 目标。
:::

也可以只编译代码：

```sh
./Tools/docker_run.sh "make scumaker_pilotpi_default"
```

#### 为 arm64 目标构建

::: info
此步骤需要安装 `aarch64-linux-gnu` 工具链。
:::

构建可执行文件：

```sh
cd PX4-Autopilot
make scumaker_pilotpi_arm64
```

然后上传：

```sh
make scumaker_pilotpi_arm64 upload
```

#### arm64 的替代构建方法（使用 docker）

如果您第一次使用 docker 编译，请参考[官方文档](../test_and_ci/docker.md#prerequisites)。

在 `PX4-Autopilot` 文件夹中执行命令：

```sh
./Tools/docker_run.sh "export AUTOPILOT_HOST=192.168.X.X; export AUTOPILOT_USER=ubuntu; export NO_NINJA_BUILD=1; make scumaker_pilotpi_arm64 upload"
```

::: info
docker 内不支持 mDNS。上传时每次都必须指定正确的 IP 地址。
:::

::: info
如果您的 IDE 不支持 ninja 构建，`NO_NINJA_BUILD=1` 选项会有帮助。
您也可以仅编译而不上传 - 只需移除 `upload` 目标。
:::

也可以只编译代码：

```sh
./Tools/docker_run.sh "make scumaker_pilotpi_arm64"
```

#### 手动运行 PX4

通过 SSH 连接并运行：

```sh
cd px4
sudo taskset -c 2 ./bin/px4 -s pilotpi_mc.config
```

现在 PX4 以多旋翼配置启动。

如果您在 Pi 上执行 `bin/px4` 时遇到类似以下问题：

```
bin/px4: /lib/xxxx/xxxx: version `GLIBC_2.29' not found (required by bin/px4)
```

那么您应该使用 docker 编译。

在进行下一步之前，首先清除现有构建：

```sh
rm -rf build/scumaker_pilotpi_*
```

然后回到上面相应的章节。

### 后期配置

请参考[这里](raspberry_pi_pilotpi_rpios.md)的说明
