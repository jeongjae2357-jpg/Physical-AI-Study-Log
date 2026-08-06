# Isaac Sim
## Interface
### 개념
- **USD:** Universal Scene Description의 약자로 모양, 질감, 물리엔진, 조명 등 3D 그래픽에 필요한 모든 요소를 담고 있으며 다른 폐쇄적인 3D 그래픽 파일에 대해서 원본을 최대한 훼손하지 않고 변환될 수 있는 파일 형식
- **Scope:** 폴더와 같이 정리를 도와주는 보조 장치
- **Mesh:** 물체
- **PhysicsScene:** 물리 엔진
- **Xform:** 그룹화를 위한 컨테이너
- **Material:** 객체의 겉모습과 물리적 성질을 정의
- **Joint:** 각 객체를 연결하는 관절
    - **Revolute Joint:** 회전의 자유도를 가지는 관절
- **OmniGraph:** 각종 3D 그래픽과 시뮬레이션을 위한 생태계인 Omniverse에서 데이터와 실행 흐름을 시각적인 그래프로 프로그래밍하는 프레임 워크
- **Lidar:** 레이저 빛의 반사를 이용하여 주변 공간을 3차원으로 인식하는 센서 
- **Transform Tree:** ROS2에서 frame들을 tf2라는 트리 형태로 관리함
- **Occupancy Map:** 공간을 격자로 나누어 장애물이 있는 위치, 이동 가능한 영역, 미확인 영역을 기록한 지도(로봇이 이동 가능한 구역을 알려주는 역할을 함)
- **Navigation:** 목표 위치를 지정해주면 로봇이 주변 환경과 현재 위치를 고려하여 스스로 이동 경로를 계획하고 움직이는 것

### 조작법
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
|Create 탭 > Sensors > PhysX Lidar or RTX Lidar|Lidar 생성|
|Tools 탭 > Robotics > Occupancy Map|Occupancy Map 창 띄우기|
|Window 탭 > Example |대부분의 예제를 찾을 수 있음|
|1. VS code에서 Isaac Sim VS Code Edition 설치 <br> 2. Window 탭 > Extension > VS CODE INTEGRATION|Isaac Sim에서 VS code 연동| 
|Window 탭 > Extension > JUPYTER NOTEBOOK INTEGRATION|Isaac Sim에서 jupyter notebook 연동| 

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
- PhysX Lidar는 물리엔진을 이용해 연산하기에 편법이라 보면 되고 RTX Lidar는 실제 빛을 최대한 구현해서 작동시킨 센서라 보면 됨
- Occupancy Map 창에서는 지도로 쓰고자 하는 물체를 원하는 시점에서 bound하고 calculation으로 3D 공간을 해당 시점에서 바라본 2D Occupancy Map을 생성해서 이미지로 저장할 수 있음, 이런 절차는 정적인 환경에서 적합하며 이후 동적인 물체가 들어와도 반영되지 않음을 유의
- Navigation의 절차를 완료하기 위해서는 주변 환경에 대한 정보(Occupancy Map), 현재 로봇의 추정 위치, 경로 계획, 로봇 제어 등을 필요로 함
  
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
- **ROS2 Context:** ROS2 네크워크 통로 구분 노드 (isaac sim 입장에서 ROS는 외부 프로세스이기 때문에라도 사용해야 함)
- **Isaac Run One Simulation Frame:** 일정 주기로 오는 신호에 맞춰 다음 프레임으로 진행할 것을 명령하는 신호를 내보내는 노드(동기화 용도로 쓰임)
- **Isaac Create Render Product:** 사용할 카메라 시점과 해상도 지정하고 들어오는 신호에 맞춰 GPU에 렌더링 데이터를 생성할 것을 요청하고 그 생성 데이터의 위치를 출력하는 노드
- **ROS2 Camera Helper:** 렌더링 데이터들을 ROS 메세지 형태로 자동 변환 시켜 발행해주는 노드
- **ROS2 RTX Lidar Helper:** Lidar 데이터들을 ROS 메세지 형태로 자동 변환 시켜 발행해주는 노드
- **Isaac Read Simulation Time:** 시뮬레이션상에서 흐르는 시간을 읽어오는 노드
- **Isaac Read System Time:** 운영체제에서 흐르는 시간을 읽어오는 노드
- **ROS2 Publish Clock:** Clock이라는 topic 타입을 발행하는 노드
- **ROS2 Subscribe Clock:** Clock이라는 topic 타입을 구독하는 노드
- **ROS2 Publish Transform Tree:** parentPrim 좌표계 기준으로 targetPrim의 **위치와 각도**를 계산한 결과를 TFMessage 타입의 형태로 /tf 토픽에 발행하는 노드 (스스로 계산O)
- **ROS2 Publish Raw Transform Tree:** 이미 계산된 Transform Tree 결과를 TFMessage 타입의 형태로 /tf 토픽에 발행하는 노드 (스스로 계산X)
- **Isaac Compute Transform Tree:** parentPrim에는 로봇의 최상위 frame을 넣고, targetPrim에는 로봇의 하위 frame들(로봇 자체를 넣으면 알아서 하위 frame들이 넣어짐)을 넣으면 그 트리구조를 자동 계산해주는 노드
- **ROS2 publish Odometry:** 계산된 로봇의 **선속도와 각속도**를 Odometry이라는 타입의 형태로 /odom 토픽에 발행하는 노드 (스스로 계산X)
- **Isaac Compute Odometry Node:** 로봇의 **선속도와 각속도**를 계산한 결과를 반환하는 노드
- 
### Note
- 노드의 여러 설정은 Property에서 할 수 있음
- 노드의 입력이나 출력 부분에 마우스를 가져다 대면 처리할 수 있는 데이터 타입을 알 수 있음
- 마치 코드에서 변수를 쓰는 것처럼 바로 Property에 직접 입력하는 것보다는 따로 Token 같은 데이터 저장 노드를 만들어 이용하는 것이 관리 측면에서 더 좋음 
- 시간을 다루는 이유는 여러 센서들로부터 오는 데이터들을 동기화해야 하기 때문이다.
- Isaac Compute Transform Tree를 이용하여 ROS2 Publish Transform Tree에 parentPrim과 targetPrim을 제공해주면 기존 단일 관계만 다룰 수 있다는 한계에서 벗어나 여러 frame들의 관계를 다룰 수 있음
- Transform Tree에서 parentPrim과 targetPrim의 관계가 실제 로봇의 tf2 구조의 부모 자식관계와 다르더라도 계산되긴 함, 그러나 실제 로봇 운영에 있어 권장되진 않음

