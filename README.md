# Han Su Chang

Robotics, ROS2, Python, C++ 기반으로 실제 장비와 소프트웨어를 연결하는 프로젝트를 만들고 있습니다.  
센서 데이터 처리, 자율주행 로봇 제어, 컴퓨터 비전, GUI 연동처럼 하드웨어와 사용자가 만나는 지점을 중심으로 학습하고 구현합니다.

<p>
  <a href="mailto:hsc0724321@gmail.com">
    <img src="https://img.shields.io/badge/Email-hsc0724321%40gmail.com%20or%20hsc07240%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" />
  </a>
  <a href="https://github.com/HanSuChang">
    <img src="https://img.shields.io/badge/GitHub-HanSuChang-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" />
  </a>
</p>

## Tech Stack

### Robotics & Embedded

![ROS2](https://img.shields.io/badge/ROS2-Humble-22314E?style=flat-square&logo=ros&logoColor=white)
![TurtleBot3](https://img.shields.io/badge/TurtleBot3-Robotis-0A66C2?style=flat-square)
![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-A22846?style=flat-square&logo=raspberrypi&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-00979D?style=flat-square&logo=arduino&logoColor=white)
![ESP32](https://img.shields.io/badge/ESP32-MCU-333333?style=flat-square)
![LiDAR](https://img.shields.io/badge/LiDAR-LDS--02-444444?style=flat-square)
![Nav2](https://img.shields.io/badge/Nav2-Navigation-2C7BE5?style=flat-square)

### AI & Computer Vision

![YOLOv8](https://img.shields.io/badge/YOLOv8-Pose-00C7B7?style=flat-square)
![Ultralytics](https://img.shields.io/badge/Ultralytics-111111?style=flat-square)
![BoT-SORT](https://img.shields.io/badge/BoT--SORT-Tracking-6E40C9?style=flat-square)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![soynlp](https://img.shields.io/badge/soynlp-Korean%20NLP-2D9CDB?style=flat-square)

### Languages & Frameworks

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![PyQt5](https://img.shields.io/badge/PyQt5-41CD52?style=flat-square&logo=qt&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native-61DAFB?style=flat-square&logo=react&logoColor=111111)
![Expo](https://img.shields.io/badge/Expo-000020?style=flat-square&logo=expo&logoColor=white)

### Tools

![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![WSL2](https://img.shields.io/badge/WSL2-Windows-0078D4?style=flat-square)
![RViz](https://img.shields.io/badge/RViz-Visualization-555555?style=flat-square)
![Gazebo](https://img.shields.io/badge/Gazebo-Simulation-7A7A7A?style=flat-square)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)

---

## Featured Projects

### 1. Smart Car ROS2 Project - `smart_car_ws`

ROS2 Humble 기반 스마트 카트 시스템입니다. TurtleBot3, Raspberry Pi 4, Ubuntu PC, ESP32 팬틸트 서보, LiDAR, YOLOv8 Pose, Flask 장바구니 UI를 하나의 워크스페이스에서 연동했습니다.

**구성 패키지**

| Package | Language | 주요 역할 |
| --- | --- | --- |
| `smart_car_cpp_pkg` | C++17 | 사람 추종 주행, LiDAR 기반 장애물 회피, Kalman 필터, Nav2 `NavigateToPose` 액션 클라이언트 |
| `smart_car_py_pkg` | Python 3 | YOLOv8 Pose 추적, 팬틸트 제어, 상품 인식, Flask 장바구니, ESP32 UDP 브리지 |

**핵심 기능**

사람 추종은 `pan_tilt_ros2.py`에서 카메라 프레임을 받아 YOLOv8 Pose와 BoT-SORT로 사람을 추적하고, 50초간 Master Learning을 거쳐 추종 대상의 HSV 히스토그램을 학습합니다. 학습 이후에는 히스토그램 Re-ID로 같은 사람을 구분하며, 상체/무릎/발목 keypoint visibility 조합으로 장애물 의심 상황을 판단합니다.

`person_follower.cpp`는 `/person_detection`, `/pan_tilt/pan_angle`, `/scan`을 결합해 `/cmd_vel`을 생성합니다. 상태 머신은 `PERSON_FOLLOW -> AVOID_TURN -> AVOID_FORWARD -> PERSON_FOLLOW` 흐름이며, 추종 거리, 회피 트리거 거리, 전방 안전거리, 회전 속도 등은 `person_follower.yaml`에서 관리하고 실행 중 파라미터 업데이트가 가능하도록 구성했습니다.

상품 인식은 `ros2_cart_bridge.py`가 YOLO로 선크림, 테이프, 가위, 물티슈 클래스를 검출해 클래스별 cooldown을 적용한 뒤 Flask `/api/add_item`을 호출합니다. `cart_gui.py`의 `CartManager`는 상품명, 가격, 이미지, 수량을 관리하고 QR 결제 페이지, 영수증, 수량 증감, 결제 완료 화면을 제공합니다.

**사람 추종 + 장애물 회피 데이터 흐름**

```text
[PC] /webcam2/image_raw/compressed
  -> pan_tilt_ros2.py
     - YOLOv8 Pose inference
     - BoT-SORT tracking
     - 50s Master Learning + HSV Re-ID
     - upper/knee/ankle keypoint visibility
     - /person_detection, /pan_tilt/pan_angle
     - /servo_pan_cmd, /servo_tilt_cmd

[Pi4] /person_detection + /pan_tilt/pan_angle + /scan
  -> person_follower.cpp
     - PERSON_FOLLOW: pan_angle 정렬 + LiDAR 거리 기반 전진
     - AVOID_TURN: 발목 미검출 + 전방 근접 -> 넓은 쪽 회전
     - AVOID_FORWARD: 전방/대각선 공간 확보 시 저속 전진
     - 복귀: pose 회복 + 안전거리 확보 시 PERSON_FOLLOW
     - /cmd_vel, /obstacle_avoidance_trigger

[ESP32] /servo_pan_cmd, /servo_tilt_cmd
  -> UDP 8889 -> 팬틸트 서보 PWM
```

**상품 인식 + Flask 장바구니 흐름**

```text
/webcam/image_raw/compressed
  -> ros2_cart_bridge.py
     - YOLO 상품 인식
     - class_name 정규화 + cooldown
     - POST http://<gui_host>:5000/api/add_item

cart_gui.py
  - 선크림 12,000원 / 테이프 1,000원 / 가위 1,000원 / 물티슈 2,000원
  - 중복 인식 시 자동 수량 증가 차단
  - 수동 수량 조절
  - QR 결제 페이지 + 영수증 + 결제 완료 화면
```

**실행 구조**

```text
[Ubuntu PC]
  - pan_tilt_ros2.py
  - yolo_detect_ros2.py
  - ros2_cart_bridge.py
  - cart_gui.py

[TurtleBot3 + Raspberry Pi 4]
  - person_follower.cpp
  - go_to_pose.cpp
  - servo_udp_bridge.py
  - scan_summary_monitor.py
  - TurtleBot3 /scan, /cmd_vel 연동
```

---

### 2. BootCamp Project 1 - Arduino Based ADAS

Arduino Uno + ESP32 + PyQt5를 묶은 RC카 기반 ADAS 주행 보조 시스템입니다. 모바일 RoboRemoDemo 앱에서 ESP32로 명령을 보내면, ESP32가 UART로 Arduino Uno 모터 컨트롤러에 명령을 전달하고 WiFi UDP로 PyQt5 GUI에 센서 데이터를 스트리밍합니다.

**통신 토폴로지**

```text
[Mobile App: RoboRemoDemo]
  -> Bluetooth Classic
     -> [ESP32]
        -> UART Serial2 -> [Arduino Uno + L293D Shield] -> 4ch DC Motor
        -> Ultrasonic x5 / Photoresistor / RGB LED / Buzzer / TM1637 FND
        -> WiFi UDP :5005 -> [PyQt5 Cockpit GUI]
```

**핵심 기능**

- ESP32 Bluetooth Classic 기반 모바일 명령 수신
- 초음파 센서 5개, 조도 센서, RGB LED, 부저, TM1637 FND 제어
- Arduino Uno + L293D 모터 쉴드 기반 4륜 DC 모터 제어
- 수동 주행: 가속, 감속, 브레이크, 좌우 조향, 기어 처리
- 자동 주행: 전방 장애물 감지, 벽 추종, 탱크턴 기반 회피
- PyQt5 계기판: 속도, 기어, 배터리, 방향지시등, AUTO/MANUAL 상태 표시

---

### 3. Hospital Chatbot Project - 건강이

고령층을 위한 병원 추천 챗봇입니다. 사용자가 자연어로 증상과 지역을 입력하면 한국어 NLP로 증상을 정규화하고, 공공 병원 데이터와 진료과 매칭을 거쳐 인근 병원을 추천합니다.

**프로젝트 개요**

| 항목 | 내용 |
| --- | --- |
| 기간 | 2025.05.20 ~ 2025.06.30 |
| 참여기관 | 동구노인종합복지관 |
| 역할 | 팀장 / Frontend Lead |
| 담당 | 프로젝트 총괄, 챗봇 흐름 설계, API 인터페이스 정의, 프론트엔드-백엔드 연동 |

**아키텍처**

```text
[React Native + Expo App]
  -> POST /recommend { message, location }
     -> [FastAPI Backend]
        - soynlp LTokenizer 토큰화
        - synonym_normalized.csv: 증상 유사어 -> 표준 증상
        - disease_name.csv: 증상 -> 추천 진료과
        - hospital_data.csv: 영업중 병원 + 진료과 + 주소
```

**핵심 기능**

백엔드는 FastAPI, pandas, soynlp를 사용해 입력 문장을 토큰화하고 유사어를 표준 증상명으로 매핑합니다. 이후 증상-진료과 매핑 테이블과 병원 데이터를 결합해 지역 기반 병원을 추천합니다.

프론트엔드는 React Native + Expo 기반이며, `home.tsx`와 `chat.tsx`로 홈/채팅 화면을 구성했습니다. 챗봇 응답은 TTS로 읽어주고, 다크/라이트 모드와 큰 글씨 UI를 적용해 고령층 사용성을 높였습니다.

---

## Repository Highlights

| Repository | Description |
| --- | --- |
| [Mignonbrothers/smart_car_ws](https://github.com/Mignonbrothers/smart_car_ws) | TurtleBot3 + YOLOv8 Pose + LiDAR 기반 스마트 카트 |
| [Daejeon-2025-Weather-Data-Analysis](https://github.com/HanSuChang/Daejeon-2025-Weather-Data-Analysis) | 대전 지역 2025년 날씨 데이터 분석 |
| [pygame-SPACE-DASH-GAME](https://github.com/HanSuChang/pygame-SPACE-DASH-GAME) | Python Pygame 기반 우주 회피 게임 |
| [Mignonbrothers/BootCamp_Project1](https://github.com/Mignonbrothers/BootCamp_Project1) | Arduino + ESP32 + PyQt5 RC카 ADAS |
| [yeojin75/hospital_chatbot_project-](https://github.com/yeojin75/hospital_chatbot_project-) | FastAPI + React Native 병원 추천 챗봇 |

---

## What I Focus On

- 실제 장비에서 동작하는 ROS2 노드 설계
- 센서 데이터와 제어 로직을 연결하는 시스템 구성
- Python/C++을 함께 사용하는 분산 로봇 소프트웨어 개발
- 컴퓨터 비전 기반 인식 기능 구현
- 사용자가 조작하기 쉬운 GUI와 로봇 상태 시각화

## Development Environment

- **로봇**: TurtleBot3 / Raspberry Pi 4 / Arduino Uno / ESP32
- **OS**: Ubuntu 22.04 / Windows 11 + WSL2
- **ROS2**: Humble Hawksbill
- **워크플로**: WSL2 개발 -> GitHub -> 실제 Ubuntu PC / TurtleBot3 배포
- **튜닝**: `ros2 param set`, `rqt_reconfigure` 기반 실시간 파라미터 조정

## GitHub Stats

<p>
  <img src="https://github-readme-stats.vercel.app/api?username=HanSuChang&show_icons=true&theme=default&hide_border=true" alt="GitHub stats" height="160" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=HanSuChang&layout=compact&hide_border=true" alt="Top languages" height="160" />
</p>

## Contact

- Email: `hsc0724321@gmail.com` or `hsc07240@gmail.com`
- GitHub: [github.com/HanSuChang](https://github.com/HanSuChang)
