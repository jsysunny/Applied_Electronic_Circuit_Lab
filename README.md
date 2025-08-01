# Applied_Electronic_Circuit_Lab (2022.05~2022.06)

&nbsp;

## 🧠 재활완료 판정기

&nbsp;

## 📑 목차

1. [📌 프로젝트 개요](#1--프로젝트-개요)  
2. [🔧 구성 요소](#2--구성-요소)  
3. [💻 사용 기술](#3--사용-기술)  
4. [🧭 동작 흐름 요약](#4--동작-흐름-요약)   

   
&nbsp;
## 📌 프로젝트 개요

본 프로젝트는 팔 또는 다리 등 근육에 심각한 손상을 입어 수축이 불가능한 환자에게  
**재활 여부를 판단하거나, 생체신호 기반의 반응을 인지하여 출력 반응을 유도**하는 시스템을 설계하는 것을 목표로 한다.

근전도(EMG) 신호를 통해 근육의 수축 유무 및 정도를 실시간으로 측정하고,  
해당 신호가 특정 기준 이상일 경우 음향 출력을 통해 반응을 제공한다.
 
&nbsp;

### 🎯 기획 의도

- 근육 기능이 저하된 환자의 상태를 판단하고, 일정 회복 수준 도달 여부를 직관적으로 전달
- 비침습적인 근전도 측정을 통해 재활 가능성을 평가하고, 훈련 동기를 제공
- 생체신호 기반의 인터페이스를 활용하여 의사소통 또는 반응 보조 장치로도 활용 가능
  
&nbsp;

### 🏭 기존 기술의 활용과 확장 가능성

- 표면 근전도 측정 기술을 활용하여 피부 위에 전극을 부착하고 전기적 신호를 분석
- EMG 신호를 증폭 회로(Amplifier)를 통해 5V 이상으로 증폭 시, 피드백 음성 출력 구현
- 인체의 공명 주파수(Resonance Frequency)를 고려한 신호 해석으로 정확한 판단 기반 확보

&nbsp;

### ✅ 확장 가능성

- **재활 치료 평가 시스템**: 정량적 근육 회복 측정 지표 제공
- **근육 반응 기반 알림 시스템**: 특정 조건에서 알람, 소리 등 외부 장치 연동
- **뇌-근육-기계 인터페이스 연구의 기초 자료**로 활용 가능
- 고령자나 환자의 **자가 운동 추적 및 피드백 장치**로 확장 가능



&nbsp;
## 2. 🔧 구성 요소

| 구성 요소                           | 설명                                                                                         |
|------------------------------------|----------------------------------------------------------------------------------------------|
| 1N4002 다이오드                    | 정류 및 역전압 보호용 일반 다이오드                                                         |
| 도시바 9V 건전지                   | 회로 전원 공급용 전원 소자                                                                  |
| TL082CP 오퍼앰프                   | 저잡음, 듀얼 연산 증폭기. 생체 신호 증폭 회로에 사용                                        |
| Round IC Socket (08P, 14P)         | IC 칩 탈부착을 용이하게 하기 위한 소켓                                                      |
| AT-1750-TFL-LW95-R                 | 생체 신호 증폭 후 조건 만족 시 소리 출력용 스피커                                          |
| EIC-106 회로보드                   | 전체 회로 구성 및 납땜용 기판                                                                |
| 100uF 6.3V 전해콘덴서              | 전원 노이즈 제거 및 신호 안정화용                                                           |
| LM339 비교기                       | 입력 신호와 기준값을 비교하여 디지털 신호로 변환                                           |
| PCB 보드 (Dual Half Size)         | 실험용 회로 구성 시 아두이노/모듈 장착용 브레드보드                                         |
| AD620BNZ 인스트루멘테이션 앰프     | 고정밀 생체 신호 증폭용. 전극 간 미세 전위차 증폭에 사용                                    |


&nbsp;

<img width="1328" height="908" alt="image" src="https://github.com/user-attachments/assets/19d921d6-f596-4d88-84ec-da9a4cb9e17d" />

<img width="1208" height="876" alt="image" src="https://github.com/user-attachments/assets/38f5e0eb-e1c6-4f36-921f-bebbebef0af9" />

<img width="1345" height="284" alt="image" src="https://github.com/user-attachments/assets/dea76b85-a19a-4cce-b183-d5ad14f5ba2d" />


&nbsp;
<img width="821" height="280" alt="image" src="https://github.com/user-attachments/assets/3ebcf197-adfd-4b89-9ded-90b3fcc41b4e" />

<img width="928" height="416" alt="image" src="https://github.com/user-attachments/assets/fb95ef9d-be8b-49e3-a99e-9eb19074e23f" />

## 3. 💻 사용 기술

| 기술                           | 내용                                                                                     |
|--------------------------------|------------------------------------------------------------------------------------------|
| 생체신호 측정                  | 팔/다리 근육에서 발생하는 미세 전기 신호(2-10mV, 20-70Hz)를 계측용 증폭기로 수집          |
| 표면 근전도 (sEMG) 방식       | 피부에 전극 부착 후 EMG 신호 수집 → 비침습적 방식으로 사용자 편의성 확보                 |
| 회로 설계 및 구현 환경        | 브레드보드 및 만능기판 기반 회로 구성, 납땜 및 실험 진행                                 |
| 계측용 증폭기 (IA)            | 입력 신호(Vin+=5mV, Vin-=3mV)를 약 495배 증폭하여 저전력 생체신호 감지에 사용             |
| 아날로그 필터 (LPF, Notch, HPF) | 불필요한 고주파 및 잡음 제거. Notch 필터로 60Hz 정전기 노이즈 제거, HPF로 저역 필터링     |
| 비반전 증폭기 + 정류회로      | 신호를 양전압으로 증폭 및 변환하여 안정적 검출 가능                                     |
| 비교기 (Comparator)           | 기준 전압(5V) 이상일 경우 디지털 출력 발생 → 소리 출력 트리거로 활용                     |
| 오디오 출력                   | 최종 증폭 전압이 5V를 넘으면 스피커에서 사운드 발생 → 재활 완료 알림 기능 구현           |


&nbsp;
## 4. 🧭 동작 흐름 요약
<img width="1272" height="618" alt="image" src="https://github.com/user-attachments/assets/67413147-9c72-4b5e-aa2a-0a3404333f03" />

### 1. 
<img width="1298" height="728" alt="image" src="https://github.com/user-attachments/assets/94a0cd66-6a6a-4011-8f94-2af5497a62a9" />

&nbsp;
<img width="974" height="542" alt="image" src="https://github.com/user-attachments/assets/7ebe4478-26c4-4962-a7fb-cf92bc4c0b89" />

<img width="959" height="520" alt="image" src="https://github.com/user-attachments/assets/1bac0d3a-1099-4c92-8b3f-ea2fb166260f" />

<img width="976" height="541" alt="image" src="https://github.com/user-attachments/assets/e20d48cc-ee51-4f8d-93da-02b5e6c47d1b" />

<img width="973" height="529" alt="image" src="https://github.com/user-attachments/assets/8b066117-bee0-4cfa-a28b-5948131236d5" />

<img width="969" height="536" alt="image" src="https://github.com/user-attachments/assets/ac822dc6-718c-4b77-9925-fa4735282d04" />

<img width="973" height="537" alt="image" src="https://github.com/user-attachments/assets/9f5d0020-122f-42a7-9fae-8a28bf5b8452" />

<img width="963" height="538" alt="image" src="https://github.com/user-attachments/assets/a703129f-0cff-4326-bab5-fbe99d8653c0" />

<img width="959" height="530" alt="image" src="https://github.com/user-attachments/assets/75fbd1b8-df51-4b8f-a8a4-b3e54ca312d9" />

<img width="967" height="531" alt="image" src="https://github.com/user-attachments/assets/3c074618-2319-494d-a13a-5a92f2757473" />

<img width="961" height="527" alt="image" src="https://github.com/user-attachments/assets/da5362d5-1c30-4b07-8b8a-f655f03252b6" />





&nbsp;


