# 小米14 Pro 亮度锁定 (Brightness Lock)

解决小米 14 Pro（HyperOS）在玩游戏、机身发热或户外强光下，温控强制把屏幕亮度暗调降级的问题。

---

## 怎么工作的
- 后台监听屏幕背光节点，一旦被温控压暗，自动拉回设定的亮度值。
- 息屏自动彻底休眠，不吃 CPU，不耗电。
- 亮屏立刻恢复锁定。
- 默认是关闭的，不会开机盲闪，需要时在 WebUI 里点开就行。

---

## 控制与兼容

| 管理器 | 锁定功能 | WebUI 界面 | 控制方式 |
| :--- | :---: | :---: | :--- |
| **KernelSU (KSU)** | 支持 | 支持 | 模块页面直接点图标打开网页调节 |
| **APatch** | 支持 | 支持 | 复用 WebUI 网页调节 |
| **Magisk / 狐狸面具** | 支持 | 无 | 改配置文件 `/data/adb/modules/brightness_lock/config` |

---

## 安装说明
1. 到 [Releases 页面](https://github.com/lifefuck/brightness_lock/releases) 下载最新的模块 zip。
2. 打开 KSU / APatch / Magisk 刷入。
3. 按音量上键确认，刷完重启一次手机。

---

## 使用方法

### KSU / APatch
在模块列表里点进本模块的 WebUI：
- 打开「锁定开关」；
- 拖动滑块或输入数值（100 ~ 4095）设定目标亮度；
- 下面可以直接看运行日志。

### Magisk / 终端控制
配置文件路径：`/data/adb/modules/brightness_lock/config`
```bash
# 开启锁定
echo enabled=1 > /data/adb/modules/brightness_lock/config

# 关闭锁定
echo enabled=0 > /data/adb/modules/brightness_lock/config

# 改目标亮度为 3000
echo target=3000 >> /data/adb/modules/brightness_lock/config
```

---

## 卸载
管理器里直接点卸载并重启。后台脚本检测到模块删除后会自动退出自愈，不改动任何系统分区。

---

## 署名
- 作者: life
- 许可证: [MIT](LICENSE)
