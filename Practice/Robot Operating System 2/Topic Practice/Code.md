# Code
**ros2 service call /turtle1/teleport_absolute turtlesim/srv/TeleportAbsolute "{x: 5.544445, y: 5.544445, theta: 1.570796}"** # 거북이의 초기 방향 정렬  
**ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 5, y: 0, z: 0}, angular: {x: 0, y: 0, z: 3.92699}}"** # 225도 만큼 회전하며 이동  
**ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 3.0738, y: 0, z: 0}, angular: {x: 0, y: 0, z: 0}}"** # 거북이가 그린 경로를 호로 갖는 부채꼴의 반지름: (5pi/4)*r = 5 -> r = 4/pi, 세 각도로 90도, 67.5도, 22.5도를 가지고 높이가 4/pi인 직각삼각형의 밑변 길이: tan(67.5)*4/pi = 3.0738  
**ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0, y: 0, z: 0}, angular: {x: 0, y: 0, z: 1.570796}}"**  
**ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 3.0738, y: 0, z: 0}, angular: {x: 0, y: 0, z: 0}}"**  
**ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 5, y: 0, z: 0}, angular: {x: 0, y: 0, z: 3.92699}}"**  

# Result
<img width="503" height="527" alt="image" src="https://github.com/user-attachments/assets/e79a781a-abbb-4511-a8e6-278f7f296131" />


## Note
- 터미널에서 실행한 코드
