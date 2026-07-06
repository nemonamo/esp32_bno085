<h1 align="center">ESP32 BNO085</h1>

<p align="center">
  <strong>9축 모션 센싱을 위한 ESP32-S3 + BNO085 KiCad 하드웨어 설계.</strong>
</p>

<p align="center">
  <img alt="KiCad" src="https://img.shields.io/badge/KiCad-hardware%20design-314cb0">
  <img alt="MCU" src="https://img.shields.io/badge/MCU-ESP32--S3-orange">
  <img alt="Sensor" src="https://img.shields.io/badge/IMU-BNO085-16a34a">
  <img alt="License" src="https://img.shields.io/badge/license-not%20declared-lightgrey">
</p>

<p align="center">
  <a href="#주요-특징">주요 특징</a> |
  <a href="#저장소-구성">구성</a> |
  <a href="#프로젝트-열기">열기</a> |
  <a href="#제작-체크리스트">제작</a> |
  <a href="#라이선스">라이선스</a>
</p>

<p align="center">
  한국어 |
  <a href="docs/i18n/README.en.md">English</a> |
  <a href="docs/i18n/README.zh-CN.md">中文</a> |
  <a href="docs/i18n/README.ja.md">日本語</a>
</p>

이 저장소는 BNO085 9축 스마트 IMU를 중심으로 한 소형 ESP32-S3 보드의 KiCad 설계 파일을 담고 있습니다. 회로도, PCB 레이아웃, 로컬 풋프린트 라이브러리, fabrication-toolkit 설정은 버전 관리하고, 생성된 Gerber와 분석 결과는 Git에 포함하지 않습니다.

## 주요 특징

- **ESP32-S3 모듈** - Wi-Fi/BLE가 가능한 MCU 모듈 풋프린트.
- **BNO085 스마트 IMU** - 가속도계, 자이로, 자력계, 센서 퓨전용 9축 센서.
- **USB-C 인터페이스** - USB 2.0 Type-C 리셉터클 기반 연결.
- **로컬 풋프린트 포함** - BNO085와 Molex 커넥터 풋프린트를 저장소에 포함.
- **제작 설정 버전 관리** - 반복 가능한 제조 파일 생성을 위한 fabrication-toolkit 설정 포함.

## 저장소 구성

```text
esp32_bno085.kicad_pro          KiCad 프로젝트 파일
esp32_bno085.kicad_sch          회로도
esp32_bno085.kicad_pcb          PCB 레이아웃
fp-lib-table                    로컬 풋프린트 라이브러리 테이블
BNO085.pretty/                  BNO085 풋프린트
530480210.pretty/               Molex 커넥터 풋프린트
fabrication-toolkit-options.json
```

생성 파일은 제외합니다.

```text
analysis/
production/
*-backups/
.history/
*.kicad_prl
```

## 프로젝트 열기

1. KiCad 8 이상을 설치합니다.
2. 저장소를 clone합니다.
3. KiCad에서 `esp32_bno085.kicad_pro`를 엽니다.
4. `fp-lib-table` 기준으로 로컬 풋프린트가 정상 연결되는지 확인합니다.
5. 제조 파일을 내보내기 전에 ERC와 DRC를 실행합니다.

```powershell
git clone https://github.com/nemonamo/esp32_bno085.git
cd esp32_bno085
```

## 제작 체크리스트

PCB 주문 전 확인할 항목:

- `esp32_bno085.kicad_sch`에서 KiCad ERC 실행
- `esp32_bno085.kicad_pcb`에서 KiCad DRC 실행
- 현재 보드 기준으로 Gerber, drill, BOM, CPL 재내보내기
- USB D+/D- clearance와 커넥터 방향 확인
- BNO085 I2C pull-up과 전원 레일 확인
- 제작 업체의 설계 규칙이 현재 PCB 제약과 맞는지 확인

이전 보드 리뷰에서는 JLCPCB 관련 copper geometry, 작은 via, USB D- clearance, silkscreen/text warning, BNO085 environmental I2C pull-up을 중점적으로 확인했습니다. 레이아웃을 바꿀 때마다 검사를 다시 실행하세요.

## 이 저장소가 아닌 것

- 펌웨어는 포함하지 않습니다.
- 생성된 production package는 포함하지 않습니다.
- 최신 커밋이 그대로 제작 검증을 마쳤다고 보장하지 않습니다.

## 보안과 안전

하드웨어 저장소도 제작 압축 파일, 공급업체 export, 주문 파일, 스크린샷, 로컬 메모를 통해 개인 정보나 프로젝트 정보를 노출할 수 있습니다. production export와 분석 보고서는 검토 전까지 로컬에만 보관하세요.

## 라이선스

현재 오픈소스 하드웨어/소프트웨어 라이선스가 선언되어 있지 않습니다. 외부 재사용, 제작, 기여를 받기 전에 `LICENSE` 파일을 추가하세요.
