# 模块参考: 仿真



## simulator_sih

源代码: [modules/simulation/simulator_sih](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/simulation/simulator_sih)


### 描述
此模块为在硬件自动驾驶仪内部完全运行的四旋翼和固定翼提供模拟器。

此模拟器订阅"actuator_outputs"，这是控制分配模块给出的执行器 PWM 信号。

此模拟器发布受现实噪声干扰的传感器信号，
以便将状态估计器纳入回路。

### 实现
模拟器使用矩阵代数实现运动方程。
使用四元数表示姿态。
使用前向欧拉法进行积分。
大多数变量在 .hpp 文件中声明为全局变量，以避免堆栈溢出。



### 用法 {#simulator_sih_usage}

```
simulator_sih <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```