<h1 align="center">ESP32 BNO085</h1>

<p align="center">
  <strong>用于 9 轴运动感知的 ESP32-S3 + BNO085 KiCad 硬件设计。</strong>
</p>

<p align="center">
  <a href="../../README.md">한국어</a> |
  <a href="README.en.md">English</a> |
  中文 |
  <a href="README.ja.md">日本語</a>
</p>

本仓库包含围绕 BNO085 9 轴智能 IMU 设计的小型 ESP32-S3 板卡 KiCad 文件。仓库跟踪原理图、PCB、局部封装库和 fabrication-toolkit 设置，不包含生成的 Gerber 和本地分析输出。

## 功能

- **ESP32-S3 模块** - 支持 Wi-Fi/BLE 的 MCU 模块封装。
- **BNO085 智能 IMU** - 加速度计、陀螺仪、磁力计和传感器融合。
- **USB-C 接口** - USB 2.0 Type-C 接口。
- **包含本地封装** - BNO085 和 Molex 连接器封装库。
- **制造导出设置** - 用于可重复生成制造文件。

## 仓库内容

```text
esp32_bno085.kicad_pro
esp32_bno085.kicad_sch
esp32_bno085.kicad_pcb
fp-lib-table
BNO085.pretty/
530480210.pretty/
fabrication-toolkit-options.json
```

## 打开项目

```powershell
git clone https://github.com/nemonamo/esp32_bno085.git
cd esp32_bno085
```

使用 KiCad 8 或更新版本打开 `esp32_bno085.kicad_pro`，确认本地封装可解析，并在导出制造文件前运行 ERC 和 DRC。

## 制造检查

- 运行 KiCad ERC 和 DRC。
- 重新导出 Gerber、钻孔文件、BOM 和 CPL。
- 检查 USB D+/D- 间距和连接器方向。
- 检查 BNO085 I2C 上拉和电源轨。
- 确认制造厂设计规则。

## 安全

生成的压缩包、订单文件、供应商导出、截图和本地笔记在审核前不要提交到 Git。

## 许可证

当前未声明开源硬件或软件许可证。公开复用、制作或接受外部贡献前，请添加 `LICENSE` 文件。
