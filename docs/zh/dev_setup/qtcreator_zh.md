# Qt Creator IDE

:::warning
此开发环境是 [社区支持和维护的](../advanced/community_supported_dev_env.md)。
它可能适用于也可能不适用于当前版本的 PX4。

Qt Creator 已被 [VSCode](../dev_setup/vscode.md) 取代，成为 PX4 开发官方支持（并推荐）的 IDE。
有关核心开发团队支持的环境和工具的信息，请参见 [工具链安装](../dev_setup/dev_env.md)。
:::

[Qt Creator](https://www.qt.io/download-open-source) 是一个流行的跨平台开源 IDE，可用于编译和调试 PX4。

## Qt Creator 功能

Qt Creator 提供可点击的符号、完整代码库的自动补全以及固件的构建和刷新。

![Screenshot of Qt Creator](../../assets/toolchain/qtcreator.png)

下面的视频展示了如何使用它。

<lite-youtube videoid="Bkk8zttWxEI" title="(Qt Creator) PX4 Flight Stack Build Experience"/>

## IDE 设置

### Linux 上的 Qt Creator

在启动 Qt Creator 之前，需要创建 [项目文件](https://gitlab.kitware.com/cmake/community/-/wikis/doc/cmake/Generator-Specific-Information#codeblocks-generator)：

```sh
cd ~/src/PX4-Autopilot
mkdir ../Firmware-build
cd ../Firmware-build
cmake ../PX4-Autopilot -G "CodeBlocks - Unix Makefiles"
```

然后通过 **File > Open File or Project** 加载根 PX4-Autopilot 文件夹中的 CMakeLists.txt（选择 CMakeLists.txt 文件）。

加载后，可以通过在运行目标配置中选择 'custom executable' 并输入 'make' 作为可执行文件和 'upload' 作为参数来配置 **play** 按钮以运行项目。

### Windows 上的 Qt Creator

::: info
Windows 尚未针对使用 Qt Creator 进行 PX4 开发进行测试。
:::

### Mac OS 上的 Qt Creator

在启动 Qt Creator 之前，需要创建 [项目文件](https://gitlab.kitware.com/cmake/community/-/wikis/doc/cmake/Generator-Specific-Information#codeblocks-generator)：

```sh
cd ~/src/PX4-Autopilot
mkdir -p build/creator
cd build/creator
cmake ../.. -G "CodeBlocks - Unix Makefiles"
```

就是这样！启动 _Qt Creator_，然后设置项目以进行构建。

<!-- 注意，这里的视频已被删除/设为私有，无论如何都已经过时。只是希望人们能够弄清楚 -->