# 故障安全状态机仿真

<Badge type="tip" text="PX4 v1.14" />

此页面可用于仿真 PX4 故障安全状态机在所有可能配置和条件下的操作。

仿真在浏览器中运行与在飞行器上执行的相同代码，实时运行（仿真会自动与最新版本的代码保持同步）。
请注意，任何延迟操作（`COM_FAIL_ACT_T`）在仿真中也会被延迟。

使用方法：

1. 首先在左侧配置参数。
   初始值对应于 PX4 默认值。
2. 设置飞行器类型
3. 在**状态**中设置其他值或在**条件**下设置任何标志
   - **预期模式**对应通过遥控或地面站（或外部脚本）发出的命令模式。
     故障安全状态机可以在故障安全情况下覆盖此模式。
4. 检查**输出**下的操作
5. 检查更改模式或**移动遥控摇杆**时会发生什么
6. 尝试不同的设置和条件！

仿真也可以在本地执行，以便测试特定版本或一组更改：

```sh
make run_failsafe_web_server
```

<iframe :src="withBase('/config/failsafe/index.html')" frameborder="0" height="1400px" style="text-align: center; margin-left: -20px; margin-right: -230px;" width="1200"></iframe>

<script setup>
import { withBase } from 'vitepress';
</script>
