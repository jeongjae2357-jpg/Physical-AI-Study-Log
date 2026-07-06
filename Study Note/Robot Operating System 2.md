# Robot Operating System 2
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
- .bashrc파일은 bash의 각종 설정을 저장한다.
- ROS2를 실행하려면 source /opt/ros/버전/setup.bash 명령어를 입력해줘야 한다.
- .bashrc에 에 source /opt/ros/버전/setup.bash를 넣고 source ~/.bashrc로 간소화할 수 있다.
- alias를 통해 더 간소화할 수 있다.
- export ROS_DOMAIN_ID=<ID>를 통해 시스템 도메인을 별도로 관리 가능하다.
