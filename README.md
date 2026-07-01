# 빅핑키 캐리어
> 빅핑키, 터틀봇, omx를 사용한 재난 구호 시스템
## 📌 프로젝트 개요
### 수행 기간
> 2026.05.26 ~ 
### 팀원
> |이름|역할|
> |------|------|
> |김권 |터틀봇 자율 주행 시스템 구성|
> |김동석 |터틀봇 주차 시스템 구성, 조난자 인식 모델 개발|
> |명지훈 |omx 동작 및 시스템 구현|
> |박준수 |관제 시스템 구현|
> |이경환 |시퀸스 구현|
> |최민석 |빅핑키 패키지 작성, 터틀봇 하드웨어 구성|
> |최민지 |빅핑키 하드웨어 구성|

### 목표
> - 터틀봇 자동 하차 및 건물 진입
> - 자율 맵핑 및 사람 감지
> - 구호 물품 자율 배달
> - 웹 서버에서 모니터링 및 제어
### 주요 기능
> - 마커 및 라인 트레이싱을 이용한 터틀봇 상하차
> - 프론티어 기반 자율 탐색을 이용한 실시간 지도 작성 및 조난자 인식
> - opencv를 이용하여 구급품 및 물을 omx를 통해 적재
> - FMS(Fleet Management System)을 통한 효율적인 터틀봇 제어 시스템
### 성과
> - 
> - 

## ⚙️ 시스템 아키텍처


## 🎥 시연
### OMX 시스템
<img width=60% alt="omx_blue (1)" src="https://github.com/user-attachments/assets/0a35aa3b-cbc6-4996-bcbc-f2c6eeb8e7ef" />

## 🛠️ 하드웨어
<details>
  <summary>HW</summary> 
  
  ### 터틀봇
> |부품명|역할|
> |------|------|
> |USB 2.0 WebCAM  |요구조자 식별 및 관제|
> |WS2812B 고휘도 LED     |전조등|
> |NMP441 전방향 마이크 모듈       |요구조자와 소통|
> |MAX98357a 앰프 + 스피커     |전달 내용 출력|
> |HAM4311 IR 감지기        |라인트레이싱|
> 
> | 전면 | LED ON | 밑면 | 후면 |
> | :---: | :---: | :---: | :---: |
> | <img src="https://github.com/user-attachments/assets/8279ed56-7f75-4aa2-9896-88c7d142da28" style="width: 100%; aspect-ratio: 4 / 3; object-fit: cover;" /> | <img src="https://github.com/user-attachments/assets/2eb6d84f-9545-4a47-b458-8a55d887c2de"  style="width: 100%; aspect-ratio: 4 / 3; object-fit: cover;" /> | <img src="https://github.com/user-attachments/assets/d340808d-7860-496e-8379-8dd7180bad9e" style="width: 100%; aspect-ratio: 4 / 3; object-fit: cover;" /> | <img src="https://github.com/user-attachments/assets/d9eb1bec-2dbe-407b-98ab-ec936ba67c39" style="width: 100%; aspect-ratio: 4 / 3; object-fit: cover;" /> |



  ### 빅핑키
> |부품명|역할|
> |------|------|
> |USB 2.0 WebCAM  |주행용 카메라, 주차용 내부 카메라|
> |Intel RealSense D435i    |매니퓰레이터 추론용 카메라|
> |DYNAMIXEL 모터       |상하차용 경사로 제어 모터|
> |OMX Manipulator     |구호품 적재용 매니퓰레이터|
> 
> | 전면 | 후면 |
> | :---: | :---: |
> | <img src="https://github.com/user-attachments/assets/053ffab6-c253-45be-853d-6aa55a905c40" style="width: 40%; aspect-ratio: 4 / 3; object-fit: cover;" /> | <img src="https://github.com/user-attachments/assets/23c33340-deb2-4478-bbb7-118865ef61cc"  style="width: 40%; aspect-ratio: 4 / 3; object-fit: cover;" /> |

</details>

## 🛠️ 소프트웨어
<details>
  <summary>SW</summary> 
  
### 경사로 기능 구현
#### 1️⃣Dynamixel SDK 드라이버 구현
> - 모터 초기화, 구동 부하값 읽기 <br/>
> - SDK에서 필요한 기능만 추가 구현 <br/>

#### 2️⃣경사로 제어 액션 서버
> - 경사로 개폐 및 자동 정지 기능 <br/>
> - 모터의 부하값을 기반으로 조기 중지하여 장애물 위에 경사로 정지 <br/>
> - 수행 결과 토픽은 멀티 스레드로 발행 <br/>

### 마커 기반 자율 줒차
#### 1️⃣외부 웹캠 ArUco 마커 기반 후진 도킹
> - P 제어 기반 정밀 후진 도킹
> - 게이트 추적
> - 헤딩 정렬
> - 후진 도킹
> - 완료

#### 2️⃣주차 시퀀스
> - 마커 인식
> - 액션 명령 수신
> - 터틀봇 인식 대기
> - 명령에 따른 주차 위치 이동 명

### Autonomous SLAM
#### 1️⃣프론티어 탐지 기반 자율 탐사
> - 가장 가까운 미탐색 경계로 목표 자동 생성 <br/>
> - slam_toolbox로 실시간 지도 작성 <br/>
> - Nav2로 경로 계획, 주행 <br/>
> - State Machine 기반 미션 관제 <br/>

### 조난자 인식 YOLO 모델
#### 1️⃣파이프라인
> - ONNX 탐지
> - 사람 별 ID 매칭
> - 미동 판정
> - 동작 실행 
#### 2️⃣ONNX 탐지
> - 입력 320x320
> - conf 0.35 이상
> - NMS 필터링
#### 3️⃣탐지 박스 상태
> - Moving
> - Still
> - Unconscious : 객체가 움직이지 않는 시간 5초 이상








</details>

## 🚨 트러블슈팅


