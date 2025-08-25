# Visual Studio Code IDE (VSCode)

[Visual Studio Code](https://code.visualstudio.com/) 是一个功能强大的跨平台源代码编辑器/IDE，可用于在 Ubuntu、Windows 和 macOS 上进行 PX4 开发。

使用 VSCode 进行 PX4 开发有以下几个原因：

- 设置 _真的_ 只需要几分钟。
- 丰富的扩展生态系统，为 PX4 开发提供了大量所需工具：C/C++（具有可靠的 _cmake_ 集成）、_Python_、_Jinja2_、ROS 消息，甚至 DroneCAN DSDL。
- 优秀的 Github 集成。

本主题解释了如何设置 IDE 并开始开发。

::: info
还有其他功能强大的 IDE，但它们通常需要更多努力来与 PX4 集成。
使用 _VScode_，配置存储在 PX4/PX4-Autopilot 树中 ([PX4-Autopilot/.vscode](https://github.com/PX4/PX4-Autopilot/tree/main/.vscode))，因此设置过程就像添加项目文件夹一样简单。
:::

## 先决条件

您必须已经为您的平台安装了命令行 [PX4 开发环境](../dev_setup/dev_env.md) 并下载了 _Firmware_ 源代码仓库。

## 安装与设置

1. [下载并安装 VSCode](https://code.visualstudio.com/)（将为您提供适用于您操作系统的正确版本）。
1. 打开 VSCode 并添加 PX4 源代码：

   - 在欢迎页面上选择 _Open folder ..._ 选项（或使用菜单：**File > Open Folder**）：

     ![Open Folder](../../assets/toolchain/vscode/welcome_open_folder.jpg)

   - 将出现文件选择对话框。
     选择 **PX4-Autopilot** 目录，然后按 **OK**。

   项目文件和配置将加载到 _VSCode_ 中。

1. 在 _This workspace has extension recommendations_ 提示上按 **Install All**（这将出现在 IDE 的右下角）。
   ![Install extensions](../../assets/toolchain/vscode/prompt_install_extensions.jpg)

   VSCode 将在左侧打开 _Extensions_ 面板，以便您可以观察安装进度。

   ![PX4 loaded into VSCode Explorer](../../assets/toolchain/vscode/installing_extensions.jpg)

1. 底部右角可能会出现许多通知/提示

   :::tip
   如果提示消失，请单击底部蓝色栏右侧的小"铃铛"图标。
   :::

   - 如果提示安装新版本的 _cmake_：
     - 说 **No**（正确版本已随 [PX4 开发环境](../dev_setup/dev_env.md) 一起安装）。
   - 如果提示登录 _github.com_ 并添加您的凭据：
     - 这取决于您！它提供了 Github 和 IDE 之间的深度集成，这可能会简化您的工作流程。
   - 其他提示是可选的，如果它们看起来有用，可以安装。 <!-- 也许添加这些提示的截图 -->

<a id="building"></a>

## 构建 PX4

要构建：

1. 选择您的构建目标（"cmake build config"）：

   - 当前 _cmake 构建目标_ 显示在底部的蓝色 _config_ 栏上（如果这已经是您想要的目标，请跳到下一步）。
     ![Select Cmake build target](../../assets/toolchain/vscode/cmake_build_config.jpg)

     ::: info
     您选择的 cmake 目标会影响 [构建/调试](#debugging) 时提供的目标（即，对于硬件调试，您必须选择硬件目标，如 `px4_fmu-v6`）。
     :::

   - 单击配置栏上的目标以显示其他选项，并选择您想要的选项（这将替换任何选定的目标）。
   - _Cmake_ 将配置您的项目（请参见右下角的通知）。
     ![Cmake config project](../../assets/toolchain/vscode/cmake_configuring_project.jpg)
   - 等待配置完成。
     完成后，通知将消失，并会显示构建位置：
     ![Cmake config project](../../assets/toolchain/vscode/cmake_configuring_project_done.jpg)。

1. 然后您可以从配置栏启动构建（选择 **Build** 或 **Debug**）。
   ![Run debug or build](../../assets/toolchain/vscode/run_debug_build.jpg)

至少构建一次后，您现在可以使用 [代码补全](#code completion) 和其他 _VSCode_ 功能。

## 调试

<a id="debugging_sitl"></a>

### SITL 调试

要在 SITL 上调试 PX4：

1. 选择侧边栏上的调试图标（红色标记）以显示调试面板。
   ![Run debug](../../assets/toolchain/vscode/vscode_debug.jpg)

1. 然后从顶部栏调试下拉菜单（紫色框）中选择您的调试目标（例如 _Debug SITL (Gazebo Iris)_）。

   ::: info
   提供的调试目标（紫色框）与您的构建目标（底部栏上的黄色框）匹配。
   例如，要调试 SITL 目标，您的构建目标必须包含 SITL。
   :::

1. 通过单击调试"播放"箭头（顶部栏上调试目标旁边 - 粉色框）开始调试。

在调试时，您可以设置断点、逐步执行代码，并以正常方式开发。

### 硬件调试

[SWD Debug Port](../debug/swd_debug.md) 中的说明解释了如何连接到常见飞控上的 SWD 接口（例如，使用 Dronecode 或 Blackmagic 探针）。

连接到 SWD 接口后，VSCode 中的硬件调试与 [SITL 调试](#debugging_sitl) 相同，只是您选择适合您的调试器类型（和固件）的调试目标 - 例如 `jlink (px4_fmu-v5)`。

:::tip
要看到 `jlink` 选项，您必须已选择了 [用于构建固件的 cmake 目标](#building-px4)。
:::

![Image showing hardware targets with options for the different probes](../../assets/toolchain/vscode/vscode_hardware_debugging_options.png)

<a id="code completion"></a>

## 代码补全

为了使代码补全（和其他 IntelliSense 魔法）工作，您需要一个活动配置并已 [构建代码](#building)。

完成后，您无需执行任何其他操作；工具链将在您键入时自动为您提供符号。

![IntelliSense](../../assets/toolchain/vscode/vscode_intellisense.jpg)

## 故障排除

本节包括关于设置和构建错误的指导。

### Ubuntu 18.04: "Visual Studio Code is unable to watch for file changes in this large workspace"

此错误在启动时出现。
在某些系统上，对应用程序施加了 8192 个文件句柄的上限，这意味着 VSCode 可能无法检测到 `/PX4-Autopilot` 中的文件修改。

您可以增加此限制以避免错误，但会消耗更多内存。
请遵循 [此处的说明](https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc)。
65536 的值应该足够了。