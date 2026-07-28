# Isaac Sim
## Interface
### 객체 조작
|조작법|설명|
|--|--|
|Create 탭> \<원하는 Object>|Object 생성|
|Move(W), Rotate(E), Scale(R)|객체 조작|
|1. Create 탭> Xform <br> 2. <원하는 Object 집어 넣기>|Object 그룹화|
|1. Create 탭> Physics > Physics Scene <br> 2. <물리 엔진 적용하고자 하는 객체> -> Property > Add > Physics > Rigid Body with Colliders Preset|물리 엔진 설정 및 적용|
|Content -> 폴더: Isaac Sim > Robots > \<원하는 로봇의 .usd 파일 끌어 옴 or <br> Create 탭 > Robots > Asset Browser|로봇 로드|
|1. 연결하길 원하는 객첵들 선택 <br> 2. Create 탭 > Physics > Joint > \<원하는 Joint 선택> |관절 연결| 
|1. Create 탭 > Camera <br> 2. Window 탭 > Viewports <br> 3. 새로운 화면의 Perspective -> Camera |카메라 생성 및 카메라 시점 보기|

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
- 화면상에 보이는 stage에서 Scope Type은 폴더 개념으로 보면 됨
