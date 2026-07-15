# Pytorch
## Pytorch 구성 요소(수정 필요)
|구성 요소|설명|
|--|--|
|torch|메인 네임스페이스, 텐서 등의 다양한 수학 함수 함유|
|troch.autograd|자동 미분 기능 제공|
|torch.nn|신경망 구축을 위한 데이터 구조나 레이어를 함유|
|torch.optim|SGD를 중심으로 한 파라미터 최적화 알고리즘|
|torch.utils|데이터 조작 등의 유틸리티 기능 제공|
|torch.onnx|ONNX(Open Neural Network Exchange), 서로 다른 프레임워크 간의 모델을 공유|

## Tensor
- 데이터 표현을 위한 기본 구조로 GPU를 사용한 연산 가속을 가능하게 함

### Tensor 초기화
|코드|설명|파라미터|
|--|--|--|
|torch.tensor(<tensor>)|해당 크기와 원소들을 가지는 tensor를 반환|dtype|
|torch.empty(<shape>)|해당 크기의 빈 tensor를 반환(메모리에 크기만 잡기 때문에 들어있는 값은 기존 메모리에 있던 값임)|dtype|
|torch.rand(<shape>)|해당 크기의 랜덤한 원소를 할당한 tensor를 반환|dtype|
|torch.zeros(<shape>)|해당 크기의 모든 원소를 0으로 할당한 tensor를 반환|dtype|
|<Tensor>.new_ones(<shape>)|기존 tensor와 같은 dtype, device를 사용면서 원소가 1인 tensor를 반환|dtype|
|torch.randn_like(<Tensor>)|기존 <Tensor>와 크기가 같고 랜덤한 원소를 할당한 tensor를 반환|dtype|
