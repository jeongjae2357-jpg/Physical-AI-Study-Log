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

## Identifier 
### *Rule*
- 키워드 X
- 특수 문자는 언더 바(_)만 허용
- 숫자로 시작 X
- 공백 포함 X
  
### *Type*
- snake_case
- CamelCase

## List
### *Structure*
[element, elemnt, ...]

### *Operater*
- **list_a + list_b:** list_b를 list_a 뒤에 합병한 리스트를 반환
- **list * (상수):** list를 (상수) 번 반복한 리스트를 반환
- **list[start : end : stride]:** start<= index < end 범위의 인덱스를 stride만큼 건너 뛰어가며 슬라이싱
- **element (not) in list:** 리스트 내부에 요소를 포함하는지를 bool로 반환
- __*list:__ list를 전개 *#Non-Mutate*

### *Fuction*
- **len(list):** 리스트 원소 개수를 반환
- **del list[index]:** index에 위치한 요소를 제거 *#Mutate*
- **min(list):** 리스트 내부 요소 중 최소값 반환
- **max(list):** 리스트 내부 요소 중 최대값 반환
- **sum(list):** 리스트 내부 요소들을 모두 더한 값 반환
- **reversed(list):** 리스트 내부 요소들의 역순서인 리스트를 반환
- **list(enumerate(list)):** 리스트의 인덱스와 요소를 매핑한 리스트를 반환
  
### *Method*
- **append(element):** 리스트 맨 뒷단에 요소 추가 *#Mutate*
- **insert(pos, element):** 리스트 pos 위치에 요소 추가 *#Mutate*
- **extend(list):** 리스트 뒤에 입력 리스트를 합병 *#Mutate*
- **pop(index):** index에 위치한 요소를 제거 후 반환 *#Mutate*
- **remove(element):** 리스트의 요소를 제거 *#Mutate*
- **clear():** 리스트의 요소를 전부 제거 *#Mutate*
- **sort(reverse):** 리스트 오름차순(내림차순) 정렬 *#Mutate*

### *Note*
- 리스트 요소로 여러 자료형 혼합 가능

## Dictionary
### *Structure*
{  
키A: 값,  
키B: 값,  
키C: 값,  
}

### *Operator*
- **dict[key]:** key와 매핑되는 값을 반환
- **dict[new key] = new data:** 딕셔너리에 새로운 키와 값을 추가
- **del dict[key]:** 딕셔너리에 키와 값을 제거
- **key in dict:** 딕셔너리 내부에 해당 키가 있는지 bool로 반환

### *Method*
- get(key): key와 매핑되는 값을 반환
- items(): 딕셔너리의 키와 값을 매핑

### *Note*
- 딕셔너리의 키로 bool, 숫자도 사용 가능

## Tuple
### *Structure*  
(요소, 요소, ...)  

### *Note*
- 한번 결정된 요소는 바꿀 수 없음
- (요소, ): 요소를 하나만 가지는 튜플
- tuple = 요소1, 요소2.. 처럼 괄호 없이 사용 가능
- a, b = b, a 처럼 값 교환 가

## String
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

### *Note*
- 문자열 내부에 큰따옴표, 작은따옴표를 넣고 싶다면 \ 뒤에 넣기
- \n: 줄바꿈, \t: 탭

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

### *while structure*
while 표현식:  
(들여쓰기)코드

### *Operator*
- **break:** 해당 키위드와 가장 가까운 반복문을 빠져나옴
- **continue:** 해당 키위드 이후 코드들은 건너뛰고 가장 가까운 반복문의 조건식으로 이동

### *Note*
- 반복문을 역으로 진행하고 싶다면 stride를 음수로 주거나 reversed() 이용

## Fuction
### *Structure*
def 함수 이름(매개변수, ...):  
(들여쓰기)코드

### *Note*
- 가변 매개변수 __*__ 는 위치인자를 여러 개 받음
- 가변 매개변수 __**__ 는 키워드인자를 여러 개 받음
- 가변 매개변수 뒤에 일반 매개 변수가 올 수 없으며 함수 당 하나만 사용 가능
- 기본 매개변수는 함수 선언에서부터 초기화 함
- 기본 매개변수 뒤에 일반 매개 변수가 올 수 없음
- 키워드 매개변수로 이름을 지정해서 값을 입력할 수 있음

## File
### *Function*
- **open("name", "mode"):** 파일 열기

### *Method*
- **close():** 파일 닫기
- **write(내용):** 파일에 내용 쓰기
- **read():** 파일에 내용 읽기

### *Note*
- With open() as file:로 파일 자동 닫기 가능

## Exception Handling
### *Structure*
try:  
(들여쓰기)예외 발생 가능성이 있는 코드  
except 예외 종류1 as 예외 객체를 활용할 변수 이름:  
(들여쓰기)예외 발생시 실행할 코드  
except 예외 종류2 as 예외 객체를 활용할 변수 이름:  
(들여쓰기)예외 발생시 실행할 코드  
except 예외 종류3 as 예외 객체를 활용할 변수 이름:  
(들여쓰기)예외 발생시 실행할 코드  
else:
(들여쓰기)예외가 발생하지 않았을 때 실행할 코드  
finally:
(들여쓰기)무조건 실행할 코드  

### *Exception Object*
- **Exception:** 모든 예외의 부모
- **ValueError:** 값이 잘못되었을 때의 예외
- **IndexError:** 인덱스 잘못 접근했을 때의 예외

### *Note*
- raise 키워드 로 예외 강제 발생 가능
