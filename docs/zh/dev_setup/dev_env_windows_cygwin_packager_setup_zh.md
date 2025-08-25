# Windows Cygwin 开发环境（维护说明）

:::warning
此开发环境是 [社区支持和维护的](../advanced/community_supported_dev_env.md)。
它可能适用于也可能不适用于当前版本的 PX4。

有关核心开发团队支持的环境和工具的信息，请参见 [工具链安装](../dev_setup/dev_env.md)。
:::

本主题解释了如何构建和扩展用于不再支持的 [基于 Cygwin 的 Windows 开发环境](../dev_setup/dev_env_windows_cygwin.md) 的开发环境。

## 附加信息

### 功能 / 问题

以下功能已知可以工作（版本 2.0）：

- 使用 jMAVSim 构建和运行 SITL，性能明显优于 VM（它生成一个原生 Windows 二进制文件 **px4.exe**）。
- 构建和上传 NuttX 构建（例如：px4_fmu-v2 和 px4_fmu-v4）
- 使用 _astyle_ 进行样式检查（支持命令：`make format`）
- 命令行自动补全
- 非侵入式安装程序！安装程序不会影响您的系统和全局路径（它只修改选定的安装目录，例如 **C:\\PX4\\** 并使用临时本地路径）。
- 安装程序支持更新到新版本，同时保留工具链文件夹内的个人更改

遗漏：

- 模拟：不支持 Gazebo 和 ROS。
- 仅支持 NuttX 和 JMAVSim/SITL 构建。

### Shell 脚本安装

您也可以使用 Github 项目中的 shell 脚本安装环境。

