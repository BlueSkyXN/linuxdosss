# Linux 环境安装指南

本文档面向 Linux 用户，指导在本地运行 Linux.do 论坛刷帖助手的环境准备流程。

## 1. 环境要求

- Python 3.8+
- 图形界面环境（X11/Wayland）
- Chrome 浏览器（推荐）或 Chromium

## 2. 安装系统依赖

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-tk
```

### CentOS / RHEL

```bash
sudo yum install -y python3 python3-pip python3-tkinter
```

### Arch Linux

```bash
sudo pacman -S --needed python python-pip tk
```

## 3. 安装 Python 依赖

在项目根目录执行：

```bash
pip3 install -r requirements.txt
```

## 4. 安装 Chrome 浏览器

### Ubuntu / Debian

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt-get install -f
```

### CentOS / RHEL

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
sudo yum install ./google-chrome-stable_current_x86_64.rpm
```

### Arch Linux（任选其一）

```bash
# AUR
yay -S google-chrome

# 或使用官方仓库的 Chromium
sudo pacman -S chromium
```

## 5. 运行程序

```bash
python3 linux_do_gui.py
```

## 6. 常见问题

### 6.1 提示 No module named 'tkinter'

```bash
# Ubuntu/Debian
sudo apt install -y python3-tk

# CentOS/RHEL
sudo yum install -y python3-tkinter

# Arch Linux
sudo pacman -S tk
```

### 6.2 提示 No module named 'DrissionPage'

```bash
pip3 install -r requirements.txt
```

### 6.3 浏览器打不开/无法启动

- 确认 Chrome/Chromium 已安装：
  ```bash
  google-chrome --version
  # 或
  chromium --version
  ```
- 确认不是无头环境（见 6.5）

### 6.4 程序启动正常但无法显示托盘图标

- 某些桌面环境可能需要托盘扩展（如 GNOME）
- 确保已安装 `pystray` 与 `pillow`（已包含在 requirements.txt）

### 6.5 无头服务器（无图形界面）

需要虚拟显示：

```bash
sudo apt install -y xvfb
xvfb-run python3 linux_do_gui.py
```

### 6.6 WSL 环境

- **WSL2 + Windows 11**：建议使用 WSLg（默认支持 GUI）
- 其他情况需配置 X Server，并设置 `DISPLAY` 环境变量

## 7. 快速自检（可选）

```bash
python3 - <<'PY'
import tkinter
from DrissionPage import ChromiumPage
import pystray
from PIL import Image
print("OK")
PY
```

若输出 `OK`，说明依赖基础环境已就绪。
