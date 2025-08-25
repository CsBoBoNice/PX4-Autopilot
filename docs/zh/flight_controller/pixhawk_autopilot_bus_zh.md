# Pixhawk 自驾仪总线和载板

[Pixhawk 自驾仪总线（PAB）标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf) 提供了标准接口设计，允许任何符合标准的 Pixhawk 飞行控制器与任何符合标准的基板"即插即用"。

这种模块化使得将飞行控制器集成到不同的系统模块设计中更加容易。
例如，PAB 意味着您可以在输出较少的更紧凑板卡上使用相同的飞行控制器硬件，或在与伴随计算机集成的板卡上使用等等。

以下载板和飞行控制器符合 PAB 标准，因此可以互换使用。

::: info
标准的"机械设计"部分提供了供应商之间机械兼容性的具体建议。
此处列出的飞行控制器和基板预期符合所有建议。
:::

## PAB 兼容载板

- [ARK Electronics Pixhawk 自驾仪总线载板](../flight_controller/ark_pab.md)
- [Holybro Pixhawk 标准基板](https://holybro.com/products/pixhawk-baseboards)
- [Holybro Pixhawk Mini 基板](https://holybro.com/products/pixhawk-baseboards)
- [Holybro Pixhawk RPi CM4 基板](../companion_computer/holybro_pixhawk_rpi_cm4_baseboard.md)（集成伴随/飞行控制器板）

## PAB 兼容飞行控制器

- [ARK Electronics ARKV6X](../flight_controller/ark_v6x.md)
- [Holybro Pixhawk 5X (FMUv5X)](../flight_controller/pixhawk5x.md)
- [Holybro Pixhawk 6X (FMUv6X)](../flight_controller/pixhawk6x.md)
- [CUAV Pixhawk V6X (FMUv6X)](../flight_controller/cuav_pixhawk_v6x.md)