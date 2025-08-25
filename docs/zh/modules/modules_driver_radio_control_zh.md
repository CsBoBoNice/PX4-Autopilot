# 模块参考: 无线电控制 (驱动程序)

## crsf_rc

源代码: [drivers/rc/crsf_rc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/rc/crsf_rc)


### 描述
此模块解析 CRSF RC 上行链路协议并生成 CRSF 下行链路遥测数据


### 用法 {#crsf_rc_usage}

```
crsf_rc <command> [arguments...]
 Commands:
   start
     [-d <val>]  RC 设备
                 值: <file:dev>, 默认: /dev/ttyS3

   stop

   status        打印状态信息
```

## dsm_rc

源代码: [drivers/rc/dsm_rc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/rc/dsm_rc)


### 描述
此模块执行 Spektrum DSM RC 输入解析。


### 用法 {#dsm_rc_usage}

```
dsm_rc <command> [arguments...]
 Commands:
   start
     [-d <val>]  RC 设备
                 值: <file:dev>, 默认: /dev/ttyS3

   bind          发送 DSM 绑定命令（模块必须正在运行）

   stop

   status        打印状态信息
```

## ghst_rc

源代码: [drivers/rc/ghst_rc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/rc/ghst_rc)


### 描述
此模块执行 Ghost (GHST) RC 输入解析。


### 用法 {#ghst_rc_usage}

```
ghst_rc <command> [arguments...]
 Commands:
   start
     [-d <val>]  RC 设备
                 值: <file:dev>, 默认: /dev/ttyS3

   stop

   status        打印状态信息
```

## rc_input

源代码: [drivers/rc_input](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/rc_input)


### 描述
此模块执行 RC 输入解析并自动选择方法。支持的方法有：
- PPM
- SBUS
- DSM
- SUMD
- ST24
- TBS Crossfire (CRSF)


### 用法 {#rc_input_usage}

```
rc_input <command> [arguments...]
 Commands:
   start
     [-d <val>]  RC 设备
                 值: <file:dev>, 默认: /dev/ttyS3

   bind          发送 DSM 绑定命令（模块必须正在运行）

   stop

   status        打印状态信息
```

## sbus_rc

源代码: [drivers/rc/sbus_rc](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/rc/sbus_rc)


### 描述
此模块执行 SBUS RC 输入解析。


### 用法 {#sbus_rc_usage}

```
sbus_rc <command> [arguments...]
 Commands:
   start
     [-d <val>]  RC 设备
                 值: <file:dev>, 默认: /dev/ttyS3

   stop

   status        打印状态信息
```