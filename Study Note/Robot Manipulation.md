# Robot Manipulation
## 개념
- **Rigid body:** 외부에서 작용하는 어떠한 힘에 대해서도 물체 내부의 모든 임의의 두 점 사이 거리가 변하지 않는다고 가정한 물체
- **Link:** 관절 사이에 존재하는 물체
- **Configuration:** 로봇의 모든 점의 위치를 명시하는 것(로봇의 상태 하나)
- **Configuration space(C-space):** 한 로봇의 표현 가능한 모든 Configuration을 모아 놓은 공간,
- **Degrees of freedom(Dof):** Configuration을 표현하기 위해 필요한 최소한의 실수 좌표, C-space의 차원
- **Task space:** 로봇의 설계 목적의 맞는 작업이 이뤄지는 공간(작업에 의존, 로봇 구조와는 별개)
- **Workspace:** end-effector가 도달할 수 있는 가능한 모든 위치와 자세를 모아 놓은 공간 (로봇 구조에 의존, 작업과는 별개)

### Note
- 여러 부품들이 있더라도 그들 사이 상대적 움직임이 없다면 이를 묶어 하나의 강체로 볼 수 있다
- 이산적으로 표현되는 좌표는 Dof에 포함되지 않음
- Dof = (모든 점의 자유도의 합) - (독립적인 제약조건의 개수) or (몸체의 자유도의 합) - (독립적인 제약조건의 개수)
