# 模块参考: 应答器 (驱动程序)

## sagetech_mxs

源代码: [drivers/transponder/sagetech_mxs](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/transponder/sagetech_mxs)


	### 描述

	此驱动程序集成 Sagetech MXS 认证应答器以发送和接收 ADSB 消息和交通信息。

	### 示例

	尝试在指定的串行设备上启动驱动程序。
	$ sagetech_mxs start -d /dev/ttyS1
	停止驱动程序
	$ sagetech_mxs stop
	设置航班 ID (最多 8 个字符)
	$ sagetech_mxs flight_id MXS12345
	设置 MXS 操作模式
	$ sagetech_mxs opmode off/on/stby/alt
	$ sagetech_mxs opmode 0/1/2/3
	设置应答机代码
	$ sagetech_mxs squawk 1200
	
### 用法 {#sagetech_mxs_usage}

```
sagetech_mxs <command> [arguments...]
 Commands:
   start         启动驱动程序
     -d <val>    串行设备

   stop          停止驱动程序

   flightid      设置航班 ID (最多 8 个字符)

   ident         在 ADSB-Out 消息中设置 IDENT 位

   opmode        设置 MXS 操作模式。('off', 'on', 'stby', 'alt', 或
                 数值 [0-3])

   squawk        设置应答机代码。[0-7777] 八进制 (没有大于 7 的数字)
```