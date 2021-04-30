# 배열

같은 타입의 여러 변수를 하나의 묶음으로 다루는 것

배열의 길이는 int 범위의 양의 정수(0 포함)이다

> ### 배열의 길이 변경
> 1. 더 큰 배열을 하나 생성한다
> 2. 기존 배열의 내용을 새로운 배열에 복사한다

## 배열의 복사

1. 더 큰 배열을 하나 생성한다
2. 반복문으로 기존 배열의 내용을 하나하나 옮긴다
3. 기존 배열의 참조 변수에 새 배열의 참조변수를 대입한다
   >기존 배열의 참조 변수가 새 배열을 가르키게 되어 기존 배열은 더 이상 사용할 수 없게된다

[배열복사 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch5/ArrayEx3.java)

[System.arraycopy()를 이용한 복사 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch5/ArrayEx4.java)

## 배열 활용

[섞기(shuffle) 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch5/ArrayEx7.java)

[버블정렬 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch5/ArrayEx10.java)

## 다차원 배열

2차원 이상의 배열도 선언가능 


그 중 2차원배열은 바깥쪽 배열이 행, 안쪽 배열이 열의 형태

따라서 바깥 배열의 요소가 1차원 배열 형태인 배열의 배열

> ### 선언 및 초기화
> * 타입[][] 변수이름 = new 타입[행][열]
> * 타입[][] 변수이름 = new 타입[][]{{},{},...};

### 가변 배열

배열의 배열인데 테이블형태가 아니라 안쪽 배열 가각의 길이가 다른 형태
> 배열의 길이를 바꿀 수 있는건 아닌데 왜 가변 배열인지는... 이름이 이상한듯

선언 시 열을 비워두고 바깥 배열의 각 요소마다 다른 길이를 갖도록 선언할 수 있음

```java
int[][] score = new int[3][];
score[0] = new int[2];
score[1] = new int[5];
score[2] = new int[4];

```

### 다차원 배열의 활용

[좌표에 X표하기 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch5/MultiArrEx1.java)

[행렬의 곱셈 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch5/MultiArrEx3.java)
