# SPRacingH7EXTREME（PX4版本）

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://shop.seriouslypro.com)获取硬件支持或合规问题。
:::

[SPRacingH7EXTREME](https://shop.seriouslypro.com/sp-racing-h7-extreme)是一个功能丰富的FC/PDB，具有双ICM20602陀螺仪、H7 400/480Mhz(+) CPU、高精度BMP388气压计、SD卡插槽、电流传感器、8个易于访问的电机输出、OSD、麦克风、音频输出等功能。

它可以轻松用于小到大型四轴飞行器、飞机、八旋翼和更高级的机架。
最好与独立ESC一起使用，因为它具有内置电源分配板（PDB）。
连接4合1 ESC也很容易。

还有一个12引脚堆叠连接器，提供4个额外的电机输出、SPI和UART连接。

![SPRacingH7EXTREME PCB顶部](../../assets/flight_controller/spracingh7extreme/spracingh7extreme-top.jpg)

![SPRacingH7EXTREME PCB底部](../../assets/flight_controller/spracingh7extreme/spracingh7extreme-bottom.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 主要特性

- 主系统芯片：[STM32H750VBT6 rev.y/v](https://www.st.com/en/microcontrollers-microprocessors/stm32h750vb.html)
  - CPU：400/480Mhz(+) ARM Cortex M7，带单精度FPU。（+ Rev V CPU可达480Mhz）
  - RAM：1MB
  - 16MB外部闪存，4位QuadSPI，内存映射模式用于代码_和_配置。
- 板载传感器：
  - 双陀螺仪（各1个SPI，带独立中断信号，支持32khz，支持fsync）
  - 高精度BMP388气压计（I2C + 中断）
  - 110A电流传感器
- 通过外部8引脚IO端口连接GPS。
- 音频/视频
  - 屏幕显示OSD（专用SPI，基于字符，MAX7456）
  - 麦克风传感器
  - CPU DAC音频输出。
  - 麦克风/DAC输出音频混合器。
- 接口
  - SD卡（4位SDIO，非1位SPI）
  - IR应答器（iLAP兼容）
  - 蜂鸣器电路
  - RSSI（模拟/PWM）
  - 12个电机输出（4个在电机焊盘上，4个在中间，4个在堆叠连接器上）。
  - 1个SPI分线至堆叠连接器
  - 6个串口（5个TX和RX，1个仅TX双向遥测）
  - 启动按钮（侧按）
  - 绑定/用户按钮（侧按）
  - 接收器端口（所有常用协议，无需反相器）
  - CAM插座上的CAM OSD控制和视频输入。
  - SWD调试端口。
- VTX插座上的视频输出+音频输出。
- 带OTG功能的USB（ID和VBUS连接到CPU）
- 电源系统
  - 集成PDB。
  - 2-6S BEC
  - TVS保护二极管
  - 陀螺仪专用500ma稳压器，带陀螺仪噪音滤波电容。
  - CPU、气压计、麦克风等第二个500ma稳压器。
- 其他功能
  - 状态LED
  - LED灯带支持（带精心设计的连接焊盘）。
  - 可从SD卡或外部闪存启动。
  - 可从SD卡刷新。
  - 从顶部焊接设计。
  - PCB镂空用于电池线。
  - 无指南针，使用连接到GPS IO端口的带磁力计/指南针传感器的外部GPS。
  - 还可运行Betaflight 4.x+、Cleanflight 4.x+。
  - 由创建Cleanflight的Dominic Clifton设计
- 尺寸
  - 36x36mm，30.5\*30.5安装孔距，M4孔。
  - 提供软安装M4到M3护套。

## 购买地点

SPRacingH7EXTREME可从[Seriously Pro商店](https://shop.seriouslypro.com/sp-racing-h7-extreme)购买。

::: info
购买时请选择PX4版本！
:::

## 手册、引脚图和连接图

带引脚图的手册可从[这里](http://seriouslypro.com/files/SPRacingH7EXTREME-Manual-latest.pdf)下载。
其他图表请参见[SPRacingH7EXTREME网站](http://seriouslypro.com/products/spracingh7extreme)。

## 致谢

此设计由[Dominic Clifton](https://github.com/hydra)创建
初始PX4支持由[Igor-Misic](https://github.com/Igor-Misic)提供