1. 确保您已安装 [Git for Windows](https://git-scm.com/download/win)。
1. 将仓库 https://github.com/PX4/windows-toolchain 克隆到您想要安装工具链的位置。默认位置和命名是通过打开 `Git Bash` 并执行以下命令实现的：

   ```sh
   cd /c/
   git clone https://github.com/PX4/windows-toolchain PX4
   ```

1. 如果您想安装所有组件，请导航到新克隆的文件夹，然后双击位于 `toolchain` 文件夹中的脚本 `install-all-components.bat`。如果您只需要某些组件并且想要节省网络流量或磁盘空间，可以导航到不同的组件文件夹，例如 `toolchain\\cygwin64`，然后点击 **install-XXX.bat** 脚本以仅获取特定内容。
1. 继续阅读 [入门指南](../dev_setup/dev_env_windows_cygwin.md#getting-started)。

### 手动安装（适用于工具链开发者）

本节描述了如何自己手动设置 Cygwin 工具链，同时指向基于脚本安装仓库中的相应脚本。
结果应该与使用脚本或 MSI 安装程序相同。

::: info
工具链会进行维护，因此这些说明可能无法涵盖所有未来变化的每个细节。
:::

1. 创建 _文件夹_: **C:\\PX4\\**, **C:\\PX4\\toolchain\\** 和 **C:\\PX4\\home\\**
1. 从 [官方 Cygwin 网站](https://cygwin.com/install.html) 下载 _Cygwin 安装程序_ 文件 [setup-x86_64.exe](https://cygwin.com/setup-x86_64.exe)
1. 运行下载的安装文件
1. 在向导中选择安装到文件夹: **C:\\PX4\\toolchain\\cygwin64\\**
1. 选择安装默认的 Cygwin 基础和以下附加包的最新可用版本：
   - **类别:包名**
   - Devel:cmake (3.3.2 不会产生已弃用警告，3.6.2 可以工作但有警告)
   - Devel:gcc-g++
   - Devel:gdb
   - Devel:git
   - Devel:make
   - Devel:ninja
   - Devel:patch
   - Editors:xxd
   - Editors:nano (除非您是 vim 专家)
   - Python:python2
   - Python:python2-pip
   - Python:python2-numpy
   - Python:python2-jinja2
   - Python:python2-pyyaml
   - Python:python2-cerberus
   - Archive:unzip
   - Utils:astyle
   - Shells:bash-completion
   - Web:wget

   ::: info
   不要选择此列表上没有的尽可能多的包，有一些包会冲突并破坏构建。
   :::

   ::: info
   这就是 [cygwin64/install-cygwin-px4.bat](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/cygwin64/install-cygwin-px4.bat) 所做的。
   :::

1. 编写或复制 **批处理脚本** [`run-console.bat`](https://github.com/PX4/PX4-windows-toolchain/blob/master/run-console.bat) 和 [`setup-environment.bat`](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/scripts/setup-environment.bat)。

   通过准备好的批处理脚本启动所有开发工具的原因是它们预先配置启动程序以使用工具链文件夹内的本地、便携式 Cygwin 环境。
   这是通过始终首先调用脚本 [**setup-environment.bat**](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/scripts/setup-environment.bat)，然后启动所需的应用程序（如控制台）来完成的。

   脚本 [setup-environment.bat](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/scripts/setup-environment.bat) 本地设置工作区根目录 `PX4_DIR`、所有二进制位置 `PATH` 和 unix 环境主目录 `HOME` 的环境变量。

1. 通过打开 Cygwin 工具链控制台（双击 **run-console.bat**）并执行以下命令，为您的设置添加必要的 **python 包**

   ```sh
   pip2 install toml
   pip2 install pyserial
   pip2 install pyulog
   ```

   ::: info
   这就是 [cygwin64/install-cygwin-python-packages.bat](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/cygwin64/install-cygwin-python-packages.bat) 所做的。
   :::

1. 下载 [**ARM GCC 编译器**](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain) 作为 Windows 二进制文件的 zip 存档，并将内容解压到文件夹 `C:\\PX4\\toolchain\\gcc-arm`。

   ::: info
   这是工具链在以下位置所做的: [gcc-arm/install-gcc-arm.bat](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/gcc-arm/install-gcc-arm.bat)。
   :::

1. 安装 JDK：
   - 从 [Oracle](https://www.oracle.com/java/technologies/downloads/) 下载 Java 14
   - 因为遗憾的是没有包含直接二进制文件的便携式存档，您必须安装它。
   - 找到二进制文件并将它们移动/复制到 **C:\\PX4\\toolchain\\jdk**。
   - 您可以从 Windows 系统中卸载该套件，我们只需要工具链的二进制文件。

   ::: info
   这是工具链在以下位置所做的: [jdk/install-jdk.bat](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/jdk/install-jdk.bat)。
   :::

1. 下载 [**Apache Ant**](https://ant.apache.org/bindownload.cgi) 作为 Windows 二进制文件的 zip 存档，并将内容解压到文件夹 `C:\\PX4\\toolchain\\apache-ant`。

   :::tip
   确保您没有从下载存档中的文件夹中获得额外的文件夹层。
   :::

   ::: info
   这是工具链在以下位置所做的: [apache-ant/install-apache-ant.bat](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/apache-ant/install-apache-ant.bat)。
   :::

1. 下载、构建并将 _genromfs_ 添加到路径：
   - 使用以下命令将源代码克隆到文件夹 **C:\\PX4\\toolchain\\genromfs\\genromfs-src**

     ```sh
     cd /c/toolchain/genromfs
     git clone https://github.com/chexum/genromfs.git genromfs-src
     ```

   - 使用以下命令编译它：

     ```sh
     cd genromfs-src
     make all
     ```

   - 将生成的二进制文件 **genromfs.exe** 复制到上一级文件夹：**C:\\PX4\\toolchain\\genromfs**

1. 确保所有已安装组件的二进制文件夹都正确列在由 [**setup-environment.bat**](https://github.com/PX4/PX4-windows-toolchain/blob/master/toolchain/scripts/setup-environment.bat) 配置的 `PATH` 变量中。