# ScreenTranslator 屏幕翻译

鼠标指向哪段译哪段的屏幕翻译工具。

## 功能

* 框选屏幕区域，自动 OCR 识别文字并翻译

* 鼠标移到文字上，弹出译文气泡（跟随模式）

* 或切换为面板模式，固定显示整个区域的全部译文

* 多语言识别（中/英/日/韩等），自动检测源语言

* 在线翻译聚合（有道 + Google CN + MyMemory），可配置百度/DeepL Key

* 悬浮球常驻，鼠标穿透不抢焦点

* 译文缓存 + 去重，避免重复请求

## 快捷键

| 快捷键   | 功能     | 说明                    |
| ----- | ------ | --------------------- |
| Alt+S | 框选区域   | 按**两次**完成：第一次开始，第二次确定 |
| Alt+X | 暂停/继续  | 切换监控状态，关闭翻译显示         |
| Alt+D | 切换显示模式 | 跟随模式 ↔ 面板模式           |

> 所有快捷键均可在设置面板中自定义。

## 使用方法

### 开发模式

```powershell
pip install -r requirements.txt
python main.py
```

### 打包为 exe

```powershell
pyinstaller screen_translator.spec --noconfirm
```

产物：`dist\ScreenTranslator\ScreenTranslator.exe`

> **注意**：必须移动整个 `ScreenTranslator` 文件夹，不能只移动 `.exe`（依赖在 `_internal` 目录下）。

### 运行

1. 启动后屏幕右上角出现绿色悬浮球
2. 按 Alt+S，移动鼠标画框，再按 Alt+S 完成框选
3. 等待 OCR + 翻译完成（悬浮球变橙）
4. 鼠标移到框选区域内文字上，看译文气泡
5. 按 Alt+D 切换面板模式查看全部译文
6. 右键悬浮球可快速访问菜单（设置/框选/暂停/退出）

## 设置项

单击悬浮球打开设置面板：

* **目标语言**：默认简体中文（可选英/日/韩/俄/法/德）

* **字体颜色**：默认 `#00ff00` 绿色

* **字体大小**：默认 14px

* **翻译引擎**：可填百度 AppID/SecretKey 或 DeepL API Key 提升稳定性

* **快捷键**：框选/暂停/切换模式均可自定义

## 技术栈

* Python + PySide6（透明置顶窗口 + 鼠标穿透）

* PaddleOCR（离线 OCR，多语言）

* 在线翻译聚合（有道 + Google CN + MyMemory）

* OpenCV（帧差检测，内容变化才重新 OCR）

* PyInstaller（打包）

## 已知限制

* 需联网翻译（断网时翻译失效）

* 首次启动需下载 PaddleOCR 模型（约 30MB，缓存后秒开）

* 打包体积约 800MB-1.2GB（PaddleOCR 运行时固有代价）

