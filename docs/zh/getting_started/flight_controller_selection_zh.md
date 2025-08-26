# 飞行控制器选择

飞行控制器是无人飞行器的"大脑"。
PX4 可以在[多种飞行控制器板](../flight_controller/index.md)上运行。

您应该选择适合您飞行器物理约束、您希望执行的活动，当然还有成本的板子。

<img src="../../assets/flight_controller/pixhawk6x/pixhawk6x_hero_upright.png" width="120px" title="Holybro Pixhawk6X"><img src="../../assets/flight_controller/cuav_pixhawk_v6x/pixhawk_v6x.jpg" width="200px" title="CUAV Pixhawk 6X" ><img src="../../assets/flight_controller/cube/orange/cube_orange_hero.jpg" width="250px" title="CubePilot Cube Orange" />

## Pixhawk 系列

[Pixhawk 系列](../flight_controller/pixhawk_series.md)开源硬件飞行控制器在 NuttX 操作系统上运行 PX4。
具有多种外形因子，有针对多种使用案例和细分市场的版本。

[Pixhawk 标准自动驾驶仪](../flight_controller/autopilot_pixhawk_standard.md)被用作 PX4 参考平台。
它们得到 PX4 开发团队的支持和测试，强烈推荐使用。

## 制造商支持的控制器

其他飞行控制器是[制造商支持的](../flight_controller/autopilot_manufacturer_supported.md)。
这包括大量基于 Pixhawk 标准（但不完全符合标准）的飞控，以及许多其他产品。

请注意，制造商支持的控制器可以与 Pixhawk 标准控制器一样"好"（或更好）。

## 用于计算密集型任务的自动驾驶仪

像 Pixhawk 这样的专用飞行控制器通常不太适合通用计算或运行计算密集型任务。
为了获得更多计算能力，最常见的方法是在单独的机载[伴随计算机](../companion_computer/index.md)上运行这些应用程序。
一些伴随计算机也可以在单独的 DSP 上运行 PX4，作为同一自动驾驶仪板的一部分。

同样，PX4 也可以在树莓派上原生运行（这种方法通常不被认为与使用单独的伴随计算机或专用 DSP 一样"稳健"）：

- [树莓派 2/3 Navio2](../flight_controller/raspberry_pi_navio2.md)
- [树莓派 2/3/4 PilotPi Shield](../flight_controller/raspberry_pi_pilotpi.md)


## 可以运行 PX4 的商用无人机

PX4 可在许多流行的商用无人机产品上使用，包括一些出厂预装 PX4 的产品和其他可以更新为 PX4 的产品（允许您为您的飞行器添加任务规划和其他 PX4 飞行模式）。

更多信息请参见[完整飞行器](../complete_vehicles/index.md)。
