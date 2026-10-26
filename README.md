# 小米14 Pro 亮度锁定 (Brightness Lock)

解决小米 14 Pro 在澎湃 HyperOS 下玩游戏、发热或户外强光时，温控强行把屏幕亮度压暗的问题。

## 原理

后台监控背光节点，一旦被系统温控压暗，就自动改回设定的亮度数值。
息屏时自动休眠，不占 CPU 也不耗电，亮屏恢复锁定。模块默认是关闭的，不会开机强制锁定，需要时在 WebUI 里开启即可。

## 兼容性与控制方式

| 环境 | 锁定功能 | WebUI 控制 | 使用方式 |
| :--- | :---: | :---: | :--- |
| KernelSU | 支持 | 支持 | 模块页面直接点图标打开 WebUI 调节 |
| APatch | 支持 | 支持 | 模块页面进入 WebUI 调节 |
| Magisk | 支持 | 无 | 修改配置文件 `/data/adb/modules/brightness_lock/config` |

## 安装

1. 在 Releases 下载最新的模块 zip。
2. 打开 KSU / APatch / Magisk 本地刷入。
3. 按音量键确认，重启手机。

## 使用

### KernelSU / APatch
直接在模块列表点开 WebUI：
- 打开锁定开关。
- 滑动或手动输入亮度数值（100 ~ 4095）。
- 底部可以查看实时日志。

### Magisk / 终端控制
修改配置文件 `/data/adb/modules/brightness_lock/config`：

```bash
# 开启锁定
echo enabled=1 > /data/adb/modules/brightness_lock/config

# 关闭锁定
echo enabled=0 > /data/adb/modules/brightness_lock/config

# 修改目标亮度为 3000
echo target=3000 >> /data/adb/modules/brightness_lock/config
```

## 卸载

在管理器中直接卸载模块并重启手机即可。不修改任何系统分区，不留后台残留。

## 作者

- life
