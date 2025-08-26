# 空速校准

::: info
强烈建议固定翼和VTOL飞行器使用[空速传感器](../sensor/airspeed.md)。
:::

:::warning
与大多数其他传感器驱动程序不同，空速传感器驱动程序不会自动启动。
校准前必须[通过相应参数启用](../advanced_config/parameters.md)：

- Sensirion SDP3X ([SENS_EN_SDP3X](../advanced_config/parameter_reference.md#SENS_EN_SDP3X))
- TE MS4525 ([SENS_EN_MS4525DO](../advanced_config/parameter_reference.md#SENS_EN_MS4525DO))
- TE MS5525 ([SENS_EN_MS5525DS](../advanced_config/parameter_reference.md#SENS_EN_MS5525DS))
- Eagle Tree空速传感器 ([SENS_EN_ETSASPD](../advanced_config/parameter_reference.md#SENS_EN_ETSASPD))
  :::

## 执行校准

校准空速传感器：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 如果尚未完成，请启用空速传感器（如上面_警告_中所述）。
1. 选择**"Q"图标 > 飞行器设置 > 传感器**（侧边栏）打开_传感器设置_。
1. 点击**空速**传感器按钮。

   ![空速校准](../../assets/qgc/setup/sensor/sensor_airspeed.jpg)

1. 用手遮挡传感器避免风的影响（即用手掌罩住它）。
   注意不要堵塞其任何孔洞。
1. 点击**确定**开始校准。
1. 当提示时，向皮托管尖端吹气以示校准结束。

   :::tip
   向管中吹气也是检查动压和静压端口是否正确安装的基本方法。
   如果它们被交换了，当您向管中吹气时，传感器将读取一个很大的负差压，校准将因错误而中止。
   :::

1. _QGroundControl_ 然后告诉您校准是否成功。

## 更多信息

- [空速验证](../advanced_config/airspeed_validation.md)。
- [QGroundControl用户指南 > 传感器](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors_px4.html#airspeed)
