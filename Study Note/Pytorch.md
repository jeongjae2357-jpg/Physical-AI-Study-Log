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
|torch.tensor(\<tensor>)|해당 크기와 원소들을 가지는 tensor를 반환|dtype, device, require_grad|
|torch.empty(\<shape>)|해당 크기의 빈 tensor를 반환(메모리에 크기만 잡기 때문에 들어있는 값은 기존 메모리에 있던 값임)|dtype, device, require_grad|
|torch.(zeros \| ones \| rand \| randn)(\<shape>)|해당 크기의 모든 원소를 (0 \| 1 \| 랜덤 \| 정규분포 기반 랜덤)으로 할당한 tensor를 반환|dtype, device, require_grad|
|\<Tensor>.new_(zeros \| ones)(\<shape>)|기존 \<Tensor>와 같은 dtype, device를 사용하는 tensor를 반환|dtype, device, require_grad|
|torch.(zeors \| ones \| rand \| randn)_like(\<tensor>)|기존 \<tensor>와 크기가 같은 tensor를 반환|dtype, device, require_grad|
|\<Tensor>.size()|\<Tensor>의 크기 반환|-|

### Tensor 데이터 타입
|코드|설명|파라미터|
|--|--|--|
|torch.(cuda.)?FloatTensor(\<tensor>), torch.(cuda.)?HalfTensor(\<tensor>), torch.(cuda.)?ShortTensor(\<tensor>) ...|해당 데이터 타입을 가지는 tensor를 (VRAM에) 반환|-|
|\<Tensor>.dtype|데이터타입을 반환|-|
|\<Tensor>.item()|<Tensor>에 원소가 하나만 존재할 경우 그 원소를 반환|-|
|\<Tensor>.(short()\|int()\|long()...)|기존 \<Tensor>의 데이터 타입을 변환|-|
|torch.device('cuda' if torch.cuda.is_available() else 'cpu')|cuda 사용 가능 여부에 따라 'cuda'나 'cpu'를 반환|-|
|\<Tensor>.to(\<device>)|기존 tensor의 device를 해당 \<device>로 변환|dtype|

#### Note
- AI피셜 과거 방식이므로 torch.tensor(dtype, device)나 torch.tensor().dtype().device()나 .to로 초기화하길 권장함

### Tensor 연산
|코드|설명|파라미터|
|--|--|--|
|torch.min(\<Tensor>)|\<Tensor>의 원소 중 최소값을 반환|-|
|torch.max(\<Tensor>)|\<Tensor>의 원소 중 최대값을 반환|-|
|torch.mean(\<Tensor>)|\<Tensor>의 원소들의 평균을 반환|-|
|torch.std(\<Tensor>)|\<Tensor>의 원소들의 표준편차를 반환|-|
|torch.prod(\<Tensor>)|\<Tensor>의 원소들의 곱을 반환|-|
|torch.unique(\<Tensor>)|\<Tensor>의 원소들 중 유니크한 값들을 반환|-|
|torch.matmul(\<Tensor1>, \<Tensor2>) or torch.mm(\<Tensor1>, \<Tensor2>)|\<Tensor1>과 \<Tensor2>를 내적한 값을 반환|-|
|torch.svd(\<Tensor>)|\<Tensor>를 Singular Value Decomposition한 결과를 반환|
|\<Tensor>.(max\|min)(dim)|해당 dim 기준으로 (최대\|최소)값을 각각 찾아 반환|-|

#### Note
- in-place 방식: \<Tensor1>.연산_(\<Tensor2>)처럼 언더바(_)를 통해 구현 가능하며, \<Tensor1>과 \<Tensor2>를 연산한 결과를 \<Tensor1>에 넣는다는 의미

### Tensor 조작
|코드|설명|파라미터|
|--|--|--|
|\<Tensor>.view(\<크기>)|\<Tensor>의 크기를 재설정한 결과를 반환|-|
|\<Tensor>.squeeze()|\<Tensor>의 크기가 1인 모든 차원을 축소한 결과를 반환|인덱스를 넣어 특정 인덱스만 제거 가능|
|\<Tensor>.unsqueeze(dim)|\<Tensor>의 dim에 해당하는 1 차원을 생성한 결과를 반환|-|
|torch.stack([\<Tensor1>, \<Tensor2> ...])|크기가 같은 tensor들을 새로운 축 방향으로 쌓은 결과를 반환|-|
|torch.cat((\<Tensor1>, \<Tensor2> ...), dim)|dim의 축을 제외한 다른 모든 축이 반드시 같은 tensor들을 dim의 축으로 결합한 결과를 반환|-|
|torch.chunk(\<Tensor>, \<분할 개수>, dim)|\<Tensor>를 dim 축 기준으로 \<분할 개수>만큼 분할하여 각각을 반환|-|
|torch.split(\<Tensor>, \<분할 크기>, dim)|\<Tensor>를 dim 축 기준으로 각 tensor의 크기가 \<분할 크기>가 되게하여 각각을 반환|-|

