# Holybro Kopis 2

[Holybro Kopis 2](https://holybro.com/products/kopis2-hdv-free-shipping) 是一架用于 FPV 飞行或目视飞行的即飞竞速四轴飞行器。

![Kopis 2](../../assets/hardware/holybro_kopis2.jpg)

## 购买渠道

_Kopis 2_ 可以从多个供应商购买，包括：

- [Holybro](https://holybro.com/products/kopis2-hdv-free-shipping) <!-- item code 30069, 30070 -->
- [GetFPV](https://www.getfpv.com/holybro-kopis-2-6s-fpv-racing-drone-pnp.html)

此外您还需要：

- 遥控发射机。_Kopis 2_ 可以配备 FrSky 接收机或不配备接收机。
- LiPo 电池和充电器。
- 如果您想进行 FPV 飞行，需要 FPV 眼镜。
  有许多兼容选项，包括来自 [Fatshark](https://www.fatshark.com/product-page/dominator-v3) 的这些选项。
  如果您有 Kopis 2 的 HDV 版本，您也可以使用大疆 FPV 眼镜。

  ::: info
  FPV 支持完全独立于 PX4/飞控。
  :::

## 刷写 PX4 Bootloader

_Kopis 2_ 预装了 Betaflight。

在加载 PX4 固件之前，您必须首先安装 PX4 bootloader。
安装 bootloader 的说明可以在 [Kakute F7](../flight_controller/kakutef7.md#bootloader) 主题中找到（这是 _Kopis 2_ 上的飞控板）。

:::tip
如果您需要，以后总是可以 [重新安装 Betaflight](../advanced_config/bootloader_update_from_betaflight.md#reinstall-betaflight)！
:::

## 安装/配置

安装 bootloader 后，您应该能够通过 USB 电缆将飞行器连接到 _QGroundControl_。

::: info
在撰写本文时，_Kopis 2_ 在 QGroundControl _Daily Build_ 上受支持，并且仅为 master 分支提供预构建固件（尚不提供稳定版本）。
:::

要安装和配置 PX4：

- [加载 PX4 固件](../config/firmware.md)。
- [设置机架](../config/airframe.md) 为 _Holybro Kopis 2_。
- 继续进行 [基本配置](../config/index.md)，包括传感器校准和无线电设置。
