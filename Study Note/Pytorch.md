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
|torch.tensor(\<tensor>)|해당 크기와 원소들을 가지는 tensor를 반환|dtype, device|
|torch.empty(\<shape>)|해당 크기의 빈 tensor를 반환(메모리에 크기만 잡기 때문에 들어있는 값은 기존 메모리에 있던 값임)|dtype, device|
|torch.(zeros \| ones \| rand )(\<shape>)|해당 크기의 모든 원소를 (0 \| 1 \| 랜덤)으로 할당한 tensor를 반환|dtype, device|
|\<Tensor>.new_(zeros \| ones)(\<shape>)|기존 \<Tensor>와 같은 dtype, device를 사용하는 tensor를 반환|dtype, device|
|torch.(zeors \| ones \| randn)_like(\<tensor>)|기존 \<tensor>와 크기가 같은 tensor를 반환|dtype, device|
|\<Tensor>.size()|\<Tensor>의 크기 반환|-|

### Tensor 데이터 타입
|코드|설명|파라미터|
|--|--|--|
|torch.(cuda.)?FloatTensor(\<tensor>), torch.(cuda.)?HalfTensor(\<tensor>), torch.(cuda.)?ShortTensor(\<tensor>) ...|해당 데이터 타입을 가지는 tensor를 (VRAM에) 반환|-|
|\<Tensor>.dtype|데이터타입을 반환|-|
|\<Tensor>.item()|원소를 반환|-|
|\<Tensor>.(short()\|int()\|long()...)|기존 \<Tensor>의 데이터 타입을 변환|-|
|torch.device('cuda' if torch.cuda.is_available() else 'cpu')|cuda 사용 가능 여부에 따라 'cuda'나 'cpu'를 반환|-|
|\<Tensor>.to(\<device>)|기존 tensor의 device를 해당 \<device>로 변환|dtype|

#### Note
- AI피셜 과거 방식이므로 torch.tensor(dtype, device)나 torch.tensor().dtype().device()나 .to로 초기화하길 권장함

### Tensor 연산
|코드|설명|파라미터|
|--|--|--|
|torch.min(\<Tensor>)||<Tensor>의 원소 중 최소값을 반환|-|
|torch.max(\<Tensor>)||<Tensor>의 원소 중 최대값을 반환|-|
|torch.mean(\<Tensor>)||<Tensor>의 원소들의 평균을 반환|-|
|torch.std(\<Tensor>)||<Tensor>의 원소들의 표준편차를 반환|-|
|torch.prod(\<Tensor>)||<Tensor>의 원소들의 곱을 반환|-|
|torch.unique(\<Tensor>)||<Tensor>의 원소들 중 유니크한 값들을 반환|-|
|\<Tensor>.(max\|min)(dim)|해당 dim 기준으로 (최대\|최소)값을 각각 찾아 반환|-|
