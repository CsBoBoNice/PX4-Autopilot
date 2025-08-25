# 模块参考: 模板



## module

源代码: [templates/template_module](https://github.com/PX4/PX4-Autopilot/tree/main/src/templates/template_module)


### 描述
描述所提供模块功能的部分。

这是一个在后台作为任务运行的模块模板，具有启动/停止/状态功能。

### 实现
描述此模块高级实现的部分。

### 示例
CLI 使用示例：
```
module start -f -p 42
```


### 用法 {#module_usage}

```
module <command> [arguments...]
 Commands:
   start
     [-f]        可选示例标志
     [-p <val>]  可选示例参数
                 默认: 0

   stop

   status        打印状态信息
```

## work_item_example

源代码: [examples/work_item](https://github.com/PX4/PX4-Autopilot/tree/main/src/examples/work_item)


### 描述
在工作队列中运行的简单模块示例。


### 用法 {#work_item_example_usage}

```
work_item_example <command> [arguments...]
 Commands:
   start

   stop

   status        打印状态信息
```