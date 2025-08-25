---
# https://vitepress.dev/reference/default-theme-home-page
layout: home

hero:
  name: "PX4"
  text: "用户指南"
  tagline: PX4 是面向专业无人机开发者的开源自动驾驶仪。
  image: /logo_pro_small.png
  actions:
    - theme: brand
      text: 阅读文档
      link: /en/index.md
    - theme: alt
      text: 官方网站
      link: https://px4.io/
    - theme: alt
      text: GitHub 源代码
      link: https://github.com/PX4/PX4-Autopilot

features:
  - title: 模块化架构
    details: PX4 在硬件和软件方面都具有高度的模块化和可扩展性。它采用基于端口的架构 - 这意味着当开发者添加组件时，扩展的系统不会失去稳健性或性能。
  - title: 开源
    details: PX4 由全球开发社区共同开发。该飞行栈不仅仅满足一个实验室或一家公司的需求，而是作为通用工具包设计，在业界得到广泛使用和采用。
  - title: 可配置性
    details: PX4 为从事集成工作的开发者提供优化的 API 和 SDK。所有模块都是独立的，可以轻松替换为不同的模块，无需修改核心。功能易于部署和重新配置。
  - title: 自主性栈
    details: PX4 设计为与嵌入式计算机视觉深度耦合，以实现自主功能。该框架降低了开发者在定位和障碍物检测算法方面的入门门槛。
  - title: 现实世界验证
    details: 全球已部署数千个基于 PX4 的商业系统。与此同时，专门的飞行测试团队每月累计数千飞行小时，进行硬件和软件测试，确保代码库的安全性和可靠性。
  - title: 宽松许可证
    details: PX4 在宽松的 BSD 3 条款许可证条款下可以自由使用和修改。这意味着该软件也允许专有使用，并允许在许可证下发布的版本合并到专有产品中。
  - title: 互操作性
    details: 除了作为稳健的飞行栈外，PX4 还提供了支持设备的生态系统。该项目还主导了通信、外设集成和电源管理解决方案发展的标准化工作。

  - title: 强大的安全功能
    details: 出色的安全功能包括自动故障安全行为、对不同返回模式的支持、降落伞等，默认已包含在代码库中。这些功能易于配置，可为定制系统调整。

search: false
footer: BSD 3 条款许可证
---

<!-- <Redirect to="/en/README.md" /> -->
