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
![TF2](https://img.shields.io/badge/TF2-Transform-22314E?style=flat-square)
![AMCL](https://img.shields.io/badge/AMCL-Localization-444444?style=flat-square)
![ArUco](https://img.shields.io/badge/ArUco-Marker-5C3EE8?style=flat-square)

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

### 1. AMR Logistics Robot ROS2 Project - `Topology_Graph_test`

매니퓰레이터를 탑재한 TurtleBot AMR과 저가형 추종 RC카가 협업하는 ROS2 기반 물류 이송 시스템입니다. React GUI, Go Backend, Python ROS2 Bridge, TurtleBot 주행 시스템, RC카, ArUco 마커, 매니퓰레이터를 하나의 ROS2 DDS 네트워크(`ROS_DOMAIN_ID=27`)로 통합했습니다.

**담당 역할** — TurtleBot 자율주행 파트 전반(Topology 미션 주행, 계층형 장애물 회피, ArUco 정밀 접근, 충전 L자 도킹, RC카 추종 초기 구현)과 GUI-주행 시스템 통합(SI)

**담당 노드 구성**

| Node / File | Language | 주요 역할 |
| --- | --- | --- |
| `mission_loop.cpp` / `mission2_loop.cpp` | C++ | A/B 구역 Topology 미션 주행, 회피 연계, ArUco 정밀 접근, 충전 L자 도킹 |
| `local_astar_pure_pursuit.cpp` | C++ | Occupancy Grid + LiDAR 기반 Local A* 경로 생성 및 Pure Pursuit 추종 |
| `topology_follower.cpp` | C++ | `topology.yaml` 노드 경로 기반 기본 주행 제어 |
| `rc_car_follower_node.cpp` | C++ | Leader Pose History 기반 RC카 추종주행 (초기 구현·검증) |
| `aruco_marker_detector_node.cpp` | C++ | ArUco 마커 검출 및 상대 위치/거리 발행 |
| `topology_marker_node.cpp` | C++ | RViz Topology 노드 시각화 |

**핵심 기능**

Topology 미션 주행은 `topology.yaml`로 물류 공간을 노드/엣지로 추상화하고, 선택된 작업 구역(A/B)에 따라 `mission_loop` / `mission2_loop`가 목표 노드를 순차 추종합니다. TF `map->base_footprint`로 현재 Pose를 구하고 거리·방향 오차를 이용해 약 20Hz로 `/cmd_vel`을 생성합니다.

장애물 회피는 계층형 구조로 설계했습니다. 평상시에는 Topology 노드로 직접 주행하다가, LiDAR로 장애물이 감지되면 Occupancy Grid(정적)와 LiDAR(동적)를 결합한 Local Planning Grid에서 8방향 `A*`(`f = g + h + alignment_penalty`, Path Corridor 제한)로 우회 경로를 만들고 Pure Pursuit로 추종합니다. Local 회피가 어려운 경우 Corridor Pass로 통로 통과 가능성을 판단한 뒤 Nav2 `FollowPath` + MPPI Controller 기반 Rescue Path로 2차 회피하고, 안전 조건이 확보되면 제어권을 다시 Local/Topology 주행으로 넘깁니다.

Leader Slot 도착 후에는 Topology 좌표만으로 부족한 수 cm 오차를 ArUco 마커 기반 정밀 접근으로 보정하고, 180° 회전과 7.5cm 후진으로 작업 자세를 맞춘 뒤 `A_mission_start`로 매니퓰레이터 작업을 연계합니다. 충전 미션은 Nav2 `NavigateToPose`로 진입 후 Parking Corner -> 후진 호 -> 직선 후진의 L자형 도킹으로 수행합니다.

**미션 주행 + 계층형 장애물 회피 흐름**

```text
[GUI/Backend] 구역 선택 -> /mission_command -> mission_loop / mission2_loop 실행

mission_loop.cpp (A) / mission2_loop.cpp (B)
  - TF map->base_footprint 기반 현재 Pose 계산
  - topology.yaml 노드 순차 추종 -> /cmd_vel (약 20Hz)
  - LiDAR /scan 목표 방향 장애물 감지 -> StopAndPlan

  -> local_astar_pure_pursuit.cpp (1차 회피)
     - Occupancy Grid(/map) + LiDAR 동적 장애물 = Local Planning Grid
     - 8방향 A* (f = g + h + alignment_penalty, Path Corridor 제한)
     - Pure Pursuit lookahead 추종 -> Topology 복귀

  -> Corridor Pass 판단 -> MPPI Rescue (2차 회피)
     - Nav2 FollowPath + MPPI Controller로 Rescue Path 추종
     - 안전 조건 충족 시 Local / Topology로 제어권 Handoff
```

**ArUco 정밀 접근 + 작업 연계 흐름**

```text
Leader Slot 도착
  -> mission_loop.cpp: /aruco_marker/enable = true
     -> aruco_marker_detector_node.cpp
        - 카메라 마커 검출 -> /aruco_marker/target (횡오차, 거리)
     - target 기반 저속 정밀 접근 -> 정지거리 도달 정지
     - 터틀봇 180° 제자리 회전 + 7.5cm 후진
     - A_mission_start -> 매니퓰레이터 작업 시작
     - 작업 위치 Zero Twist 정지 유지
```

**RC카 추종 + GUI-주행 통합(SI) 흐름**

```text
mission_loop.cpp
  - /turtlebot/pose 발행 (Leader Pose)
  - /rc_car/follower_mode (follow / stop / turn_ccw_90 ...)

rc_car_follower_node.cpp   (ROS_DOMAIN_ID=27 도메인 통합)
  - Leader Pose History 저장 -> 약 0.70m 뒤 Follow Target 선택
  - /rc_car/odom, /rc_car/slot_wait_status 발행
  ※ RC카 거리·속도·PWM 튜닝은 팀원 담당

[React GUI] 구역/충전 선택 -> [Go Backend] Mission Runner 프로세스 실행
  -> [Python ROS2 Bridge] /mission_command, /initialpose 전달 -> 주행 시스템
  <- 상태 피드백: TF / /odom / /scan -> Bridge -> Backend -> WebSocket -> GUI
  ※ GUI / Backend / Bridge 개발은 팀원, 주행 로직 연동(SI)은 본인 담당
```

**Tech Stack** — ROS2 Humble · C++ · Nav2 (FollowPath / NavigateToPose / MPPI) · TF2 · LiDAR · AMCL · ArUco · DDS

---

### 2. Smart Car ROS2 Project - `smart_car_ws`

ROS2 Humble 기반 스마트 카트 시스템입니다. TurtleBot3, Raspberry Pi 4, Ubuntu PC, ESP32 팬틸트 서보, LiDAR, YOLOv8 Pose, Flask 장바구니 UI를 하나의 워크스페이스에서 연동한 팀 프로젝트입니다.

**담당 역할** — 팬틸트 서보 제어와 C++ 추종 주행(`person_follower.cpp`)·LiDAR 장애물 회피·Nav2 `NavigateToPose` 목적지 이동을 개발하고, 팀원이 구현한 YOLOv8 Pose·BoT-SORT 인식·추적 알고리즘을 가져와 서보 제어·주행 로직과 융합해 하나의 추종 주행 시스템으로 통합

**구성 패키지**

| Package | Language | 담당 | 주요 역할 |
| --- | --- | --- | --- |
| `smart_car_cpp_pkg` | C++17 | 본인 | 추적 대상 추종 주행, LiDAR 장애물 회피, Nav2 `NavigateToPose` 목적지 이동 |
| `smart_car_py_pkg` | Python 3 | 팀원 · 본인 | YOLOv8 Pose·BoT-SORT 추적·상품 인식·Flask 장바구니(팀원) / 팬틸트 서보 제어(본인) |

**팬틸트 서보 제어 (담당)**

팀원이 개발한 인식·추적 노드가 BoT-SORT로 대상 객체를 추적하면, 본인은 그 대상의 화면 내 위치를 받아 팬틸트 서보를 제어합니다. 대상 중심과 화면 중심의 오차를 계산하고 Dead Zone으로 미세 흔들림을 제거한 뒤, 오차에 비례해 Pan 각도를 보정하고 smoothing으로 급격한 움직임을 완화합니다. 0~180°를 500~2500μs로 변환해 `/servo_pan_cmd`로 서보를 구동하고, 현재 Pan 각도를 `/pan_tilt/pan_angle`로 발행해 카메라가 대상을 화면 중앙에 유지하면서 주행 로직에 방향 정보를 제공합니다.

**추종 주행 및 장애물 회피 (담당)**

`person_follower.cpp`는 `/pan_tilt/pan_angle`, `/person_detection`, LiDAR `/scan`을 결합해 `/cmd_vel`을 생성하여 대상 객체를 따라 주행합니다. Pan 각도로 대상 방향을 향해 본체를 정렬(P 제어, `angular.z`)하고 Pan 방향의 LiDAR 거리로 선속도 단계를 제어하며 10Hz로 동작합니다. 상태 머신은 `PERSON_FOLLOW -> AVOID_TURN -> AVOID_FORWARD -> PERSON_FOLLOW` 흐름이며, 전방 ±45° 최소거리 0.40m에서 회피를 트리거하고 좌우 평균 공간을 비교해 넓은 방향으로 회전, 목표 0.65m Wall Following(P 제어) 후 Pan 각도가 정렬되면 추종으로 복귀합니다. 파라미터는 `person_follower.yaml`에서 실행 중 조정할 수 있으며, `go_to_pose.cpp`로 GUI 목적지를 Nav2 `NavigateToPose` 액션으로 자율주행합니다.

**추적 융합 + 추종 주행 데이터 흐름**

```text
[PC · 팀원] YOLOv8 Pose + BoT-SORT
  - 대상 객체 추적 -> 대상 화면 위치 / 검출 정보 제공

[PC · 본인] 팬틸트 서보 제어
  - 대상 화면 위치 오차 -> Dead Zone -> 비례 보정 -> smoothing
  - 0~180° -> 500~2500μs -> /servo_pan_cmd (카메라가 대상 추종)
  - /pan_tilt/pan_angle 발행

[Pi4 · 본인] person_follower.cpp
  - 입력: /pan_tilt/pan_angle + /person_detection + /scan
  - PERSON_FOLLOW : pan 각도 정렬 + LiDAR 거리 기반 전진 (대상 추종)
  - AVOID_TURN    : 전방 0.40m 근접 -> 좌우 넓은 쪽 회전
  - AVOID_FORWARD : 측면 0.65m Wall Following
  - 복귀          : pan 각도 정렬 시 PERSON_FOLLOW
  - 출력: /cmd_vel

[본인] go_to_pose.cpp -> Nav2 NavigateToPose 목적지 이동
```

> 대상 인식·추적 알고리즘(YOLOv8 Pose·BoT-SORT), 상품 인식, Flask 장바구니 UI는 팀원이 개발했으며, 본인은 그 인식 결과를 팬틸트 서보 제어 및 추종 주행과 융합해 통합했습니다.

---

### 3. BootCamp Project 1 - Arduino Based ADAS

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

### 4. Hospital Chatbot Project - 건강이

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
| [HanSuChang/Topology_Graph_test](https://github.com/HanSuChang/Topology_Graph_test) | 매니퓰레이터 탑재 TurtleBot AMR + 추종 RC카 물류 이송 시스템 |
| [Mignonbrothers/smart_car_ws](https://github.com/Mignonbrothers/smart_car_ws) | TurtleBot3 + YOLOv8 Pose + LiDAR 기반 스마트 카트 |
| [Daejeon-2025-Weather-Data-Analysis](https://github.com/HanSuChang/Daejeon-2025-Weather-Data-Analysis) | 대전 지역 2025년 날씨 데이터 분석 |
| [pygame-SPACE-DASH-GAME](https://github.com/HanSuChang/pygame-SPACE-DASH-GAME) | Python Pygame 기반 우주 회피 게임 |
| [Mignonbrothers/BootCamp_Project1](https://github.com/Mignonbrothers/BootCamp_Project1) | Arduino + ESP32 + PyQt5 RC카 ADAS |
| [yeojin75/hospital_chatbot_project-](https://github.com/yeojin75/hospital_chatbot_project-) | FastAPI + React Native 병원 추천 챗봇 |

---

## What I Focus On

- 실제 장비에서 동작하는 ROS2 노드 설계
- Topology 기반 미션 주행과 계층형(Local A* / MPPI) 장애물 회피 설계
- 인식 결과를 서보·주행 제어와 융합하는 시스템 통합
- Python/C++을 함께 사용하는 분산 로봇 소프트웨어 개발
- 센서 데이터와 제어 로직을 연결하는 시스템 구성
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
