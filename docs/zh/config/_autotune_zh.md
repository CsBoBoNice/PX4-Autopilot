<!-- 这是自动调节文档的单一源文件，用于 autotune_mc.md 和 autotune_fw.md
在编写时，只有FW、MC和VTOL支持自动调节。
VTOL有自己的文档，引用其他两个
-->

<div v-if="$frontmatter.frame === 'Multicopter'">

# 自动调节 (多旋翼)

</div>
<div v-else-if="$frontmatter.frame === 'Plane'">

# 自动调节 (固定翼)

</div>

自动调节自动化了PX4速率和姿态控制器的调节过程，这些控制器是稳定和响应式飞行最重要的控制器（其他调节更多是"可选的"）。

调节只需要执行一次，除非您使用的是制造商已经调节过的飞行器（并且自那时起没有修改过），否则建议进行调节。

:::warning
自动调节是在飞行过程中执行的。
机体必须能够很好地处理适度的扰动，并且应该密切关注：

- 测试您的飞行器是否[足够稳定以进行自动调节](#pre-tuning-test)。
- 准备中止自动调节过程。
  您可以通过更改飞行模式来做到这一点<div style="display: inline;" v-if="$frontmatter.frame === 'Plane'">或使用自动调节启用/禁用开关（[如果已配置](#enable-disable-autotune-switch)）</div>。
- 验证飞行器在调节后飞行良好。

:::

<lite-youtube videoid="5xswOhhqrIQ" title="QGroundControl 自动调节功能详解 PX4自动驾驶仪"/>

## 调节前测试

飞行器必须能够飞行并在运行自动调节之前充分稳定自己。
此测试确保飞行器能够在位置控制模式下安全飞行。

要确保飞行器足够稳定以进行自动调节：

1. 执行正常的飞行前安全检查表，以确保飞行区域清晰且有足够的空间。

2. 起飞并<div style="display: inline;" v-if="$frontmatter.frame === 'Multicopter'">在[高度模式](../flight_modes_mc/altitude.md)或[稳定模式](../flight_modes_mc/manual_stabilized.md)下悬停在距离地面1米的位置</div><div style="display: inline;" v-else-if="$frontmatter.frame === 'Plane'">在[位置模式](../flight_modes_fw/position.md)或[高度模式](../flight_modes_fw/altitude.md)下以巡航速度飞行</div>。

3. 使用遥控发射机的横滚摇杆执行以下操作，将飞行器倾斜几度：_左滚 > 右滚 > 居中_（整个操作应该需要大约3秒）。
   飞行器应该在2次振荡内稳定自己。
4. 重复操作，在每次尝试时增加倾斜幅度。
   如果飞行器能够在约20度的倾斜角度下在2次振荡内稳定自己，则转到下一步。
5. 在俯仰轴上重复相同的操作。
   如上所述，从小角度开始，确认飞行器能够在2次振荡内稳定自己，然后再增加倾斜角度。

如果无人机能够在2次振荡内稳定自己，则它已准备好进行[自动调节程序](#auto-tuning-procedure)。

::: warning
如果无人机无法充分稳定自己，请按照[故障排除](#troubleshooting)部分的说明进行操作。
这些说明解释了为自动调节准备飞行器所需的最小手动调节。
:::

## 自动调节程序

自动调节序列必须在**安全飞行区域内执行，且有足够的空间**。
大约需要40秒（[19到68秒之间](#how-long-does-autotuning-take)）。
为了获得最佳结果，我们建议在平静的天气条件下运行测试。

推荐的自动调节模式是<div style="display: inline;" v-if="$frontmatter.frame === 'Multicopter'">[高度模式](../flight_modes_mc/altitude.md)</div><div  style="display: inline;" v-else-if="$frontmatter.frame === 'Plane'">[悬停模式](../flight_modes_fw/hold.md)</div>，但也可以使用任何其他飞行模式。
在自动调节过程中无法使用遥控摇杆（移动摇杆会停止自动调节操作）。

测试步骤如下：

1. 执行[调节前测试](#pre-tuning-test)。

2. 使用遥控器起飞<div style="display: inline;" v-if="$frontmatter.frame === 'Multicopter'">在[高度模式](../flight_modes_mc/altitude.md)下。
   将飞行器悬停在安全距离和距离地面几米的高度（4到20米之间）。</div><div v-else-if="$frontmatter.frame === 'Plane'">
   一旦以巡航速度飞行，激活[悬停模式](../flight_modes_fw/hold.md)。
   这将引导飞机在恒定高度和速度下绕圈飞行。</div>

3. 启用自动调节。

   <div v-if="$frontmatter.frame === 'Plane'">
   <div class="tip custom-block"><p class="custom-block-title">提示</p>

   如果配置了[启用/禁用自动调节开关](#enable-disable-autotune-switch)，您可以直接将开关切换到"启用"位置。

   </div></div>

   1. 在QGroundControl中，打开菜单 **飞行器设置 > PID调节**：

      ![调节设置 > 自动调节启用](../../assets/qgc/setup/autotune/autotune.png)

   2. 选择 _速率控制器_ 或 _姿态控制器_ 选项卡。
   3. 确保 **自动调节启用** 按钮已启用（这将显示**自动调节**按钮并移除手动调节选择器）。
   4. 阅读警告弹窗并点击 **确定** 开始调节。

4. 无人机将首先开始执行快速横滚运动，然后是俯仰和偏航运动。
   进度显示在 _自动调节_ 按钮旁边的进度条中。

<div style="display: inline;" v-if="$frontmatter.frame === 'Multicopter'">

5. 手动着陆并解除武装以应用新的调节参数。
   小心起飞并手动测试飞行器是否稳定。

</div><div v-else-if="$frontmatter.frame === 'Plane'">

5. 调节将立即/自动应用并在飞行中测试（默认情况下）。
   PX4将运行4秒测试，如果检测到问题，则恢复新调节。

</div>

::: warning
如果出现任何强烈振荡，请立即着陆并按照下面[故障排除](#troubleshooting)部分的说明进行操作。
:::

附加说明：

<div v-if="$frontmatter.frame === 'Multicopter'">

- 上述说明在[高度模式](../flight_modes_mc/altitude.md)下调节飞行器。
  如果飞行器在这些模式下_已知_稳定，您可以改为在[起飞模式](../flight_modes_mc/takeoff.md)下起飞并在[位置模式](../flight_modes_mc/position.md)下调节。

</div>
<div v-else-if="$frontmatter.frame === 'Plane'">

- 自动调节也可以在[高度模式](../flight_modes_fw/altitude.md)或[位置模式](../flight_modes_fw/position.md)下运行。
  但是，在直线飞行时运行测试需要更大的调节安全区域，并且不会显著改善调节结果。

</div>

- 调节是在飞行中应用还是着陆后应用可以[使用参数配置](#apply-tuning-when-in-air-landed)。

<div v-if="$frontmatter.frame === 'Multicopter'">

## 大型飞行器自动调节

对于大型多旋翼飞行器，您可能需要增加阶跃响应的期望上升时间[MC_AT_RISE_TIME](../advanced_config/parameter_reference.md#MC_AT_RISE_TIME)。
这需要一些试验和错误，因为适当的上升时间取决于飞行器尺寸和转子响应。

请注意，如果预调节中存在缓慢振荡，可能意味着姿态环路相对于速率环路太快。
在这种情况下，您应该按照[无人机在执行预调节测试时振荡](#drone-oscillates-when-performing-the-pre-tuning-test)中的描述进行故障排除。

<!-- 固定翼上升时间是硬编码的（它比多旋翼上低，对于大多数平台可能足够）。 -->

</div>

## 故障排除

### 无人机在执行预调节测试时振荡

<div v-if="$frontmatter.frame === 'Multicopter'">

缓慢振荡（每秒1次振荡或更慢）：这通常发生在大型平台上，意味着姿态环路相对于速率环路太快：

- 将[MC_ROLL_P](../advanced_config/parameter_reference.md#MC_ROLL_P)和[MC_PITCH_P](../advanced_config/parameter_reference.md#MC_PITCH_P)降低1.0步长。

快速振荡（每秒超过1次振荡）：这是因为速率环路的增益太高。

- 将`MC_[ROLL|PITCH|YAW]RATE_K`降低0.02步长

</div>
<div v-else-if="$frontmatter.frame === 'Plane'">

缓慢振荡（每秒1次振荡或更慢）：这通常发生在大型平台上，意味着姿态环路相对于速率环路太快。

- 将[FW_R_TC](../advanced_config/parameter_reference.md#FW_R_TC)和[FW_P_TC](../advanced_config/parameter_reference.md#FW_P_TC)增加0.1步长。

快速振荡（每秒超过1次振荡）：这是因为速率环路的增益太高。

- 将[FW_RR_P](../advanced_config/parameter_reference.md#FW_RR_P)、[FW_PR_P](../advanced_config/parameter_reference.md#FW_PR_P)、[FW_YR_P](../advanced_config/parameter_reference.md#FW_YR_P)降低0.01步长。

</div>

### 自动调节序列失败

如果无人机在自动调节期间移动不够，系统识别算法可能无法找到正确的系数。

将<div style="display: inline;" v-if="$frontmatter.frame === 'Multicopter'">[MC_AT_SYSID_AMP](../advanced_config/parameter_reference.md#MC_AT_SYSID_AMP)</div><div style="display: inline;" v-else-if="$frontmatter.frame === 'Plane'">[FW_AT_SYSID_AMP](../advanced_config/parameter_reference.md#FW_AT_SYSID_AMP)</div>参数增加1步长并重新触发自动调节。

### 自动调节后无人机振荡

由于数学模型中未包含的效应（如延迟、饱和、转换速率、机身柔韧性），环路增益可能太高。
要解决这个问题，请按照[无人机在预调节测试中振荡](#drone-oscillates-when-performing-the-pre-tuning-test)时描述的相同步骤进行。

### 我仍然无法让它工作

尝试使用下面[另请参阅](#see-also)中列出的指南进行手动调节。

## 可选配置

### 在空中/着陆时应用调节

<div v-if="$frontmatter.frame === 'Multicopter'">

多旋翼在应用参数之前着陆。
此行为可以使用[MC_AT_APPLY](../advanced_config/parameter_reference.md#MC_AT_APPLY)参数配置：

</div>
<div v-else-if="$frontmatter.frame === 'Plane'">

默认情况下，固定翼调节参数在飞行时应用，然后PX4运行测试以确认控制器工作正常。
此行为可以使用[FW_AT_APPLY](../advanced_config/parameter_reference.md#FW_AT_APPLY)参数配置：

</div>

- `0`：不应用增益。
  如果用户希望检查自动调节算法的结果而不直接使用它们，则用于测试目的。
- `1`：解除武装后应用增益（多旋翼默认）。
  然后操作员可以在小心起飞时测试新调节。
- `2`：立即应用（固定翼默认）。
  应用新调节，向控制器发送扰动，并在接下来的4秒内监测稳定性。
  如果控制环路不稳定，控制增益会立即恢复到之前的值。
  如果测试通过，飞行员可以使用新调节。

<div v-if="$frontmatter.frame === 'Plane'">

### 启用/禁用自动调节开关

可以使用RC AUX通道配置遥控开关以在任何模式下启用/禁用自动调节（注意，这仅在固定翼飞行器上受支持）。

要映射开关：

1. 在您的控制器上选择一个RC通道用于自动调节启用/禁用开关。
2. 设置[RC_MAP_AUX1](../advanced_config/parameter_reference.md#RC_MAP_AUX1)以匹配开关的RC通道（您可以使用`RC_MAP_AUX1`到`RC_MAP_AUX6`中的任何一个）。
3. 设置[FW_AT_MAN_AUX](../advanced_config/parameter_reference.md#FW_AT_MAN_AUX)为所选通道（即，如果您映射了`RC_MAP_AUX1`，则为`1: Aux 1`）。

当开关低于`0.5`（在`[-1, 1]`的手动控制设定点范围内）时，自动调谐器将被禁用，当开关通道高于`0.5`时启用。

如果使用RC AUX开关启用自动调节，请确保在飞行前[选择调节轴](#select-tuning-axis)。

### 选择调节轴

固定翼飞行器（仅）可以使用[FW_AT_AXES](../advanced_config/parameter_reference.md#FW_AT_AXES)位掩码参数选择调节哪些轴：

- 位`0`：横滚（默认）
- 位`1`：俯仰（默认）
- 位`2`：偏航

</div>

## 开发者/SDK

自动调节使用[MAV_CMD_DO_AUTOTUNE_ENABLE](https://mavlink.io/en/messages/common.html#MAV_CMD_DO_AUTOTUNE_ENABLE) MAVLink命令启动。

在编写时，消息以固定间隔重新发送以轮询PX4的进度：`COMMAND_ACK`包括操作正在进行的结果，以及作为百分比的进度。
当进度为100%或飞行器着陆并解除武装时操作完成。

::: info
这不是[命令协议长运行命令](https://mavlink.io/en/services/command.html#long_running_commands)的MAVLink兼容实现。
PX4应该流式传输进度，因为协议不允许轮询。
:::

MAVSDK尚不支持此功能。

## 背景/详细信息

PX4使用[PID控制器](../flight_stack/controller_diagrams.md)（速率、姿态、速度和位置）来计算将飞行器从当前估计状态移动到匹配期望设定点所需的输出。
控制器必须调节良好才能从飞行器获得最佳性能。
特别是，调节不良的速率控制器会导致所有模式下的飞行不太稳定，并且从扰动中恢复的时间更长。

通常，如果您使用类似于您的飞行器的[机架配置](../config/airframe.md)，飞行器就能够飞行。
但是，除非配置与您的硬件完全匹配，否则您应该调节速率和姿态控制器。
调节速度和位置控制器不太重要，因为它们受飞行器动力学影响较小，类似机架的默认调节配置通常就足够了。

自动调节提供了调节速率和姿态控制器的自动机制。
它可用于调节固定翼和多旋翼飞行器，以及在作为多旋翼或固定翼飞行时的VTOL飞行器（模式之间的转换必须手动调节）。
理论上，它应该适用于具有速率控制器的其他飞行器类型，但目前仅支持上述类型。

自动调节适用于PX4支持的多旋翼和固定翼飞行器配置，前提是机架不太柔韧（有关更多信息，请参见[下面](#does-autotuning-work-for-all-supported-airframes)）。

飞行器必须在高度稳定模式下飞行（如[高度模式](../flight_modes_mc/altitude.md)、[悬停模式](../flight_modes_mc/hold.md)或[位置模式](../flight_modes_mc/position.md)）。
飞行堆栈将对飞行器在每个轴上施加小扰动，然后尝试计算新的调节参数。
对于固定翼飞行器，默认情况下新调节在空中应用，之后飞行器测试新设置，如果控制器不稳定则恢复调节。
对于多旋翼，飞行器着陆并在解除武装后应用新调节参数；飞行员应该小心起飞并测试调节。

调节过程大约需要40秒（[19到70秒之间](#how-long-does-autotuning-take)）。
可以使用[参数](#optional-configuration)配置默认行为。

### 常见问题

#### 支持哪些机架类型？

自动调节适用于多旋翼、固定翼和混合VTOL固定翼飞行器。

虽然尚未为其他机架类型启用，理论上可以与使用速率控制器的任何机架一起使用。

#### 自动调节是否适用于所有受支持的机架？

自动调节使用的数学模型估计无人机的动力学，假设这是一个在轴之间没有耦合的线性系统（SISO），且复杂性有限（2个极点和2个零点）。
如果真实无人机与这些条件相差太远，模型将无法表示无人机的真实动力学。

在实践中，自动调节通常适用于固定翼和多旋翼，前提是机架不太柔韧。

#### 自动调节需要多长时间？

每轴调节需要5s-20s（如果在20s内无法建立调节则中止）+ 每轴之间2s暂停 + 如果新增益在空中应用则4s测试。

多旋翼必须调节所有三个轴，默认情况下不在空中测试新增益。
因此调节需要19s（`5 + 2 + 5 + 2 + 5`）到64s（`20x3 + 2x2`）。

默认情况下，固定翼飞行器调节所有三个轴，然后在空中测试新增益。
因此范围是25s（`5 + 2 + 5 + 2 + 5 + 2 + 4`）到70s（`20x3 + 3x2 + 4`）。

但是请注意，上述设置是默认设置。
多旋翼可以选择在空中运行测试，固定翼可以选择不运行。
此外，固定翼可以选择调节更少的轴。

根据经验，通常需要大约40秒的时间。

<!--
#### 调节施加的扰动有多剧烈

这可能会在以后添加。我想只是指向一个视频。

如果没有，也许说"不是很"，但您应该期望飞行器可能会偏转多达20度，因此应该能够使用默认调节应对该偏转。

-->

<div v-if="$frontmatter.frame === 'Multicopter'">

## 另请参阅

- [多旋翼PID调节指南](../config_mc/pid_tuning_guide_multicopter_basic.md)（手动/简单）
- [多旋翼PID调节指南](../config_mc/pid_tuning_guide_multicopter.md)（高级/详细）
- [参数 > 自动调节](../advanced_config/parameter_reference.md#autotune)（以`MC_AT_`为前缀）。

</div>
<div v-else-if="$frontmatter.frame === 'Plane'">

## 另请参阅

- [固定翼PID调节指南](../config_fw/pid_tuning_guide_fixedwing.md)
- [参数 > 自动调节](../advanced_config/parameter_reference.md#autotune)（以`FW_AT_`为前缀）。

</div>
