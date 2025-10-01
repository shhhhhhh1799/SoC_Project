# ⚙️ SoC Project – AMBA BUS (APB, AXI4-Lite)

본 프로젝트는 **AMBA BUS (APB, AXI4-Lite)** 기반의 **SoC(System on Chip)** 내부 통신 구조를 설계하고,  
**SystemVerilog**를 활용하여 **시뮬레이션 검증**을 수행한 프로젝트입니다.  

CPU – 메모리 – 주변장치(GPIO, LED, FND 등)를 효율적으로 연결하기 위해  
APB와 AXI4-Lite 인터페이스를 구현하고 동작을 검증하였습니다.  

---

## 🧑‍💻 프로젝트 개요

| 항목          | 내용                                                                 |
|---------------|----------------------------------------------------------------------|
| **진행 기간** | 2025.08.27 ~ 2025.09.07                                              |
| **개발 환경** | Vivado, VSCode, Verdi, VCS                                           |
| **언어**      | SystemVerilog                                                        |
| **구조**      | AMBA BUS(APB, AXI4-Lite) 기반 SoC 내부 통신 아키텍처                  |
| **검증 방식** | Testbench 및 시뮬레이션 (GPIO, LED, FND 동작 검증)                    |

---

## 📖 AMBA BUS 개요

- **AMBA (Advanced Microcontroller Bus Architecture)** : ARM에서 제안한 SoC 내부 표준 버스 아키텍처  
- CPU, 메모리, 주변장치를 효율적으로 연결하기 위해 사용  
- 본 프로젝트에서는 **APB**와 **AXI4-Lite** 두 가지 구조를 구현 및 비교  

<p align="center">
  <img src="https://raw.githubusercontent.com/shhhhhhh1799/Image/main/AMBA%20BUS.png" 
       alt="AMBA Bus Overview" width="700"/>
</p>

---

## 📁 주요 모듈 설명

| 모듈      | 설명                                                                 |
|-----------|----------------------------------------------------------------------|
| 🖥 **APB** | 저속 주변장치 제어용 인터페이스. 저전력·저복잡도 구조, GPIO/FND/Timer 등에 적합 |
| ⚡ **AXI4-Lite** | AXI4의 단순화 버전. 단일 Read/Write 지원, 제어 레지스터 접근 최적화         |
| 💡 **GPIO/LED** | 입력/출력 신호 검증, LED 토글/Shift 동작 구현                             |
| 🔢 **FND (7-Segment)** | 0.1초마다 값 증가, 출력 변화 검증                                   |

---

## 🧩 APB 구조

- **특징**  
  - 단순한 구조, 레지스터 접근에 최적화  
  - UART, GPIO, Timer 등 저속 장치 제어에 적합  

- **검증 결과**  
  - GPIO 입력값 → LED Shift 동작 확인  
  - FND_ODR 값이 일정 시간마다 +1 증가하는지 시뮬레이션  

<p align="center">
  <img src="https://raw.githubusercontent.com/shhhhhhh1799/Image/main/APB%20BUS.png" 
       alt="APB Block Diagram" width="800"/>
</p>

---

## 🧩 AXI4-Lite 구조

- **특징**  
  - AXI4의 단순화 버전  
  - Burst 미지원, 단일 Read/Write 지원  
  - FPGA IP 제어나 저속 주변장치 연결에 최적화  

- **검증 결과**  
  - LED : 0.1초마다 반전  
  - FND : 0.1초마다 +1 증가  

<p align="center">
  <img src="https://raw.githubusercontent.com/shhhhhhh1799/Image/main/AXI4_Lite.png" 
       alt="AXI4-Lite Block Diagram" width="800"/>
</p>

---

## 🧪 시뮬레이션 결과

- **APB Testbench** : GPIO 입력에 따른 LED Shift, FND 증가 동작 검증  
- **AXI4-Lite Testbench** : LED 주기적 반전, FND 값 증가 검증  

<p align="center">
  <img src="https://github.com/shhhhhhh1799/Image/blob/main/SoC_Simulation.png" alt="SoC Simulation Result" width="900"/>
</p>

---

## 🔚 마무리 및 고찰

본 프로젝트를 통해 **SoC 내부 통신 표준(AMBA BUS)**을 직접 구현하고,  
APB와 AXI4-Lite의 구조적 차이와 장단점을 비교할 수 있었습니다.  

- **APB** : 단순 구조, 저속 장치 제어에 최적  
- **AXI4-Lite** : IP 제어 및 제어 레지스터 접근에 최적  

추후 발전 방향:  
- **AXI4 Full** 버전으로 확장 (Burst 지원)  
- **DMA, 고속 메모리 연동** 구조 설계  
- **FPGA 보드에서 실제 구현 및 HW 검증**  
