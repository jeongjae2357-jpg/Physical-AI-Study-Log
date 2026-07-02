# Python
## Data
### *Operater*
- **/:** 몫  
- **//:** 몫(소수점 버림)  
- **%:** 나머지  
- __**:__ 제곱

### *Fuction*
- **type(data)** : data의 자료형을 반환
- **cast:** int("str"), float("str"), str(data)
- **input():** 사용자의 입력을 문자열 형태로 반환

## List
### *Operater*
**list_a + list_b:** list_b를 list_a 뒤에 합병한 리스트를 반환
**list * (상수):** list를 (상수) 번 반복한 리스트를 반환
**list[start : end : stride]:** start<= index < end 범위의 인덱스를 stride만큼 건너 뛰어가며 슬라이싱
**element (not) in list:** 리스트 내부에 요소를 포함하는지를 bool로 반환
__*list:__ list를 전개 *#Non-Mutate*

### *structure*
[element, elemnt, ...]

### *Fuction*
- **len(list):** 리스트 원소 개수를 반환
- **del list[index]:** index에 위치한 요소를 제거 *#Mutate*
- 
### *Method*
- **append(element):** 리스트 맨 뒷단에 요소 추가 *#Mutate*
- **insert(pos, element):** 리스트 pos 위치에 요소 추가 *#Mutate*
- **extend(list):** 리스트 뒤에 입력 리스트를 합병 *#Mutate*
- **list.pop(index):** index에 위치한 요소를 제거 후 반환 *#Mutate*
- **list.remove(element):** 리스트의 요소를 제거 *#Mutate*
- **list.clear():** 리스트의 요소를 전부 제거 *#Mutate*
- **list.sort(reverse):** 리스트 오름차순(내림차순) 정렬 *#Mutate*
- 
### *Note*
- 리스트 요소로 여러 자료형 혼합 가능
  
## Identifier 
### *Rule*
- 키워드 X
- 특수 문자는 언더 바(_)만 허용
- 숫자로 시작 X
- 공백 포함 X
  
### *Type*
- snake_case
- CamelCase

## String
### 
- 문자열 내부에 큰따옴표, 작은따옴표를 넣고 싶다면 \ 뒤에 넣기
- \n: 줄바꿈, \t: 탭

### *Operater*
- **"str" + "str":** 문자열 연결
- **"str" * (상수):** 문자열 (상수) 번 반복
- __+=, *=__ 사용 가능
- **"str"[index]**: index 위치의 문자 반환
- **"str"[num1:num2]:** 문자열 슬라이싱
- 
### *Fuction*
- **len("str"):** 문자열 길이를 반환

### *Method*
- **upper(), lower():** 대소문자 변환
- **strip(), lstrip(), rstrip():** 끝단 공백 제거
- **is00:** 문자열이 00으로 구성되어있는지 판단하여 bool 반환
- **find("str"), rfind("str"):** 문자열 내부에 "str"이 위치한 index를 반환
- **"찾는 str" in "기반 str":** "기반 str"이 "찾는 str"을 포함하는지 bool로 반환
- **split("기준 str"):** "기준 str"을 기준으로 문자열을 분할하여 list 형태로 반환
- **f"str":** "str" 내부에 중괄호 속 내용을 문자열로 바꿔 반환
- 
## Conditional statement   
### *Operater*
- **비교 연산자:** (a<x<b)
- **논리 연산자:** and, or, not 

### *if structure*
if 표현식:
(들여쓰기)표현식이 참인 경우 실행  

### *Note*
- 표현식이 None, 0, 0.0라면 False로 나머지는 True로 간주
- pass키워드로 골격만 잡아두기 가능

## Loop statement
### *for structure*
for 반복자 in 반복할 수 있는 것:
(들여쓰기)코드
