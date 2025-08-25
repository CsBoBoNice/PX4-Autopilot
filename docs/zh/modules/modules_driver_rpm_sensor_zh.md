# 模块参考: 转速传感器 (驱动程序)

## pcf8583

源代码: [drivers/rpm/pcf8583](https://github.com/PX4/PX4-Autopilot/tree/main/src/drivers/rpm/pcf8583)

### 用法 {#pcf8583_usage}

```
pcf8583 <command> [arguments...]
 Commands:
   start
     [-I]        内部 I2C 总线
     [-X]        外部 I2C 总线
     [-b <val>]  板级特定总线 (默认=全部) (外部 SPI: 第 n 个总线
                 (默认=1))
     [-f <val>]  总线频率 kHz
     [-q]        静默启动 (如果未找到设备则无消息)
     [-a <val>]  I2C 地址
                 默认: 80
     [-k]        如果初始化 (探测) 失败，则定期继续重试

   stop

   status        打印状态信息
```