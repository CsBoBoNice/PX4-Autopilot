# 构建 PX4 软件

PX4 固件可以从源代码在控制台或 IDE 中构建，适用于模拟和硬件目标。

您需要构建 PX4 才能使用 [模拟器](../simulation/index.md)，或者如果您想修改 PX4 并创建自定义构建。
如果您只想在真实硬件上试用 PX4，则可以使用 QGroundControl [加载预构建的二进制文件](../config/firmware.md)（无需遵循这些说明）。

::: info
在遵循这些说明之前，您必须首先为您的主机操作系统和目标硬件安装 [开发者工具链](../dev_setup/dev_env.md)。
如果您在遵循这些步骤后遇到任何问题，请参阅下面的 [故障排除](#troubleshooting) 部分。
:::

## 下载 PX4 源代码

PX4 源代码存储在 Github 上的 [PX4/PX4-Autopilot](https://github.com/PX4/PX4-Autopilot) 仓库中。

要将 _最新的_ (`main` 分支) 版本获取到您的计算机上，请在终端中输入以下命令：

```sh
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

请注意，您可能在安装 [开发者工具链](../dev_setup/dev_env.md) 时已经执行了此操作。

::: info
这就是获取最新代码所需的全部操作。
如果需要，您还可以 [获取特定版本的源代码](../contribute/git_examples.md#get-a-specific-release)。
[GIT 示例](../contribute/git_examples.md) 提供了更多关于使用版本和为 PX4 做贡献的信息。
:::

## 首次构建（使用模拟器）

首先，我们将在控制台环境中构建一个模拟目标。
这允许我们在转向真实硬件和 IDE 之前验证系统设置。

导航到 **PX4-Autopilot** 目录并使用以下命令启动 [Gazebo SITL](../sim_gazebo_gz/index.md)：

```sh
make px4_sitl gz_x500
```

::: details  如果您安装了 Gazebo Classic
使用以下命令启动  [Gazebo Classic SITL](../sim_gazebo_classic/index.md)：

```sh
make px4_sitl gazebo-classic
```

:::

这将启动 PX4 控制台：

![PX4 Console](../../assets/toolchain/console_gazebo.png)

::: info
在继续之前，您可能需要启动 _QGroundControl_，因为默认的 PX4 配置需要在起飞前建立地面控制连接。
可以从 [这里下载](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html)。
:::

可以通过在控制台中输入以下命令来使无人机起飞（如上图所示）：

```sh
pxh> commander takeoff
```

飞行器将起飞，您将在 Gazebo 模拟器 UI 中看到：

![Gazebo UI with vehicle taking off](../../assets/toolchain/gazebo_takeoff.png)

可以通过输入 `commander land` 来降落无人机，整个模拟可以通过 **CTRL+C**（或输入 `shutdown`）来停止。

通过地面控制站进行模拟飞行更接近于飞行器的真实操作。
在飞行器飞行时（起飞飞行模式），点击地图上的一个位置并启用滑块。
这将重新定位飞行器。

![QGroundControl GoTo](../../assets/toolchain/qgc_goto.jpg)

## NuttX / Pixhawk 基于的开发板

### 构建 NuttX

要为基于 NuttX 或 Pixhawk 的开发板构建，请导航到 **PX4-Autopilot** 目录，然后使用适用于您开发板的构建目标调用 `make`。

例如，要为 [Pixhawk 4](../flight_controller/pixhawk4.md) 硬件构建，您可以使用以下命令：

```sh
cd PX4-Autopilot
make px4_fmu-v5_default
```

成功的运行将以类似的输出结束：

```sh
-- Build files have been written to: /home/youruser/src/PX4-Autopilot/build/px4_fmu-v4_default
[954/954] Creating /home/youruser/src/PX4-Autopilot/build/px4_fmu-v4_default/px4_fmu-v4_default.px4
```

构建目标的第一部分 `px4_fmu-v4` 表示固件的目标飞控硬件。
后缀，在本例中为 `_default`，表示固件 _配置_，例如支持或省略特定功能。

::: info
`_default` 后缀是可选的。
例如，`make px4_fmu-v5` 和 `px4_fmu-v5_default` 结果相同。
:::

以下列表显示了 [Pixhawk 标准](../flight_controller/autopilot_pixhawk_standard.md) 开发板的构建命令：

- [Holybro Pixhawk 6X-RT (FMUv6X)](../flight_controller/pixhawk6x-rt.md): `make px4_fmu-v6xrt_default`
- [Holybro Pixhawk 6X (FMUv6X)](../flight_controller/pixhawk6x.md): `make px4_fmu-v6x_default`
- [Holybro Pixhawk 6C (FMUv6C)](../flight_controller/pixhawk6c.md): `make px4_fmu-v6c_default`
- [Holybro Pixhawk 6C Mini (FMUv6C)](../flight_controller/pixhawk6c_mini.md): `make px4_fmu-v6c_default`
- [Holybro Pix32 v6 (FMUv6C)](../flight_controller/holybro_pix32_v6.md): `make px4_fmu-v6c_default`
- [Holybro Pixhawk 5X (FMUv5X)](../flight_controller/pixhawk5x.md): `make px4_fmu-v5x_default`
- [Pixhawk 4 (FMUv5)](../flight_controller/pixhawk4.md): `make px4_fmu-v5_default`
- [Pixhawk 4 Mini (FMUv5)](../flight_controller/pixhawk4_mini.md): `make px4_fmu-v5_default`
- [CUAV V5+ (FMUv5)](../flight_controller/cuav_v5_plus.md): `make px4_fmu-v5_default`
- [CUAV V5 nano (FMUv5)](../flight_controller/cuav_v5_nano.md): `make px4_fmu-v5_default`
- [Pixracer (FMUv4)](../flight_controller/pixracer.md): `make px4_fmu-v4_default`
- [Pixhawk 3 Pro](../flight_controller/pixhawk3_pro.md): `make px4_fmu-v4pro_default`
- [Pixhawk Mini](../flight_controller/pixhawk_mini.md): `make px4_fmu-v3_default`
- [Pixhawk 2 (Cube Black) (FMUv3)](../flight_controller/pixhawk-2.md): `make px4_fmu-v3_default`
- [mRo Pixhawk (FMUv3)](../flight_controller/mro_pixhawk.md): `make px4_fmu-v3_default` (支持 2MB 闪存)
- [Holybro pix32 (FMUv2)](../flight_controller/holybro_pix32.md): `make px4_fmu-v2_default`
- [Pixfalcon (FMUv2)](../flight_controller/pixfalcon.md): `make px4_fmu-v2_default`
- [Dropix (FMUv2)](../flight_controller/dropix.md): `make px4_fmu-v2_default`
- [Pixhawk 1 (FMUv2)](../flight_controller/pixhawk.md): `make px4_fmu-v2_default`

  :::warning
  您 **必须** 使用受支持版本的 GCC 来构建此开发板（例如，与 [CI/docker](../test_and_ci/docker.md) 使用的相同版本），否则需要从构建中移除模块。使用不受支持的 GCC 可能会失败，因为 PX4 接近开发板的 1MB 闪存限制。
  :::

- 具有 2 MB 闪存的 Pixhawk 1：`make px4_fmu-v3_default`

非 Pixhawk 的 NuttX 飞控（以及其他所有开发板）的构建命令在各个 [飞控开发板](../flight_controller/index.md) 的文档中提供。

### 上传固件（刷新开发板）

在 make 命令末尾附加 `upload` 可通过 USB 将编译好的二进制文件上传到飞控硬件。
例如

```sh
make px4_fmu-v4_default upload
```

成功的运行将以如下输出结束：

```sh
Erase  : [====================] 100.0%
Program: [====================] 100.0%
Verify : [====================] 100.0%
Rebooting.

[100%] Built target upload
```

::: tip
在基于 WSL2 的开发环境中不支持此功能。
请参阅 [Windows 开发环境 (基于 WSL2) > 刷新飞控](../dev_setup/dev_env_windows_wsl.md#flash-a-flight-control-board)。
:::

## 其他开发板

其他开发板的构建命令在 [特定开发板飞控页面](../flight_controller/index.md) 中给出（通常在 _构建固件_ 标题下）。

您也可以使用以下命令列出所有配置目标：

```sh
make list_config_targets
```

## 在图形化 IDE 中编译

[VSCode](../dev_setup/vscode.md) 是 PX4 开发官方支持（并推荐）的 IDE。
它易于设置，并且可以用于为模拟和硬件环境编译 PX4。

## 故障排除

### 一般构建错误

许多构建问题是由子模块不匹配或构建环境清理不彻底引起的。
更新子模块并执行 `distclean` 可以解决这类错误：

```sh
git submodule update --recursive
make distclean
```

### Flash 超出 XXX 字节

`region 'flash' overflowed by XXXX bytes` 错误表明固件对于目标硬件平台来说太大。
这在 `make px4_fmu-v2_default` 构建中很常见，其中闪存大小限制为 1MB。

如果您正在构建 _vanilla_ 主分支，最可能的原因是使用了不受支持的 GCC 版本。
在这种情况下，请安装 [开发者工具链](../dev_setup/dev_env.md) 说明中指定的版本。

如果您正在构建自己的分支，可能是您增加了固件大小，超过了 1MB 的限制。
在这种情况下，您需要从构建中移除不需要的驱动程序/模块。

### macOS: 打开文件过多错误

MacOS 默认允许所有运行进程最多打开 256 个文件。
PX4 构建系统会打开大量文件，因此您可能会超过这个数量。

然后构建工具链会报告许多文件的 `Too many open files`，如下所示：

```sh
/usr/local/Cellar/gcc-arm-none-eabi/20171218/bin/../lib/gcc/arm-none-eabi/7.2.1/../../../../arm-none-eabi/bin/ld: cannot find NuttX/nuttx/fs/libfs.a: Too many open files
```

解决方案是增加允许打开的最大文件数（例如增加到 300）。
您可以在 macOS _Terminal_ 中为每个会话执行此操作：

- 运行此脚本 [Tools/mac_set_ulimit.sh](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/mac_set_ulimit.sh)，或者
- 输入此命令：

  ```sh
  ulimit -S -n 300
  ```

### macOS Catalina: cmake 运行问题

在 macOS Catalina 10.15.1 中，尝试使用 _cmake_ 构建模拟器时可能会出现问题。
如果在此平台上遇到构建问题，请尝试在终端中运行以下命令：

```sh
xcode-select --install
sudo ln -s /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/* /usr/local/include/
```

### Ubuntu 18.04: 编译错误涉及 arm_none_eabi_gcc

与 `arm_none_eabi_gcc` 相关的构建问题可能是由于 g++ 工具链安装损坏。
您可以通过检查缺少的依赖项来验证是否是这种情况：

```sh
arm-none-eabi-gcc --version
arm-none-eabi-g++ --version
arm-none-eabi-gdb --version
arm-none-eabi-size --version
```

缺少依赖项的 bash 输出示例：

```sh
arm-none-eabi-gdb --version
arm-none-eabi-gdb: command not found
```

可以通过删除并 [重新安装编译器](https://askubuntu.com/questions/1243252/how-to-install-arm-none-eabi-gdb-on-ubuntu-20-04-lts-focal-fossa) 来解决。

### Ubuntu 18.04: Visual Studio Code 无法监视此大型工作区中的文件更改

请参阅 [Visual Studio Code IDE (VSCode) > 故障排除](../dev_setup/vscode.md#troubleshooting)。

### Python 包导入失败

运行 `make px4_sitl jmavsim` 命令时出现 "Failed to import" 错误，表明一些 Python 包没有安装（在预期的位置）。

```sh
Failed to import jinja2: No module named 'jinja2'
You may need to install it using:
    pip3 install --user jinja2
```

如果您已经安装了这些依赖项，这可能是因为计算机上存在多个 Python 版本（例如 Python 2.7.16 Python 3.8.3），并且模块不存在于构建工具链使用的版本中。

您应该能够通过显式安装依赖项来解决此问题：

```sh
pip3 install --user pyserial empty toml numpy pandas jinja2 pyyaml pyros-genmsg packaging
```

## PX4 Make 构建目标

前面的章节展示了如何调用 _make_ 来构建许多不同的目标，启动模拟器，使用 IDE 等。
本节展示了 _make_ 选项是如何构造的，以及如何找到可用的选择。

使用特定配置和初始化文件调用 _make_ 的完整语法是：

```sh
make [VENDOR_][MODEL][_VARIANT] [VIEWER_MODEL_DEBUGGER_WORLD]
```

**VENDOR_MODEL_VARIANT**: (也称为 `CONFIGURATION_TARGET`)

- **VENDOR:** 开发板的制造商：`px4`, `aerotenna`, `airmind`, `atlflight`, `auav`, `beaglebone`, `intel`, `nxp`, 等。
  Pixhawk 系列开发板的厂商名称是 `px4`。
- **MODEL:** _开发板型号_ "model": `sitl`, `fmu-v2`, `fmu-v3`, `fmu-v4`, `fmu-v5`, `navio2`, 等。
- **VARIANT:** 表示特定配置：例如 `bootloader`, `cyphal`，这些组件在 `default` 配置中不存在。
  通常为 `default`，可以省略。

:::tip
您可以使用以下命令获取 _所有_ 可用的 `CONFIGURATION_TARGET` 选项列表：

```sh
make list_config_targets
```

:::

**VIEWER_MODEL_DEBUGGER_WORLD:**

- **VIEWER:** 这是要启动并连接的模拟器（"viewer"）：`gz`, `gazebo`, `jmavsim`, `none` <!-- , ?airsim -->

  :::tip
  如果您想启动 PX4 并等待模拟器（jmavsim、Gazebo、Gazebo Classic 或其他模拟器），可以使用 `none`。
  例如，`make px4_sitl none_iris` 启动 PX4 但没有模拟器（但有 iris 机型）。
  :::

- **MODEL:** 要使用的 _载具_ 模型（例如 `iris` (_默认_), `rover`, `tailsitter`, 等），模拟器将加载该模型。
  环境变量 `PX4_SIM_MODEL` 将被设置为所选模型，然后在 [启动脚本](../simulation/index.md#startup-scripts) 中用于选择适当的参数。
- **DEBUGGER:** 要使用的调试器：`none` (_默认_), `ide`, `gdb`, `lldb`, `ddd`, `valgrind`, `callgrind`。
  有关更多信息，请参见 [模拟调试](../debug/simulation_debugging.md)。
- **WORLD:** (仅限 Gazebo Classic)。
  设置要加载的世界 ([PX4-Autopilot/Tools/simulation/gazebo-classic/sitl_gazebo-classic/worlds](https://github.com/PX4/PX4-SITL_gazebo-classic/tree/main/worlds))。
  默认为 [empty.world](https://github.com/PX4/PX4-SITL_gazebo-classic/blob/main/worlds/empty.world)。
  有关更多信息，请参见 [Gazebo Classic > 加载特定世界](../sim_gazebo_classic/index.md#loading-a-specific-world)。

:::tip
您可以使用以下命令获取 _所有_ 可用的 `VIEWER_MODEL_DEBUGGER_WORLD` 选项列表：

```sh
make px4_sitl list_vmd_make_targets
```

:::

::: info

- `CONFIGURATION_TARGET` 和 `VIEWER_MODEL_DEBUGGER` 中的大多数值都有默认值，因此是可选的。
  例如，`gazebo-classic` 等同于 `gazebo-classic_iris` 或 `gazebo-classic_iris_none`。
- 如果您想在两个其他设置之间指定默认值，可以使用三个下划线。
  例如，`gazebo-classic___gdb` 等同于 `gazebo-classic_iris_gdb`。
- 您可以对 `VIEWER_MODEL_DEBUGGER` 使用 `none` 值来启动 PX4 并等待模拟器。
  例如，使用 `make px4_sitl_default none` 启动 PX4，并使用 `./Tools/simulation/jmavsim/jmavsim_run.sh -l` 启动 jMAVSim。

:::

`VENDOR_MODEL_VARIANT` 选项映射到 PX4 源代码树 [/boards](https://github.com/PX4/PX4-Autopilot/tree/main/boards) 目录下的特定 _px4board_ 配置文件。
具体来说，`VENDOR_MODEL_VARIANT` 映射到配置文件 **boards/VENDOR/MODEL/VARIANT.px4board**
（例如，`px4_fmu-v5_default` 对应于 [boards/px4/fmu-v5/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/default.px4board)）。

相关章节中讨论了其他 make 目标：

- `bloaty_compare_master`: [二进制大小分析](../debug/binary_size_profiling.md)
- ...

## 固件版本 & Git 标签

_PX4 固件版本_ 和 _自定义固件版本_ 使用 MAVLink [AUTOPILOT_VERSION](https://mavlink.io/en/messages/common.html#AUTOPILOT_VERSION) 消息发布，并显示在 _QGroundControl_ **设置 > 概要** 机型面板中：

![Firmware info](../../assets/gcs/qgc_setup_summary_airframe_firmware.jpg)

这些信息在构建时从您仓库树的活动 _git 标签_ 中提取。
git 标签应格式化为 `<PX4-version>-<vendor-version>`（例如，上图中的标签设置为 `v1.8.1-2.22.1`）。

:::warning
如果您使用不同的 git 标签格式，版本信息可能无法正确显示。
:::