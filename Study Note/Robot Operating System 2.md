# Robot Operating System 2
## Concept
- **Node:** 실행 가능한 프로세스의 최소 단위
- **Service:** 클라이언트가 요청하고 서버가 응답하는 방식으로 두 노드가 데이터를 주고 받는 것
- **NameSpace:** 서비스나 토픽, 액션의 적용을 구분하기 위한 경로
- **Topic:** 토픽의 이름과 데이터의 구조를 공유하는 Publisher에서 Subscriber로 비동기적으로 데이터를 전달하는 방식
- **Action:** 클라이언트 노드가 Goal(목표)를 요청하면 목표 수행 중에 계속 토픽을 통해 feedback을 발행하고 일을 완료하면 result를 응답하는 방식

### Concept Note
- NameSpace 덕분에 경로가 유니크 해져서 통신간 얽힘이 없음
- 서비스나 토픽, 액션의 이름은 주소로 데이터 타입은 메시지 형식으로 비유해 볼 수 있음
- 서비스나 액션의 요청과 응답의 과정은 메시지 전달을 통해 이루어짐 (요청을 메시지로 보내고 응답을 행동자체로 받는 구조가 아님)

## Command
|명령어|설명|
|--|--|
|source /opt/ros/<버전>/setup.bash|환경변수 설정|
|rqt_graph|현 통신 상태를 도식으로 표현|
|ros2 run \<PKG Name> \<Node Name>|패키지의 노드를 실행 #\<Node Name>은 임의로 정하는 것이 아닌 executable 파일 임|
|ros2 node list|실행 중인 노드 목록|
|ros2 node info <노드 이름>|노드의 정보를 조회|
|ros2 service list|현재 제공되고 있는 서비스 목록|
|ros2 service type <서비스 이름>|해당 서비스가 사용하는 정의|
|ros2 interface show <인터페이스 이름>|해당 서비스, 토픽이나 액션의 내용 확인|
|ros2 service call \<service name> \<service definition> "data" |서비스 요청|
|ros2 topic list|현재 존재하는 토픽 목록|
|ros2 topic type <토픽 이름>|해당 토픽의 데이터 타입|
|ros2 topic info <토픽 이름>|해당 토픽의 데이터 타입과 publish, subscribe 상황 정보|
|ros2 topic pub --(once or rate <hz>) \<topic_name> \<msg_type> "\<args>"|topic을 publish|
|ros2 topic echo <토픽 이름>|topic을 subscribe|
|ros2 action list|액션 목록을 조회|
|ros2 action send_goal \<action_name> \<action_type> "values"|액션의 목표를 지정|
|ros2 param list| 파라미터 목록을 조회|
|ros2 param get <노드 이름> <파라미터 이름>|파라미터의 값 확인|
|ros2 param set <노드 이름> <파라미터 이름>|파라미터의 값 설정|
|ros2 param dump <노드 이름> > <파일 이름.yaml>|노드의 파라미터들을 저장|
|ros2 param load <노드 이름> > <경로/파일 이름.yaml>|노드의 파라미터들을 적용|

### Command Note
- ROS를 실행하기 위해서는 'sudo apt install' 명령으로 설치한 패키지 환경을 /opt/ros/<버전>/ 경로에 setup.bash파일로 읽어와야 함
- .bashrc파일은 bash의 각종 설정을 저장한다.
- .bashrc에 source /opt/ros/버전/setup.bash를 넣고 source ~/.bashrc로 간소화할 수 있다.
- alias를 통해 더 간소화할 수 있다.
- 서비스의 정의는 srv 확장명을 가진 파일에 저장된다.
- srv 파일은 ---를 기준으로 윗부분은 서비스 요청할 때의 데이터를 선언, 아랫부분은 서비스를 응답할 때의 데이터를 선언한다.
- 서비스 요청의 "data"는 srv에 정의된 형식에 따라 작성하면 된다.
- ros2 service call \reset std_srvs/srv/Empty로 초기화 가능
- topic이나 service의 이름과 타입의 경로가 다르게 보임 -> 이름은 변수와 비슷한 개념, 타입은 어떤 패키지의 어느 메세지 타입인지를 보임
- action의 내용은 ---를 기준으로 윗부분은 goal, 중간은 result, 마지막은 feedback을 의미함
- ROS의 노드, 서비스, 토픽, 액션 이름 모두 경로처럼 생김

