# Isaac Sim
## Interface
### 개념
- **Scope:** 폴더와 같이 정리를 도와주는 보조 장치
- **Mesh:** 물체
- **PhysicsScene:** 물리 엔진
- **Xform:** 그룹화를 위한 컨테이너
- **Material:** 객체의 겉모습과 물리적 성질을 정의
- **Joint:** 각 객체를 연결하는 관절
    - **Revolute Joint:** 회전의 자유도를 가지는 관절
- **OmniGraph:** 각종 3D 그래픽과 시뮬레이션을 위한 생태계인 Omniverse에서 데이터와 실행 흐름을 시각적인 그래프로 프로그래밍하는 프레임 워크

### 객체 조작
|조작법|설명|
|--|--|
|Create 탭> \<원하는 Object>|Object 생성|
|Move(W), Rotate(E), Scale(R)|객체 조작|
|1. Create 탭> Xform <br> 2. <원하는 Object 집어 넣기>|Object 그룹화|
|1. Create 탭> Physics > Physics Scene <br> 2. <물리 엔진 적용하고자 하는 객체> -> Property > Add > Physics > Rigid Body with Colliders Preset|물리 엔진 설정 및 적용|
|Content -> 폴더: Isaac Sim > Robots > \<원하는 로봇의 .usd 파일 끌어 옴 or <br> Create 탭 > Robots > Asset Browser|로봇 로드|
|1. 연결하길 원하는 객첵들 선택 <br> 2. Create 탭 > Physics > Joint > \<원하는 Joint 선택> |관절 연결| 
|1. Create 탭 > Camera <br> 2. Window 탭 > Viewports <br> 3. 새로운 화면의 Perspective -> Camera |카메라 생성 및 카메라 시점으로 보기|
|Window 탭 > Graph Editors > Action Graph |액션 그래프 창 띄우기|
|Tools 탭 > Robotics > OmniGraph Controllers|기본 제공 OmniGraph|
|Window 탭 > Extensions > ROS 2 BRIDGE > ENABLED|ROS2 연결|

### 카메라 조작
|조작법|설명|
|--|--|
|\<마우스 오른쪽 클릭> + \<드래그>|카메라 현 위치 기준으로 회전|
|\<Alt> + \<마우스 왼쪽 클릭> + \<드래그>|카메라 시점 기준으로 회전|
|\<마우스 휠 클릭> + \<드래그>|카메라 평행 이동|
|\<마우스 휠 돌리기> or \<Alt> + \<마우스 오른쪽 클릭> + \<드래그>|줌 인, 줌 아웃|
|\<F>|Object로 카메라 초기화|

### Note
- Issac Sim 6.0.1버전 기준으로 작성되었음
- 각종 실행마다 생기는 오류 메세지 같은 로그들은 Console 창에서 확인 가능 

## Omni Graph
### Action Graph
- 이벤트 트리거에 의한 동작을 관리하는 실행 흐름을 정의하는 그래프 
#### Node
- **Differential Controller:** 두 개의 바퀴가 달린 로봇의 선속도와 각속도를 입력 받아 필요한 바퀴의 회전 속도 계산 결과를 출력
- **Articulation Controller:** 로봇의 관절에 대해 목표 속도, 목표 위치, 힘 등을 입력 받아 실행 명령을 주어 실제 장치를 움직임
- **Constant Token:** Token 형태로 저장하는 노드
- **Make Array:** 배열 만들어주는 노드
- **On Playback Tick:** 매 프레임마다 신호(Tick)을 보내는 노드(Clock 생각하면 됨)
- **Break 3-Vector:** 입력받은 실수값을 3개의 축으로 분해하여 출력하는 노드
- **Scale to/from stage units:** 실제 세상의 거리 단위와 시뮬레이션 상의 거리 단위를 변환해주는 노드
- **ROS2 Subscribe Twist:** Twist라는 topic 타입을 구독하는 노드

### Note
- 노드의 여러 설정은 Property에서 할 수 있음
- 노드의 입력이나 출력 부분에 마우스를 가져다 대면 처리할 수 있는 데이터 타입을 알 수 있음
- 마치 코드에서 변수를 쓰는 것처럼 바로 Property에 직접 입력하는 것보다는 따로 Token 같은 데이터 저장 노드를 만들어 이용하는 것이 관리 측면에서 더 좋음
