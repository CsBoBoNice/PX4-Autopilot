# 无线电控制（RC）设置

_无线电设置_屏幕用于配置RC控制器主要姿态控制摇杆（横滚、俯仰、偏航、油门）到通道的映射，并校准所有其他发射器控制/RC通道的最小、最大、修正和反向设置。

::: info
可以使用[摇杆](../config/joystick.md)代替RC进行手动控制。
[COM_RC_IN_MODE](../advanced_config/parameter_reference.md#COM_RC_IN_MODE)参数[可以设置](../advanced_config/parameters.md)来定义启用什么类型的手动控制器。
:::

## 绑定接收器

在您可以校准无线电系统之前，接收器和发射器必须连接/绑定。
绑定发射器和接收器对的过程是特定于硬件的（请参阅您的RC手册了解说明）。

::: info
如果您使用 _Spektrum_ 接收器，您可以使用 _QGroundControl_ 将其置于绑定模式，如[下面所示](#spectrum-bind)。
:::

::: info
如果您使用 _FrSky_ 接收器，您可以通过遵循[这里](https://www.youtube.com/watch?v=1IYg5mQdLVI)的说明将其与发射器绑定。
:::

## RC信号丢失检测

PX4需要能够检测RC控制器信号丢失，以便能够采取[适当的安全措施](../config/safety.md#manual-control-loss-failsafe)。

RC接收器有不同的方式指示信号丢失：

- 不输出任何信号（PX4自动检测）
- 输出低油门值（您可以配置PX4检测此情况）。
- 输出最后接收到的信号（_PX4无法检测_，因为它看起来像有效输入）。

如果您的RC接收器不支持在RC信号丢失时不输出信号，您必须将其配置为设置低油门，并在[RC_FAILS_THR](../advanced_config/parameter_reference.md#RC_FAILS_THR)中设置相应的值。

做到这一点的方法是将RC控制器修正和油门摇杆设置得尽可能低，并在PX4和接收器中使用产生的输出PWM值（阅读您的接收器手册以确定如何设置RC丢失值）。
然后将油门摇杆修正重置回其正常位置。
此过程确保RC丢失值低于接收器在正常操作中输出的最小值。

::: info
不要使用不能支持两种受支持的RC丢失检测方法之一的接收器！
:::

## 执行校准

校准过程很简单 - 您将被要求按照屏幕右上角发射器图表上显示的特定模式移动摇杆。

校准无线电：

1. 打开您的RC发射器。
1. 启动 _QGroundControl_ 并连接飞行器。
1. 在顶部工具栏中选择**齿轮**图标（飞行器设置），然后在侧边栏中选择**无线电**。
1. 按**确定**开始校准。

   ![无线电设置 - 开始前](../../assets/qgc/setup/radio/radio_start_setup.jpg)

1. 设置与您的发射器匹配的[发射器模式](../getting_started/rc_transmitter_receiver.md#transmitter_modes)单选按钮（这确保 _QGroundControl_ 显示正确的摇杆位置供您在校准期间遵循）。

   ![无线电设置 - 移动摇杆](../../assets/qgc/setup/radio/radio_sticks_throttle.jpg)

1. 将摇杆移动到文本中指示的位置（以及发射器图像上）。当摇杆在位置时按**下一步**。对所有位置重复。
1. 当提示时，将所有其他开关和旋钮移动到其全范围（您将能够在_通道监视器_上观察它们移动）。

1. 按**下一步**保存设置。

无线电校准在[这里的自动驾驶仪设置视频](https://youtu.be/91VGmdSlbo4?t=4m30s)中演示（youtube）。

## 额外的无线电设置

除了校准您的控制摇杆和其他发射器控制外，在此屏幕上还有许多您可能发现有用的额外无线电设置选项。

<img src="../../assets/qgc/setup/radio/radio_additional_radio_setup.jpg" title="无线电设置 - 额外设置" width="300px" />

### Spektrum绑定

在您可以校准无线电系统之前，接收器和发射器必须连接/绑定。如果您有 _Spektrum_ 接收器，您可以使用 _QGroundControl_ 将其置于_绑定模式_，如下所示（如果您无法轻松物理访问飞行器上的接收器，这可能特别有用）。

绑定Spektrum发射器/接收器：

1. 选择**Spektrum绑定**按钮
1. 为您的接收器选择单选按钮
1. 按**确定**

   ![Spektrum绑定](../../assets/qgc/setup/radio/radio_additional_setup_spectrum_bind_select_channels.jpg)

1. 在按住绑定按钮的同时打开您的Spektrum发射器。

### 复制修正

此设置用于复制无线电发射器的手动修正设置，以便它们可以在自动驾驶仪内自动应用。完成此操作后，您需要移除手动设置的修正。

::: info
修正设置用于调整横滚、俯仰、偏航，使当您将遥控器上的摇杆居中时，您在稳定飞行模式下获得稳定或水平飞行。
一些RC控制器提供修正旋钮，允许您为每个摇杆位置提供RC控制器发送值的偏移。
这里的**复制修正**设置将偏移移动到自动驾驶仪中。
:::

复制修正：

1. 选择**复制修正**。
1. 将您的摇杆居中并将油门一直向下移动。
1. 按**确定**。

   ![复制修正](../../assets/qgc/setup/radio/radio_additional_radio_setup_copy_trims.jpg)

1. 将您发射器上的修正重置回零。

### AUX透传通道

AUX透传通道允许您从发射器控制任意可选硬件（例如，抓手）。

使用AUX透传通道：

1. 将最多2个发射器控制映射到单独的通道。
1. 指定这些通道分别映射到AUX1和AUX2端口，如下所示。
   设置后立即将值保存到飞行器。

   ![AUX1和AUX2 RC透传通道](../../assets/qgc/setup/radio/radio_additional_setup_aux_passthrough_channels.jpg)

飞行控制器将把指定通道的未修改值从AUX1/AUX2传递到连接的舵机/继电器，这些驱动您的硬件。

### 参数调参通道

调参通道允许您将发射器调参旋钮映射到参数（以便您可以从发射器动态修改参数）。

:::tip
此功能提供以启用手动飞行中调参：[多旋翼PID调参指南](../config_mc/pid_tuning_guide_multicopter.md)，[固定翼PID调参指南](../config_fw/pid_tuning_guide_fixedwing.md)。
:::

用于参数调参的通道在_无线电_设置中分配（这里！），而从每个调参通道到其关联参数的映射在_参数编辑器_中定义。

设置调参通道：

1. 将最多3个发射器控制（旋钮或滑块）映射到单独的通道。
1. 使用选择列表选择_PARAM调参Id_到无线电通道的映射。
   设置后立即将值保存到飞行器。

   ![将无线电通道映射到调参通道](../../assets/qgc/setup/radio/radio_additional_radio_setup_param_tuning.jpg)

将PARAM调参通道映射到参数：

1. 打开**参数**侧边栏。
1. 选择要映射到发射器的参数（这将打开_参数编辑器_）。
1. 选中**高级设置**复选框。
1. 点击**设置RC到参数...**按钮（这将弹出下面显示的前景对话框）

   ![将调参通道映射到参数](../../assets/qgc/setup/radio/parameters_radio_channel_mapping.jpg)

1. 从_参数调参ID_选择列表中选择要映射的调参通道（1、2或3）。
1. 按**确定**关闭对话框。
1. 按**保存**保存所有更改并关闭_参数编辑器_。

:::tip
您可以通过在_参数_屏幕右上角选择菜单**工具 > 清除RC到参数**来清除所有参数/调参通道映射。
:::

## 更多信息

- [QGroundControl > 无线电控制](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/radio.html)
- [PX4设置视频 - @4m30s](https://youtu.be/91VGmdSlbo4?t=4m30s) (Youtube)
- [RC系统选择](../getting_started/rc_transmitter_receiver.md) - 选择兼容的RC系统。
