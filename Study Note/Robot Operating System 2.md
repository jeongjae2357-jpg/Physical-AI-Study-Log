# Robot Operating System 2
## Concept
- **Node:** 실행 가능한 프로세스의 최소 단위
- **Service:** 클라이언트가 요청하고 서버가 응답하는 방식으로 두 노드가 데이터를 주고 받는 것
- **NameSpace:** 서비스 적용을 구분하기 위한 경로
- **Topic:** 토픽의 이름과 데이터의 구조를 공유하는 Publisher에서 Subscriber로 비동기적으로 데이터를 전달하는 방식


### Concept Note
- NameSpace 덕분에 경로가 유니크 해져서 통신간 얽힘이 없음
## Command
|명령어|설명|
|--|--|
|source /opt/ros/<버전>/setup.bash|환경변수 설정|
|ros2 run \<PKG Name> \<Node Name>|패키지의 노드를 실행 #\<Node Name>은 임의로 정하는 것이 아닌 executable 파일 임|
|ros2 node list|실행 중인 노드 목록|
|ros2 node info <경로>|노드의 정보를 조회|
|ros2 service list|실행 중인 노드에 제공되고 있는 서비스 목록|
|ros2 service type <경로>|해당 서비스가 사용하는 정의|
|ros2 interface show <경로>|해당 서비스나 토픽의 내용 확인|
|ros2 service call \<service name> \<service definition> "data" |서비스 요청|
|ros2 topic list|실행 중인 노드에 존재하는 토픽 목록|
|ros2 topic type <경로>|해당 토픽의 데이터 타입|
|ros2 topic info <경로>|해당 토픽의 데이터 타입과 publish, subscribe 상황 정보|
|ros2 topic pub --(once or rate <hz>) \<topic_name> \<msg_type> "<args>'|topic을 publish|
|ros2 topic echo <경로>|topic을 subscribe|

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

## Linux Command
|명령어|설명|
|--|--|
|ls|현재 디렉토리 속 디렉토리들 보여줌|
|cd (이름)|현재 디렉토리를 (이름)으로 이동|
|rm (이름)|(이름)을 제거, -r 옵션으로 경고 없이 제거 가능, sudo를 통해 관리자 권한으로 제거 가능|
|mkdir (이름)|현재 디렉토리에 (이름) 디렉토리 생성|
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