## Python
|코드|설명|
|--|--|
|import rclpy as rp|ROS Client Library for Python 모듈을  임포트|
|rp.init()|rclpy 초기화|
|rp.create_node('노드 이름')|해당 이름을 가진 노드를 생성하여 반환
|def callback(data):|구독 노드가 일정 주기로 발행되는 토픽을 받을 때마다 실행되는 함수를 정의|
|(node).create_subscription(<data_type>, '<topic_name>', \<callback>, \<QoS History>)|노드가 해당 토픽에 구독하게 하는 메소드|
|rp.spin(<노드>) {rp.spin_once(<노드>)}|구독한 토픽에서 발행되는 메세지를 받으면 등록된 callback 함수를 {한번만} 실행|
|pub = (node).create_publisher(<data_type>, '<topic_name>', \<QoS History>|노드가 발행하게 하는 메소드|
|msg = <data_type>(), pub.publish(msg)|해당 메세지를 발행|
|(node).create_timer(timer_period, timer_callback)|주기마다 callback 함수를 실행 > callback 함수 안에 토픽 발행을 구현하여 주기마다 발행하는 기능 구현 가능|
|cli = (node).create_client(<data_type>, '<service_name>')|해당 노드가 클라이언트 노드가 되게 하는 메소드|
|cli.call_async(<data_type>.Request())|클라이언트 노드가 요청을 보내게 함|
|cli.wait_for_service(timeout_sec)|파라미터로 설정한 시간 주기로 서비스가 실행되지 않았다면 False를 반환|
|ActionServer(self, <data_type>, '<action_name>', callback)|해당 데이터 타입의 액션 서버를 생성하고 객체를 반환|
|MultiThreadedExecutor()|멀티스레드 기능을 제공하는 객체를 반환|
|(node).declare_parameter('<파라미터 이름>', 초기치)|Node 클래스에서 제공하는 파라미터 생성 메소드|
|(node).get_parameters(['<파라미터 이름>', '<파라미터 이름>', ...])|Node 클래스에서 제공하는 파라미터들을 리스트로 받아 리스트형태로 파라미터 객체를 반환|
|(node).add_on_set_parameters_callback(<callback>)|파라미터 변경 전 콜백 함수를 먼저 실행 시키는 메소드|

### Python Note
- pub.publish(<data_type>())을 바로 했을 때는 초기화된 값이 들어가기 때문에 msg라는 변수로 지정해준 뒤 넣는다.
- 각 클래스들은 rclpy를 임포트해야 사용할 수 있음

## Package
|명령어|설명|
|--|--|
|ros2 pkg create --build-type ament_python <package_name>|패키지 생성 명령|
|ros2 pkg create --build-type ament_cmake <package_name>|CMakeList.txt라는 파일을 포함하면서 새로운 메시지만 정의는 패키지 생성 명령|

### Package Structure
```text
WorkSpace/
├─ build/
├─ install/
├─ log/
└─ src/
    └─ package/
          ├─ package/
          │     ├─ __init__.py
          │     └─ source code.py
          ├─ resource/
          │     └─ package
          ├─ test/
          ├─ package.xml
          ├─ setup.py
          ├─ setup.cfg
          └─ README.md
```
|파일|설명|
|--|--|
|pacakge(안쪽)|실제 python 코드가 들어감|
|\_\_init__.py|해당 파일이 python 패키지로 인식하게 만듦|
|resource/package|ament index가 패키지를 찾게함|
|test/|테스트 코드나 코드 검사 파일이 들어감|
|package.xml|패키지의 메타데이터를 담음(<depend>에 해당 패키지 빌드에 필요한 코드를 담음)|
|setup.py|해당 패키지를 설치하는 법이 담김(entry_points에서 사용할 소스코드를 적음)|
|setup.cfg|setup.py의 일부 설정을 분리|
|README.md|패키지 설명 문서|

### Package Note
- workspace를 빌드하는 colcon builds는 해당 폴더로 가서 사용해야 함(workspace는 여러 개 존재할 수 있기 때문)
- workspace를 빌드하고 나면 install 폴더의 local_setup.bash를 source로 읽어야 빌드한 환경을 읽을 수 있음
- 노드를 실행시킬 때, 오류가 났다면 코드 고친 뒤 빌드까지 다시 할 것
- 파이썬과 ROS2를 이용하여 원하는 아이디어를 구현할 때는 파이썬으로 알고리즘 부분만 먼저 개발하고 그 코드를 ROS에 맞게 변환해서 적용하는 것이 효율적

## Log

|로그 레벨|설명|
|--|--|
|Fatal|시스템을 멈춰야 할 정도의 에러|
|Error|시스템의 오류|
|Warn|경고|
|Info|정보|
|Debug|-|

|명령어|설명|
|--|--|
|(node).get_logger().<로그 레벨>('메세지')||
  
## Linux Command
|명령어|설명|
|--|--|
|ls|현재 디렉토리 속 디렉토리들 보여줌|
|cd (이름)|현재 디렉토리를 (이름)으로 이동|
|rm (이름)|(이름)을 제거, -r 옵션으로 경고 없이 제거 가능, sudo를 통해 관리자 권한으로 제거 가능|
|mkdir (이름)|현재 디렉토리에 (이름) 디렉토리 생성|
|colcon build|src(소스코드 폴더)에 있는 코드들을 빌드|
|exit|터미널 끄기|

|단축키|설명|
|--|--|
|Ctrl + Alt + T|터미널 생성|
|Ctrl + Shift + T|터미널 탭 생성|
|Ctrl + Shift + V|붙여넣기|
|Tab|자동완성, 공백 후 두 번 연속으로 누르면 입력 가능 목록 등장|

## 운영체제
- **Terminal:**: 사용자가 명령을 내리는 공간
- **Shell:**: 사용자가 입력한 명령어와 커널이 이해할 수 있는 명령어 사이에서 해석
- **Kernel:** 컴퓨터의 자원을 관리

## Note
- 터미널을 볼 때 본능적으로 프롬프트의 앞부분을 보는 습관을 기르기
- 항상 내가 어떤 경로에서 명령을 실행하는지 신경 쓸 것
- 프롬프트의 ~은 HOME 폴더를 의미한다.
- export ROS_DOMAIN_ID=<ID>를 통해 시스템 도메인을 별도로 관리 가능하다.
