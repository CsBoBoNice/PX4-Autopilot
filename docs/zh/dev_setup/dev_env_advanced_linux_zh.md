# 高级 Linux 安装用例

## 使用 JTAG 编程适配器

Linux 用户需要显式允许访问 USB 总线以使用 JTAG 编程适配器。

::: info
对于 Archlinux：在以下命令中将组 plugdev 替换为 uucp
:::

在 `sudo` 模式下运行一个简单的 `ls` 命令以确保以下命令成功执行：

```sh
sudo ls
```

然后在临时授予 `sudo` 权限的情况下，运行此命令：

```sh
cat > $HOME/rule.tmp <<_EOF
# 所有 3D Robotics 设备（包括 PX4）
SUBSYSTEM=="usb", ATTR{idVendor}=="26AC", GROUP="plugdev"
# FTDI（和 Black Magic Probe）设备
SUBSYSTEM=="usb", ATTR{idVendor}=="0483", GROUP="plugdev"
# Olimex 设备
SUBSYSTEM=="usb",  ATTR{idVendor}=="15ba", GROUP="plugdev"
_EOF
sudo mv $HOME/rule.tmp /etc/udev/rules.d/10-px4.rules
sudo /etc/init.d/udev restart
```

用户需要被添加到 **plugdev** 组：

```sh
sudo usermod -a -G plugdev $USER
```