## Python
### Structure
```python

# 기본 구조
class 이름(부모):

    # 자기 자신과 부모 클래스를 생성 및 초기화
    def __init__(self) -> None:
        super().__init__()

    # 초기 Scene을 설정하는 곳
    def setup_scene(self) -> None:

    async def setup_post_load(self) -> None:
        # 시뮬레이선 실행시 한 번 실행되는 명령어들을 적는 곳
```

```python
# 로봇 조작
from isaacsim.core.simulation_manager import SimulationManager

from isaacsim.core.simulation_manager.impl.isaac_events import IsaacEvents

    # 물리엔진 틱마다(IsaacEvents.POST_PHYSICS_STEP) 등록한 함수(self.send_robot_actions)를 실행하도록 구독
    self._physics_callback_id = SimulationManager.register_callback(
        self.send_robot_actions, IsaacEvents.POST_PHYSICS_STEP
    )

    # callback이 호출될 때마다 실행할 로봇의 행동을 정의
    def send_robot_actions(self, dt, context):
```
### Code
- **UsdGeom:** USD에서 기하학과 관련된 처리를 하는 **모듈** (from pxr import UsdGeom)
- **omni:** Isaac Sim에서 Python API를 사용하기 위한 **패키지** (import omni)
- **stage_utils:** USD 스테이지를 직접 조작하는 함수들을 모아 놓은 모듈을 가져옴
- **GeomPrim:** 3D Geometry를 다루는 **클래스**
- **RigidPrim:** 중력, 질량, 속도 등 물리연산을 다루는 **클래스**

|코드|설명|
|--|--|
|import isaacsim.core.experimental.utils.stage as stage_utils|stage_utils를 가져옴|
|from isaacsim.storage.native import get_assets_root_path|엔비디아가 제공하는 3D 로봇, 환경, 오브젝트 파일(USD 파일)들이 저장되어 있는 공식 클라우드 서버의 주소를 반환하는 함수를 가져옴|
|from isaacsim.core.experimental.prims import GeomPrim, RigidPrim| GeomPrim과 RigidPrim 클래스를 가져옴|
|GeomPrim(paths, apply_collision_apis)|paths의 객체에게 형상 정보를 부여, apply_collision_apis로 충돌 여부 결정 가능|
|RigidPrim(paths)|paths의 객체에게 PhysicsScene에서 정한 물리엔진(중력, 힘 등)에 지배를 받게 함|