#### Note
- 인덱싱과 슬라이싱 가능
- tensor의 크기를 재설정할 때, 원소 개수는 기존과 같아야 하고, -1을 주면 가능할 경우 컴터가 알아서 설정함
- stack은 새로운 축 방향으로 결합하고 cat은 기존 축 방향에서 결합
- .numpy()를 통해 넘파이로, torch.from_numpy(<배열>)을 통해 tensor로 변환 가능

## Autograd
### Basic Procedure
1. **x = torch.tensor([[a, b, c], [d, e, f], [g, h, i]], require_grad=True)**  기본 절차
   \# require_grad=True로 하여 x의 연산 과정을 추적
2. **--연산--**
3. **result.backward()**  
   \# 역전파를 구하고 싶은 기준 결과에서 backward() 메소드 시행하여 역방향으로 gradient 계산을 시행
4. **x.grad**  
   \# 역전파 결과로 연산을 추적하기 시작했던 tensor의 grad 변수에 $\frac{\partial result}{\partial x}$ 값을 저장

### Code
|코드|설명|파라미터|
|--|--|--|
|torch.tensor(\<tensor>, require_grad), \<Tensor>.require_grad_(\<bool>), |gradient 계산 그래프를 그리길 시작 여부를 설정 (기본 False)|-|
|\<Tensor>.backward()|역방향으로 gradient 계산을 시행|\<Vector>를 넣어 초기 gradient 설정 가능|
|\<Tensor>.grad|역전파 결과를 반환|-|
|\<Tensor>,grad_fn|추적한 연산을 반환|-|
|with torch.no_grad(): |해당 블럭 안에서는 autograd를 기록하지 않음|-|
|\<Tensor>.detach()|<Tensor>의 데이터는 유지하나 기존 gradient 계산 그래프를 분리한 tensor를 반환|-|

#### Code Note
- 역전파 과정 중 chain rule에 따라 중간 연산도 수행되긴 하지만 그 값은 grad에 저장되지 않음

## Handling Data 
### Module
- **torch.utils.data:** 여러 도구 모음
     - **Dataset:** 데이터를 어떻게 가져오는지를 정의한 클래스데이터 다루기
     - **DataLoader:** batch, shuffle 등을 다루는 클래스
- **torchvision:** 컴퓨터 비전과 관련된 작업을 지원하는 라이브러리
   - **datasets:** 이미지 데이터셋 제공
   - **transforms:** 이미지 전처리 기능 제공
   - **models:** 사전 학습된 이미지 모델 제공

### Code
|코드|설명|파라미터|
|--|--|--|
|transforms.Compose([\<전처리1>, \<전처리2>, ...])|여러 전처리들을 하나의 전처리 파이프라인으로 묶은 \<Transform> 객체를 반환|-|
|transforms.ToTensor()|torchvision이 처리하는 이미지 형태로 변환|-|
|transforms.Normalize(mean, std)|입력 데이터를 정규화하여 반환|-|
|DataLoader(\<dataset>, batch_size, shuffle, num_workers)|어느 \<dataset>인지, batch 크기, shuffle여부, num_workers 설정들을 저장한 \<DataLoader> 객체를 반환|-|
|iter(\<DataLoader>)|데이터를 순회하는 \<Iterator> 객체를 반환|-|
|next(\<Iterator>)|현 데이터 위치를 기억하고 있는 \<Iterator>객체에서 다음 데이터를 반환|-|

#### Note
- batch로 모델이 한번에 처리하는 데이터 개수를 조절하는 이유는 메모리 부족 현상이 발생할 수 있기 때문이다.
- num_workers는 데이터를 가져오는 작업을 몇 개의 프로세스가 동시에 할 것인지를 정함
- \<DataLoader>는 데이터를 Dataset으로부터 가져와 모델에게 batch만큼씩 제공함
- for문도 내부적으로 iter()을 실행한다 함

## Neural network
### Code
- import torch.nn as nn
|코드|설명|입력 tensor|
|--|--|--|
|nn.Linear(\<입력 차원>, \<출력 차원>)| tensor x를 입력 받아 xW^T + b 연산을 수행하는 Fully Connected layer를 생성|tensor의 마지막 차원을 입력 차원으로 간주|
|nn.Conv2d(\<입력 차원>, \<출력 차원>, kernel_size, stride, padding, bias)| tensor를 입력 받아 합성곱 연산을 수행하는 Convolution layer를 생성|(N, C, H, W) 형식의 tensor만 입력 받을 수 있음|
|\<Layer>(\<Tensor>)|해당 layer에 tensor를 입력하여 출력|-|

#### Note
- Layer들의 초기 weight와 bias은 랜덤으로 설정되고 후에 학습을 통해 Loss를 최소화하는 방향으로 재설정 되어감
