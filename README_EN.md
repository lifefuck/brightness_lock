# Xiaomi 14 Pro Brightness Lock

Prevents Android / HyperOS thermal throttling from forcing down screen backlight. Supports KernelSU, APatch, and Magisk.

---

## Problem Solved

Under bright sunlight or thermal throttling conditions, Android often forces screen brightness down silently, making the screen hard to read even when manually cranked to the maximum.

This module listens to broadcast events and sysfs backlight nodes. Whenever brightness drops below the configured target, it automatically restores it to the desired value. When the screen turns off, it enters a deep sleep state with zero CPU and power overhead.

---

## Platform Compatibility

| Root Manager | Daemon | WebUI Panel | Notes |
| :--- | :---: | :---: | :--- |
| **KernelSU (KSU)** | Supported | Supported | Full Material 3 WebUI panel |
| **APatch** | Supported | Supported | Reuses KSU WebUI API |
| **Magisk / Kitsune Mask** | Supported | Terminal / Config | Controlled via config file |

---

## Device & Node Support

- **Primary Device**: Xiaomi 14 Pro (HyperOS)
- **General Support**: Automatically discovers backlight nodes under `/sys/class/backlight/*/brightness` on startup.

---

## Installation

### Prerequisites
- Unlocked bootloader;
- Rooted with KernelSU, APatch, or Magisk.

### Steps
1. Download the latest module zip from [Releases](https://github.com/lifefuck/brightness_lock/releases);
2. Root Manager ➔ Modules ➔ Install from storage ➔ select zip;
3. Confirm with volume keys: **[Volume+]** to install, **[Volume-]** to cancel;
4. Reboot device.

---

## Usage

### 1. KSU / APatch (WebUI)
1. Open Root Manager ➔ Modules ➔ tap the **WebUI** icon on this module;
2. Turn on the **Keep Brightness Locked** toggle;
3. Adjust target brightness (100 ~ 4095) and view live logs.

### 2. Magisk / Terminal Control
Configuration file: `/data/adb/modules/brightness_lock/config`

```bash
# Enable lock
echo enabled=1 > /data/adb/modules/brightness_lock/config

# Disable lock
echo enabled=0 > /data/adb/modules/brightness_lock/config

# Check current config
cat /data/adb/modules/brightness_lock/config
```

---

## Configuration

| Key | Default | Description |
| :--- | :--- | :--- |
| `enabled` | `0` | Lock toggle (0=disabled, 1=enabled) |
| `target` | Current system brightness | Target brightness value (100~4095) |
| `interval` | `1` | Detection interval mode (1=realtime, 2=normal, 5=power save) |

---

## Uninstallation

Uninstall the module in your Root Manager and reboot. The daemon automatically shuts down once it detects module removal, without modifying system partitions.

---

## License & Credits

- **Author**: life
- **License**: [MIT](LICENSE)
