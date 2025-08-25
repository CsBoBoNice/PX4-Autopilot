<div style="float:right; padding:10px; margin-right:20px;"><a href="https://px4.io/"><img src="../assets/site/logo_pro_small.png" title="PX4 Logo" width="180px" /></a></div>

# PX4 Autopilot 用户指南

[![Releases](https://img.shields.io/badge/release-main-blue.svg)](https://github.com/PX4/PX4-Autopilot/releases) [![Discuss](https://img.shields.io/badge/discuss-px4-ff69b4.svg)](https://discuss.px4.io//) [![Discord](https://discordapp.com/api/guilds/10221702755984457759/widget.png?style=shield)](https://discord.gg/dronecode)

PX4 是_专业自动驾驶仪_。
由来自工业界和学术界的世界级开发者开发，并得到活跃的全球社区支持，它为各种飞行器提供动力，从竞速无人机和货运无人机到地面车辆和水下航行器。

:::tip
本指南包含组装、配置和安全驾驶 PX4 飞行器所需的一切。有兴趣参与贡献？请查看[开发](development/development.md)部分。

:::

:::warning
本指南适用于 PX4 的_开发_版本（`main` 分支）。
请使用**版本**选择器查找当前的_稳定_版本。

自稳定版本以来记录的更改包含在不断更新的[发布说明](releases/main.md)中。
:::

## 如何开始？

[基本概念](getting_started/px4_basic_concepts.md)应该被所有用户阅读！
它提供了 PX4 的概述，包括飞行堆栈提供的功能（飞行模式和安全功能）以及支持的硬件（飞行控制器、飞行器类型、遥测系统、RC 控制系统）。

根据您想要实现的目标，以下提示将帮助您浏览本指南：

### 我想要一个与 PX4 兼容的飞行器

在[多旋翼](frames_multicopter/index.md)、[VTOL](frames_vtol/index.md)和[固定翼（飞机）](frames_plane/index.md)部分，您将找到以下主题（这些链接用于多旋翼）：

- [完整飞行器](complete_vehicles_mc/index.md)列出"即飞"（RTF）预构建飞行器
- [套件](frames_multicopter/kits.md)列出了您需要从一组预选部件自行构建的无人机
- [DIY 构建](frames_multicopter/diy_builds.md)展示了一些使用单独采购部件构建的无人机的示例

套件和完整飞行器通常包含除电池和 RC 系统之外所需的一切。
套件通常不难构建，很好地介绍了无人机的组装方式，并且相对便宜。
我们提供了通用的组装说明，例如[组装多旋翼](assembly/assembly_mc.md)，大多数套件也附有具体说明。

如果套件和完整无人机不太适合您，那么您可以从头开始构建飞行器，但这需要更多知识。
[机架构建](airframes/index.md)列出了支持的机架起点，让您了解可能的选择。

拥有支持 PX4 的飞行器后，您需要配置它并校准传感器。
每种飞行器类型都有自己的配置部分，解释主要步骤，例如[多旋翼配置/调参](config_mc/index.md)。

### 我想添加载荷/相机

[载荷](payloads/index.md)部分描述了如何添加相机以及如何配置 PX4 以便您能够运送包裹。

### 我在修改支持的飞行器

[硬件选择与设置](hardware/drone_parts.md)部分提供了您可能用于 PX4 及其配置的硬件的高级和产品特定信息。
如果您想修改无人机并添加新组件，这是您首先应该查看的地方。

### 我想飞行

在飞行之前，您应该阅读[操作](config/operations.md)以了解如何设置飞行器的安全功能以及所有机架类型的常见行为。
完成后，您就可以飞行了。

每种飞行器类型的基本飞行说明在各自的部分中提供，例如[基础飞行（多旋翼）](flying/basic_flying_mc.md)。

### 我想在新的飞行控制器上运行 PX4 并扩展平台

[开发](development/development.md)部分解释了如何支持新的机架和飞行器类型、修改飞行算法、添加新模式、集成新硬件、从飞行控制器外部与 PX4 通信，以及为 PX4 做贡献。

## 获取帮助

[支持](contribute/support.md)页面解释了如何从核心开发团队和更广泛的社区获取帮助。

其中包括：

- [可以获取帮助的论坛](contribute/support.md#forums-and-chat)
- [诊断问题](contribute/support.md#diagnosing-problems)
- [如何报告错误](contribute/support.md#issue-bug-reporting)
- [每周开发通话](contribute/support.md#weekly-dev-call)

## 报告错误和问题

如果您在使用 PX4 时遇到任何问题，首先请在[支持论坛](contribute/support.md#forums-and-chat)上发布（因为它们可能是由飞行器配置引起的）。

如果开发团队指示，代码问题可以在 [Github 这里](https://github.com/PX4/PX4-Autopilot/issues) 上提出。
尽可能提供[飞行日志](getting_started/flight_reporting.md)和问题模板中要求的其他信息。

## 贡献

有关如何贡献代码和文档的信息可以在[贡献](contribute/index.md)部分找到：

- [代码](contribute/index.md)
- [文档](contribute/docs.md)
- [翻译](contribute/translation.md)

## 翻译

本指南有几种[翻译版本](contribute/translation.md)。
您可以从语言菜单（右上角）访问这些版本：

![语言选择器](../assets/vuepress/language_selector.png)

<!--@include: _contributors.md-->

## 许可证

PX4 代码在宽松的[BSD 3条款许可证](https://opensource.org/license/BSD-3-Clause)条款下可免费使用和修改。
本文档根据[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)许可。
更多信息请参见：[许可证](contribute/licenses.md)。

## 日历和事件

_Dronecode 日历_显示平台用户和开发者的重要社区事件。
选择以下链接以在您的时区显示日历（并将其添加到您自己的日历中）：

- [瑞士 – 苏黎世](https://calendar.google.com/calendar/embed?src=linuxfoundation.org_g21tvam24m7pm7jhev01bvlqh8%40group.calendar.google.com&ctz=Europe%2FZurich)
- [太平洋时间 – 蒂华纳](https://calendar.google.com/calendar/embed?src=linuxfoundation.org_g21tvam24m7pm7jhev01bvlqh8%40group.calendar.google.com&ctz=America%2FTijuana)
- [澳大利亚 – 墨尔本/悉尼/霍巴特](https://calendar.google.com/calendar/embed?src=linuxfoundation.org_g21tvam24m7pm7jhev01bvlqh8%40group.calendar.google.com&ctz=Australia%2FSydney)

:::tip
日历默认时区为中欧时间（CET）。

:::

<iframe src="https://calendar.google.com/calendar/embed?title=Dronecode%20Calendar&amp;mode=WEEK&amp;height=600&amp;wkst=1&amp;bgcolor=%23FFFFFF&amp;src=linuxfoundation.org_g21tvam24m7pm7jhev01bvlqh8%40group.calendar.google.com&amp;color=%23691426&amp;ctz=Europe%2FZurich" style="border-width:0" width="800" height="600" frameborder="0" scrolling="no"></iframe>

### 图标

本库中使用的以下图标单独许可（如下所示）：

<img src="../assets/site/position_fixed.svg" title="需要位置修正（例如 GPS）" width="30px" /> _placeholder_ 图标由 <a href="https://www.flaticon.com/authors/smashicons" title="Smashicons">Smashicons</a> 从 <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> 制作，根据 <a href="https://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a> 许可。

<img src="../assets/site/automatic_mode.svg" title="自动模式" width="30px" /> _camera-automatic-mode_ 图标由 <a href="https://www.freepik.com" title="Freepik">Freepik</a> 从 <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> 制作，根据 <a href="https://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a> 许可。

## 治理

PX4 飞行堆栈由 [Dronecode 项目](https://dronecode.org/)托管。

<a href="https://dronecode.org/" style="padding:20px" ><img src="../assets/site/logo_dronecode.png" alt="Dronecode Logo" width="110px"/></a>
<a href="https://www.linuxfoundation.org/projects" style="padding:20px;"><img src="../assets/site/logo_linux_foundation.png" alt="Linux Foundation Logo" width="80px" /></a>

<div style="padding:10px">&nbsp;</div>

文档构建时间：{{ $buildTime }}
