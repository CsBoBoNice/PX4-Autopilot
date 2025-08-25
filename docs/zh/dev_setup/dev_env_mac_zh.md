# MacOS 开发环境

以下说明设置了用于 macOS 的 PX4 开发环境。
此环境可用于构建 PX4 用于：

- Pixhawk 和其他基于 NuttX 的硬件
- [Gazebo Classic 模拟](../sim_gazebo_classic/index.md)

:::tip
此设置由 PX4 开发团队支持。
要构建其他目标，您将需要使用 [不同的操作系统](../dev_setup/dev_env.md#supported-targets)（或 [不受支持的开发环境](../advanced/community_supported_dev_env.md)）。
:::

## 视频指南

<lite-youtube videoid="tMbMGiMs1cQ" title="在 macOS 上设置您的 PX4 开发环境"/>

## 基础设置

"基础" macOS 设置安装了构建固件所需的工具，并包括安装/使用模拟器所需的常见工具。

### 环境设置

:::details Apple Silicon Macbook 用户！
如果您有 Apple M1、M2 等 Macbook，请确保通过设置 x86 终端以 x86 模式运行终端：

1. 在实用工具文件夹中找到终端应用程序（**Finder > Go 菜单 > 实用工具**）
2. 选择 _Terminal.app_ 并右键单击它，然后选择 **Duplicate**。
3. 重命名复制的终端应用程序，例如命名为 _x86 Terminal_
4. 现在选择重命名的 _x86 Terminal_ 应用程序并右键单击并选择 \\*_Get Info_
5. 勾选 **Open using Rosetta** 框，然后关闭窗口
6. 照常运行 _x86 Terminal_，它将完全支持当前的 PX4 工具链
   :::

首先设置环境

1. 通过将以下行附加到 `~/.zshenv` 文件（如果需要则创建它）来启用更多打开的文件：

   ```sh
   echo ulimit -S -n 2048 >> ~/.zshenv
   ```

   ::: info
   如果您不这样做，构建工具链可能会报告错误：`"LD: too many open files"`
   :::

1. 通过将以下行附加到 `~/.zshenv` 来强制使用 Python 3

   ```sh
   # 将 pip3 指向 MacOS 系统 python 3 pip
   alias pip3=/usr/bin/pip3
   ```

### 常用工具

要设置能够为 Pixhawk/NuttX 硬件构建的环境（并安装使用模拟器的常用工具）：

1. 通过遵循这些 [安装说明](https://brew.sh) 安装 Homebrew。
1. 在您的 shell 中运行这些命令以安装常用工具：

   ```sh
   brew tap PX4/px4
   brew install px4-dev
   ```

1. 安装所需的 Python 包：

   ```sh
   # 使用 pip3 安装所需的包
   python3 -m pip install --user pyserial empty toml numpy pandas jinja2 pyyaml pyros-genmsg packaging kconfiglib future jsonschema
   # 如果这因权限错误而失败，您的 Python 安装位于系统路径中 - 请改用此命令：
   sudo -H python3 -m pip install --user pyserial empty toml numpy pandas jinja2 pyyaml pyros-genmsg packaging kconfiglib future jsonschema
   ```

## Gazebo Classic 模拟

要设置 [Gazebo Classic](../sim_gazebo_classic/index.md) 模拟的环境：

1. 在您的 shell 中运行以下命令：

   ```sh
   brew unlink tbb
   sed -i.bak '/disable! date:/s/^/  /; /disable! date:/s/./#/3' $(brew --prefix)/Library/Taps/homebrew/homebrew-core/Formula/tbb@2020.rb
   brew install tbb@2020
   brew link tbb@2020
   ```

   ::: info
   2021 年 9 月：上述命令是对此错误的解决方法：[PX4-Autopilot#17644](https://github.com/PX4/PX4-Autopilot/issues/17644)。
   一旦修复，可以删除它们（以及此注释）。
   :::

1. 安装带有 Gazebo Classic 的 SITL 模拟：

   ```sh
   brew install --cask temurin
   brew install --cask xquartz
   brew install px4-sim-gazebo
   ```

1. 运行 macOS 设置脚本：`PX4-Autopilot/Tools/setup/macos.sh`
   最简单的方法是克隆 PX4 源代码，然后从目录中运行脚本，如下所示：

   ```sh
   git clone https://github.com/PX4/PX4-Autopilot.git --recursive
   cd PX4-Autopilot/Tools/setup
   sh macos.sh
   ```


## 下一步

完成命令行工具链设置后：

- 安装 [VSCode](../dev_setup/vscode.md)（如果您更喜欢使用 IDE 而不是命令行）。
- 安装 [QGroundControl 每日构建版](../dev_setup/qgc_daily_build.md)

  :::tip
  _每日构建版_ 包含在发布构建中隐藏的开发工具。
  它也可能提供对尚未在发布构建中支持的新 PX4 功能的访问。
  :::

- 继续阅读 [构建说明](../dev_setup/building_px4.md)。