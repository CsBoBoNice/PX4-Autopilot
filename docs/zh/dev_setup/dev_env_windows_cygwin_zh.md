# Windows 开发环境（基于 Cygwin）

:::warning
此开发环境是 [社区支持和维护的](../advanced/community_supported_dev_env.md)。
它可能适用于也可能不适用于当前版本的 PX4。

该工具链之前被推荐使用，但由于打包问题，它不适用于 PX4 v1.12 及更高版本。
应优先使用 [基于 Windows WSL2 的开发环境](../dev_setup/dev_env_windows_wsl.md)。

有关核心开发团队支持的环境和工具的信息，请参见 [工具链安装](../dev_setup/dev_env.md)。
:::

以下说明解释了如何在 Windows 10 上设置（基于 Cygwin 的）PX4 开发环境。
此环境可用于构建 PX4 用于：

- Pixhawk 和其他基于 NuttX 的硬件
- [jMAVSim 模拟](../sim_jmavsim/index.md)

<a id="installation"></a>

## 安装说明

1. 从以下位置下载最新版本的即用型 MSI 安装程序：[Github releases](https://github.com/PX4/PX4-windows-toolchain/releases) 或 [Amazon S3](https://s3-us-west-2.amazonaws.com/px4-tools/PX4+Windows+Cygwin+Toolchain/PX4+Windows+Cygwin+Toolchain+0.9.msi)（快速下载）。
1. 运行它，选择您想要的安装位置，让它安装：

   ![jMAVSimOnWindows](../../assets/toolchain/cygwin_toolchain_installer.png)

1. 在安装结束时勾选框以 _克隆 PX4 仓库，构建并使用 jMAVSim 运行模拟_（这简化了入门过程）。

   ::: info
   如果您错过了此步骤，则需要 [手动克隆 PX4-Autopilot 仓库](#getting-started)。
   :::

:::warning
在撰写本文时，安装程序缺少一些依赖项（由于 [PX4-windows-toolchain#31](https://github.com/PX4/PX4-windows-toolchain/issues/31)，目前还无法重新构建来添加它们）。

要自己添加这些依赖项：

1. 浏览到工具链安装目录（默认 **C:\\PX4\\**）
1. 运行 **run-console.bat**（双击）以启动类似 Linux 的 Cygwin bash 控制台
1. 在控制台中输入以下命令：

   ```sh
   pip3 install --user kconfiglib jsonschema future
   ```

:::

## 入门指南

工具链使用一个特别配置的控制台窗口（通过运行 **run-console.bat** 脚本启动），您可以从中调用正常的 PX4 构建命令：

1. 浏览到工具链安装目录（默认 **C:\\PX4\\**）
1. 运行 **run-console.bat**（双击）以启动类似 Linux 的 Cygwin bash 控制台（您必须使用此控制台来构建 PX4）。
1. 在控制台内克隆 PX4 PX4-Autopilot 仓库：

   ::: info
   如果您勾选了安装程序选项 _克隆 PX4 仓库，构建并使用 jMAVSim 运行模拟_，请跳过此步骤。
   克隆只需要执行一次！
   :::

   ```sh
   # 将 PX4-Autopilot 仓库克隆到主文件夹 & 并行加载子模块
   git clone --recursive -j8 https://github.com/PX4/PX4-Autopilot.git
   ```

   您现在可以使用控制台/PX4-Autopilot 仓库来构建 PX4。

1. 例如，要运行 JMAVSim：

   ```sh
   # 导航到 PX4-Autopilot 仓库
   cd Firmware
   # 构建并使用 jMAVSim 运行 SITL 模拟以测试设置
   make px4_sitl jmavsim
   ```

   控制台将显示：

   ![jMAVSimOnWindows](../../assets/simulation/jmavsim/jmavsim_windows_cygwin.png)

## 下一步

完成命令行工具链设置后：

- 安装 [QGroundControl 每日构建版](../dev_setup/qgc_daily_build.md)
- 继续阅读 [构建说明](../dev_setup/building_px4.md)。

## 故障排除

### 文件监控工具 vs 工具链速度

防病毒软件和其他后台文件监控工具会显著减慢工具链的安装和 PX4 构建时间。

您可能希望在构建期间临时停止它们（风险自负）。

### Windows & Git 特殊情况

#### Windows CR+LF vs Unix LF 行尾

我们建议您为使用此工具链处理的每个仓库强制使用 Unix 风格的 LF 行尾（并使用在保存更改时保留它们的编辑器 - 例如 Eclipse 或 VS Code）。
源文件的编译也可以使用本地检出的 CR+LF 行尾工作，但在 Cygwin 中有些情况（例如执行 shell 脚本）需要 Unix 行尾（否则会出现类似 `$'\\r': Command not found.` 的错误）。
幸运的是，git 可以为您执行此操作，当您在仓库的根目录中执行以下两个命令时：

```sh
git config core.autocrlf false
git config core.eol lf
```

如果您在多仓库中使用此工具链，也可以为您的机器全局设置这两个配置：

```sh
git config --global ...
```

不建议这样做，因为它可能会影响您 Windows 机器上的任何其他（无关）git 使用。

#### Unix 权限执行位

在 Unix 下，每个文件的权限中都有一个标志，告诉操作系统是否允许执行该文件。
_git_ 在 Cygwin 下支持并关心该位（即使 Windows NTFS 文件系统不使用它）。
这通常会导致 _git_ 发现权限的"假阳性"差异。
生成的差异可能如下所示：

```sh
diff --git ...
old mode 100644
new mode 100755
```

我们建议在 Windows 上全局禁用权限检查以避免此问题：

```sh
# 为机器全局禁用执行位检查
git config --global core.fileMode false
```

对于因本地配置而导致此问题的现有仓库，另外：

```sh
# 删除此仓库的本地选项以应用全局选项
git config --unset core.filemode

# 删除所有子模块的本地选项
git submodule foreach --recursive git config --unset core.filemode
```

<!--
有关构建/更新此工具链的说明，请参见 [Windows Cygwin 开发环境（维护说明）](../dev_setup/dev_env_windows_cygwin_packager_setup.md)
-->