# 小米14 Pro 亮度锁定 (Brightness Lock)

用于防止 Android / HyperOS 温控策略强行压低屏幕背光。支持 KernelSU、APatch 与 Magisk。

---

## 解决的问题

在户外高照度或机身发热场景下，系统的温控策略常会在后台强制下调屏幕背光，导致手动拉满仍然无法看清屏幕。

本模块通过监听系统广播与 sysfs 节点事件，当检测到当前背光低于设定目标值时，自动将亮度恢复至目标值；息屏时挂起休眠，不占用额外 CPU 与电池功耗。

---

## 平台兼容性

| 管理器 | 守护功能 | WebUI 控制台 | 说明 |
| :--- | :---: | :---: | :--- |
| **KernelSU (KSU)** | 支持 | 支持 | 完整支持 Material 3 控制面板 |
| **APatch** | 支持 | 支持 | 复用 KSU WebUI 接口 |
| **Magisk / 狐狸面具** | 支持 | 终端配置文件 | 官方 Magisk 不支持 WebUI，通过命令行/配置文件控制 |

---

## 机型与节点支持

- **主要测试机型**：小米 14 Pro (HyperOS)
- **通用支持**：守护脚本启动时会自动探测 `/sys/class/backlight/*/brightness` 节点，其他高通/联发科机型亦具备通用兼容性。

---

## 安装说明

### 前提条件
- 设备已解锁 Bootloader；
- 已刷入 KernelSU / APatch / Magisk 之一。

### 刷入步骤
1. 前往 [Releases 页面](https://github.com/lifefuck/brightness-lock/releases) 下载最新模块 Zip 包；
2. 打开 Root 管理器 ➔ 模块 ➔ 本地安装 ➔ 选择 Zip；
3. 音量键确认安装：**[音量+]** 确认，**[音量-]** 取消；
4. 重启设备。

---

## 使用方式

### 1. KSU / APatch（WebUI 控制台）
1. 打开 Root 管理器 ➔ 模块 ➔ 点击本模块的 **WebUI 图标**；
2. 开启 **保持高亮锁定** 开关；
3. 支持在面板中实时调节目标亮度（100 ~ 4095）并查看实时运行日志。

### 2. Magisk / 终端控制
配置文件路径：`/data/adb/modules/brightness_lock/config`

```bash
# 开启锁定
echo enabled=1 > /data/adb/modules/brightness_lock/config

# 关闭锁定
echo enabled=0 > /data/adb/modules/brightness_lock/config

# 查看当前配置
cat /data/adb/modules/brightness_lock/config
```

---

## 配置参数

| 参数名 | 默认值 | 说明 |
| :--- | :--- | :--- |
| `enabled` | `0` | 锁定开关（0=关闭，1=开启） |
| `target` | 系统当前亮度 | 目标锁定亮度（取值范围 100~4095） |
| `interval` | `1` | 守护灵敏度（1=实时侦测，2=普通，5=低频节能） |

---

## 卸载

在 Root 管理器中直接点击卸载模块并重启。守护脚本检测到模块目录被删除后会自动终止，不修改系统分区。

---

## 许可证与署名

- **作者**：life
- **许可证**：[MIT](LICENSE)
