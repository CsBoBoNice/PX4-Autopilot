# 模块参考: 估计器



## AttitudeEstimatorQ

源代码: [modules/attitude_estimator_q](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/attitude_estimator_q)


### 描述
姿态估计器 q。


### 用法 {#AttitudeEstimatorQ_usage}

```
AttitudeEstimatorQ <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## airspeed_estimator

源代码: [modules/airspeed_selector](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/airspeed_selector)


### 描述
此模块提供了一个单一的 airspeed_validated 主题，包含指示空速 (IAS)、
校准空速 (CAS)、真空速 (TAS) 以及估计当前是否无效的信息，
以及基于传感器读数还是基于地速减去风速的信息。
支持多个"原始"空速输入，此模块在故障检测时自动切换
到有效传感器。对于故障检测以及从 IAS 到 CAS 的比例因子估计，
它运行几个风速估计器并也发布这些估计器。


### 用法 {#airspeed_estimator_usage}

```
airspeed_estimator <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## ekf2

源代码: [modules/ekf2](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/ekf2)


### 描述
使用扩展卡尔曼滤波器的姿态和位置估计器。用于多旋翼和固定翼。

文档可以在 [ECL/EKF 概述与调优](https://docs.px4.io/main/en/advanced_config/tuning_the_ecl_ekf.html) 页面找到。

ekf2 可以在重放模式下启动 (`-r`)：在此模式下，它不访问系统时间，而只使用
传感器主题的时间戳。


### 用法 {#ekf2_usage}

```
ekf2 <command> [arguments...]
 Commands:
   start
     [-r]        启用重放模式

   stop

   status        打印状态信息
     [-v]        详细 (打印所有状态和完整协方差矩阵)

   select_instance 请求切换到新的估计器实例
     <instance>  指定所需的估计器实例
```

## local_position_estimator

源代码: [modules/local_position_estimator](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/local_position_estimator)


### 描述
使用扩展卡尔曼滤波器的姿态和位置估计器。


### 用法 {#local_position_estimator_usage}

```
local_position_estimator <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```

## mc_hover_thrust_estimator

源代码: [modules/mc_hover_thrust_estimator](https://github.com/PX4/PX4-Autopilot/tree/main/src/modules/mc_hover_thrust_estimator)


### 描述


### 用法 {#mc_hover_thrust_estimator_usage}

```
mc_hover_thrust_estimator <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```