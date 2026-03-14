# ESP32-CAM 摄像头节点 | ESP32-CAM Camera Node

[中文](#中文) | [English](#english)

---

## 中文

📷 基于 ESP32-CAM 开发板的 Home Assistant 网络摄像头

![ESP32](https://img.shields.io/badge/ESP32-CAM-blue)
![Home Assistant](https://img.shields.io/badge/Home_Assistant-Integration-blue)
![ESPHome](https://img.shields.io/badge/ESPHome-2024.11+-green)

---

### 🎯 功能特性

- ✅ **实时视频流** - Home Assistant 直接查看
- ✅ **PSRAM 支持** - 外挂内存，流畅运行
- ✅ **闪光灯控制** - GPIO4 补光灯
- ✅ **XGA 分辨率** - 1024x768
- ✅ **JPEG 压缩** - 高质量图像
- ✅ **I2C 总线** - 独立摄像头 I2C
- ✅ **OTA 更新** - 无线升级

### 📦 硬件清单

| 组件 | 型号 | 数量 | 备注 |
|------|------|------|------|
| 主控板 | ESP32-CAM | 1 | OV2640 摄像头 |
| 电源 | 5V 2A | 1 | 推荐独立供电 |
| 杜邦线 | - | 若干 | 编程用 |
| FTDI 模块 | CP2102/CH340 | 1 | 上传程序用 |

### 🔌 GPIO 分配

| 功能 | GPIO | 功能 | GPIO |
|------|------|------|------|
| I2C SDA | GPIO26 | 数据 D0 | GPIO5 |
| I2C SCL | GPIO27 | 数据 D1 | GPIO18 |
| VSYNC | GPIO25 | 数据 D2 | GPIO19 |
| HREF | GPIO23 | 数据 D3 | GPIO21 |
| PCLK | GPIO22 | 数据 D4 | GPIO36 |
| XCLK | GPIO0 | 数据 D5 | GPIO39 |
| PWDN | GPIO32 | 数据 D6 | GPIO34 |
| 闪光灯 | GPIO4 | 数据 D7 | GPIO35 |

### 🚀 快速开始

```bash
# 安装 ESPHome
pip3 install esphome

# 配置密钥
cp secrets.example.yaml secrets.yaml

# 编译
esphome compile esp32-cam.yaml

# 上传 (首次需要 USB 连接)
esphome upload esp32-cam.yaml

# 后续 OTA 更新
esphome upload esp32-cam.yaml --device 192.168.2.XXX
```

### 🏠 Home Assistant 集成

**自动发现:**
- ESPHome 集成会自动发现摄像头
- 实体：`camera.esp32_camera`
- 开关：`light.摄像头闪光灯`

**Lovelace 卡片:**
```yaml
type: picture
entity: camera.esp32_camera
camera_view: live
```

### 📁 文件说明

```
esp32-cam-node/
├── README.md                 # 本文件
├── esp32-cam.yaml            # ESPHome 配置
└── secrets.example.yaml      # 密钥模板
```

### ⚙️ 配置说明

#### 分辨率选项
```yaml
resolution:
  - FRAMESIZE_96X96    # 96x96
  - FRAMESIZE_QQVGA    # 160x120
  - FRAMESIZE_QCIF     # 176x144
  - FRAMESIZE_HQVGA    # 240x176
  - FRAMESIZE_240X240  # 240x240
  - FRAMESIZE_QVGA     # 320x240
  - FRAMESIZE_CIF      # 400x296
  - FRAMESIZE_HVGA     # 480x320
  - FRAMESIZE_VGA      # 640x480
  - FRAMESIZE_SVGA     # 800x600
  - FRAMESIZE_XGA      # 1024x768 ← 默认
  - FRAMESIZE_HD       # 1280x720
  - FRAMESIZE_SXGA     # 1280x1024
  - FRAMESIZE_UXGA     # 1600x1200
```

#### JPEG 质量
```yaml
jpeg_quality: 10  # 1-63, 越小质量越高
```

### 🔧 故障排除

#### 无法连接
- 检查 WiFi 密码
- 确认电源充足 (建议 5V 2A)
- 查看串口日志

#### 图像花屏
- 检查排线连接
- 降低分辨率
- 增加 `jpeg_quality` 值

#### 无法上传
- 按住板载 FLASH 按钮
- 连接 RST 到 GND 重启
- 使用 FTDI 模块

---

## English

📷 Home Assistant network camera based on ESP32-CAM development board

### 🎯 Features

- ✅ **Live Video Stream** - View directly in Home Assistant
- ✅ **PSRAM Support** - External memory for smooth operation
- ✅ **Flashlight Control** - GPIO4 fill light
- ✅ **XGA Resolution** - 1024x768
- ✅ **JPEG Compression** - High quality images
- ✅ **I2C Bus** - Dedicated camera I2C
- ✅ **OTA Updates** - Wireless firmware updates

### 📦 Hardware List

| Component | Model | Qty | Notes |
|-----------|-------|-----|-------|
| Main Board | ESP32-CAM | 1 | OV2640 camera |
| Power Supply | 5V 2A | 1 | Independent power recommended |
| Jumper Wires | - | Several | For programming |
| FTDI Module | CP2102/CH340 | 1 | For uploading |

### 🔌 GPIO Assignment

| Function | GPIO | Function | GPIO |
|----------|------|----------|------|
| I2C SDA | GPIO26 | Data D0 | GPIO5 |
| I2C SCL | GPIO27 | Data D1 | GPIO18 |
| VSYNC | GPIO25 | Data D2 | GPIO19 |
| HREF | GPIO23 | Data D3 | GPIO21 |
| PCLK | GPIO22 | Data D4 | GPIO36 |
| XCLK | GPIO0 | Data D5 | GPIO39 |
| PWDN | GPIO32 | Data D6 | GPIO34 |
| Flashlight | GPIO4 | Data D7 | GPIO35 |

### 🚀 Quick Start

```bash
# Install ESPHome
pip3 install esphome

# Configure secrets
cp secrets.example.yaml secrets.yaml

# Compile
esphome compile esp32-cam.yaml

# Upload (USB required for first time)
esphome upload esp32-cam.yaml

# OTA updates
esphome upload esp32-cam.yaml --device 192.168.2.XXX
```

### 🏠 Home Assistant Integration

**Auto Discovery:**
- ESPHome integration auto-discovers camera
- Entity: `camera.esp32_camera`
- Switch: `light.camera_flashlight`

**Lovelace Card:**
```yaml
type: picture
entity: camera.esp32_camera
camera_view: live
```

### 📁 File Structure

```
esp32-cam-node/
├── README.md                 # This file
├── esp32-cam.yaml            # ESPHome config
└── secrets.example.yaml      # Secrets template
```

### ⚙️ Configuration

#### Resolution Options
```yaml
resolution:
  - FRAMESIZE_96X96    # 96x96
  - FRAMESIZE_QQVGA    # 160x120
  - FRAMESIZE_QCIF     # 176x144
  - FRAMESIZE_HQVGA    # 240x176
  - FRAMESIZE_240X240  # 240x240
  - FRAMESIZE_QVGA     # 320x240
  - FRAMESIZE_CIF      # 400x296
  - FRAMESIZE_HVGA     # 480x320
  - FRAMESIZE_VGA      # 640x480
  - FRAMESIZE_SVGA     # 800x600
  - FRAMESIZE_XGA      # 1024x768 ← Default
  - FRAMESIZE_HD       # 1280x720
  - FRAMESIZE_SXGA     # 1280x1024
  - FRAMESIZE_UXGA     # 1600x1200
```

#### JPEG Quality
```yaml
jpeg_quality: 10  # 1-63, lower = higher quality
```

### 🔧 Troubleshooting

#### Cannot Connect
- Check WiFi password
- Ensure adequate power (5V 2A recommended)
- Check serial logs

#### Corrupted Image
- Check ribbon cable connection
- Lower resolution
- Increase `jpeg_quality` value

#### Cannot Upload
- Hold onboard FLASH button
- Connect RST to GND to restart
- Use FTDI module

---

## 📄 许可证 | License

MIT License

---

## 🙏 致谢 | Credits

- [ESPHome](https://esphome.io/)
- [Home Assistant](https://www.home-assistant.io/)
- [ESP32-CAM](https://www.espressif.com/en/products/modules/esp32)

---

## 📬 联系方式 | Contact

- GitHub: [@Jane84894](https://github.com/Jane84894)
- Issues: [Issues](https://github.com/Jane84894/esp32-cam-node/issues)

---

**⭐ 如果这个项目对你有帮助，请给个 Star! | If this project helps you, please give a Star!**
