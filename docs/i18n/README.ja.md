<h1 align="center">ESP32 BNO085</h1>

<p align="center">
  <strong>9 軸モーションセンシング向け ESP32-S3 + BNO085 KiCad ハードウェア設計。</strong>
</p>

<p align="center">
  <a href="../../README.md">한국어</a> |
  <a href="README.en.md">English</a> |
  <a href="README.zh-CN.md">中文</a> |
  日本語
</p>

このリポジトリは、BNO085 9 軸スマート IMU を中心にした小型 ESP32-S3 ボードの KiCad 設計ファイルを含みます。回路図、PCB、ローカルフットプリント、fabrication-toolkit 設定を管理し、生成済み Gerber や分析出力は含めません。

## 機能

- **ESP32-S3 モジュール** - Wi-Fi/BLE 対応 MCU モジュールのフットプリント。
- **BNO085 スマート IMU** - 加速度、ジャイロ、磁気、センサーフュージョン。
- **USB-C インターフェース** - USB 2.0 Type-C レセプタクル。
- **ローカルフットプリント同梱** - BNO085 と Molex コネクタ用ライブラリ。
- **製造出力設定** - 再現性のある製造ファイル出力用設定。

## 内容

```text
esp32_bno085.kicad_pro
esp32_bno085.kicad_sch
esp32_bno085.kicad_pcb
fp-lib-table
BNO085.pretty/
530480210.pretty/
fabrication-toolkit-options.json
```

## プロジェクトを開く

```powershell
git clone https://github.com/nemonamo/esp32_bno085.git
cd esp32_bno085
```

KiCad 8 以降で `esp32_bno085.kicad_pro` を開き、ローカルフットプリントが解決できることを確認してから、製造ファイル出力前に ERC と DRC を実行してください。

## 製造チェック

- KiCad ERC と DRC を実行する。
- Gerber、ドリル、BOM、CPL を再出力する。
- USB D+/D- のクリアランスとコネクタ向きを確認する。
- BNO085 I2C プルアップと電源レールを確認する。
- 製造業者の設計ルールを確認する。

## 安全性

生成アーカイブ、注文ファイル、サプライヤー出力、スクリーンショット、ローカルメモは、レビュー前に Git に含めないでください。

## ライセンス

現在、オープンソースハードウェアまたはソフトウェアライセンスは宣言されていません。再利用、製造、外部貢献を受ける前に `LICENSE` ファイルを追加してください。
