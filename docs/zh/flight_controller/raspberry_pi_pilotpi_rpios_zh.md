# 使用 Raspberry Pi OS 的 PilotPi

## 开发者快速入门

### 操作系统镜像

始终推荐使用最新的官方 [Raspberry Pi OS Lite](https://downloads.raspberrypi.org/raspios_lite_armhf_latest) 镜像。

要安装，您必须已经有一个工作的 SSH 连接到 RPi。

### 设置访问（可选）

#### 主机名和 mDNS

mDNS 帮助您使用主机名而不是 IP 地址连接到您的 RPi。

```sh
sudo raspi-config
```

导航到 **Network Options > Hostname**。
设置并退出。
您可能也想设置[免密认证](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md)。

### 设置操作系统

#### config.txt

```sh
sudo nano /boot/config.txt
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

```sh
sudo raspi-config
```

**Interfacing Options > Serial > login shell = No > hardware = Yes**。
启用 UART 但不在其上使用登录 shell。

```sh
sudo nano /boot/cmdline.txt
```

在最后一个单词后追加 `isolcpus=2`。
整个文件应该是：

```sh
console=tty1 root=PARTUUID=xxxxxxxx-xx rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait isolcpus=2
```

这告诉 Linux 内核不要在 CPU 核心 2 上调度任何进程。
我们稍后将手动在该核心上运行 PX4。

重启并 SSH 到您的 RPi。

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

检查 SPI 接口

```sh
ls /dev/spidev*
```

应该有 `/dev/spidev0.0`。

#### rc.local

在这一部分，我们将在 **rc.local** 中配置自动启动脚本。

```sh
sudo nano /etc/rc.local
```

在 `exit 0` 上方追加以下内容：

```sh
echo "25" > /sys/class/gpio/export
echo "in" > /sys/class/gpio/gpio25/direction
if [ $(cat /sys/class/gpio/gpio25/value) -eq 1 ] ; then
        echo "Launching PX4"
        cd /home/pi/px4 ; nohup taskset -c 2 ./bin/px4 -d -s pilotpi_mc.config 2 &> 1 > /home/pi/px4/px4.log &
fi
echo "25" > /sys/class/gpio/unexport
```

保存并退出。

::: info
不需要时别忘了关闭开关。
:::

#### CSI 摄像头

::: info
启用 CSI 摄像头将停止在 I2C-0 上工作的任何设备。
:::

```sh
sudo raspi-config
```

**Interfacing Options > Camera**

### 构建代码

要将_最新_版本获取到您的计算机上，请在终端中输入以下命令：

```sh
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

::: info
这就是构建最新代码所需的全部。
:::

#### 为 Raspberry Pi OS 交叉构建

使用以下方式设置您的 RPi 的 IP（或主机名）：

```sh
export AUTOPILOT_HOST=192.168.X.X
```

或

```sh
export AUTOPILOT_HOST=pi_hostname.local
```

构建可执行文件：

```sh
cd PX4-Autopilot
make scumaker_pilotpi_default
```

然后上传：

```sh
make scumaker_pilotpi_default upload
```

通过 ssh 连接并运行：

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
rm -rf build/scumaker_pilotpi_default
```

### 替代构建方法（使用 docker）

以下方法可以提供与 CI 中部署的相同工具集。

如果您第一次使用 docker 编译，请参考[官方文档](../test_and_ci/docker.md#prerequisites)。

在 PX4-Autopilot 文件夹中执行命令：

```sh
./Tools/docker_run.sh "export AUTOPILOT_HOST=192.168.X.X; export NO_NINJA_BUILD=1; make scumaker_pilotpi_default upload"
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

### 后期配置

您需要检查这些额外项目以使您的载具正常工作。

#### 执行器配置

首先为您的载具设置 [CA_AIRFRAME](../advanced_config/parameter_reference.md#CA_AIRFRAME) 参数。

然后您将能够使用正常的[执行器配置](../config/actuators.md)配置屏幕分配输出（将为 RPi PWM 输出驱动程序显示一个输出选项卡）。

#### 外部罗盘

在启动脚本（`*.config`）中，您会找到

```sh
# external GPS & compass
gps start -d /dev/ttySC0 -i uart -p ubx -s
#hmc5883 start -X
#ist8310 start -X
```

根据您的情况取消注释正确的一行。
不确定您的 GPS 模块配备了哪个罗盘？执行以下命令并查看输出：

```sh
sudo apt-get update
sudo apt-get install i2c-tools
i2cdetect -y 0
```

示例输出：

```
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- 0e --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- 1e --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --
```

`1e` 表示基于 HMC5883 的罗盘安装在外部 I2C 总线上。类似地，IST8310 的值是 `0e`。

::: info
通常您只有其中一个。
如果其他设备连接到外部 I2C 总线（`/dev/i2c-0`），它们也会在这里显示。
:::
