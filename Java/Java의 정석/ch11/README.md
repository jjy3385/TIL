# 컬렉션 프레임웍

📌데이터 그룹을 다루는 표준화된 프로그래밍 방식

## 핵심 인터페이스

#### 상속계층도

- Collection 
  - List
  - Set

- Map

인터페이스 List 와 Set 의 공통점을 뽑아 Collection인터페이스로 묶음

Map 인터페이스의 경우는 전혀 다른 형태로 컬렉션을 다룸

| 인터페이스 | 특징                                                         |
| ---------- | :----------------------------------------------------------- |
| List       | 순서가 있음,중복허용<br />구현클래스 : ArrayList,LinkedList,Stack,Vector 등 |
| Set        | 순서는 유지하지 않음,중복을 허용하지 않음<br />구현클래스 : HashSet,TreeSet 등 |
| Map        | 키(key)와 값(value)의 쌍으로 이루어짐<br />순서는 유지하지 않음,키는 중복을 허용하지 않고 값은 중복 허용<br />구현클래스 : HashMap,TreeMap,HashTable,Properties 등 |

> Vector,Stack,HashTable,Properties 는 컬렉션 프레임웍이 만들어지기 이전부터 존재하던 것들이라 명명법을 따르지 않았음
>
> Vector -> ArrayList 를, HashTable은 HashMap을 쓰는게 좋음



## 1.Collection 인터페이스

List 와 Set의 조상으로 컬렉션 클래스에 저장된 데이터를 읽고 추가하고 삭제하는 등 컬렉션을 다루는데 가장 기본적인 메서드를 정의하고 있다.

### List인터페이스

중복을 허용하면서 저장순서가 유지되는 컬렉션을 구현하는데 사용

#### 상속계층도(List인터페이스를 구현한 클래스)

- List
  - Vector
    - Stack
  - ArrayList
  - LinkedList

### Set인터페이스

중복을 허용하지 않고 저장순서가 유지되지 않는 컬렉션 클래스를 구현하는데 사용

#### 상속계층도(Set인터페이스를 구현한 클래스)

- Set
  - HashSet
  - SortedSet
    - TreeSet

### Map인터페이스

키(key)와 값(value)을 하나의 쌍으로 묶어서 저장하는 컬렉션 클래스를 구현하는데 사용

키는 중복X,값은 중복 허용

중복된 키로 키와 값을 입력하면 기존에 입력됨 키와 값을 찾아 값을 덮어씀

#### 상속계층도(Map인터페이스를 구현한 클래스)

- Map
  - HashTable
  - HashMap
    - LinkedHashMap
  - SortedMap
    - TreeMap

#### Map.Entry인터페이스

Map인터페이스의 내부 인터페이스

Map에 저장되는 key-value쌍을 다루기 위한 내부 인터페이스

## 2.ArrayList

List인터페이스를 구현하였기 때문에 저장순서가 유지되고 중복을 허용한다

Object배열을 이용하여 데이터를 순차적으로 저장함

> ⁉ String이 char배열을 저장공간으로 갖고 거기다 이런저런 기능들을 추가한 것과 별반 다르지 않음

```java
public calss ArrayList extends AbstractList implements List,RandomAceess,Cloneable,java.io.Serializable{
...
	transient Object[] elementData;	//Object 배열
...
}
```

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/ArrayListEx1.java)

> 컬렉션 내 저장공간이 배열이기 때문에 중간 요소를 삭제할 경우 삭제된 요소 뒤에 있는 요소들은 자동으로 한칸앞으로 당겨짐

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/VectorEx1.java)

#### Vector의 용량과 크기

* trimToSize() 호출 시 size와 capacity가 같도록 함

  이때, 배열은 크기를 변경할 수 없으므로 새로운 배열을 생성하여 그 주소값을 변수 v에 할당한다

- ensureCapacity(6) 는 변수 v의 capacity가 최소한 6이 되도록함

  1보다 큰 경우, 아무일도 일어나지 않고 6보다 작으면 크기가 6인 새로운 배열을 생성하여 v의 내용을 복사한다

* setSize(7) 호출 시 v의 size가 7이 되도록 함

  v 의 capacity가 충분하면 새로운 인스턴스를 생성하지 않지만, capacity가 6이므로 새로운 인스턴스를 생성해야함

  그리고 capacity가 부족한 경우엔 자동적으로 기존 capacity의 2배로 생성함

> 위의 예제로 봤을 때, ArrayList나 Vector같이 List인터페이스를 구현한 컬렉션들은 데이터를 읽어오고 저장하는 효율은 좋지만 용량을 변경해야될 때는 새로운 배열을 생성한 후 기존 배열의 정보를 복사해줘야되기 때문에 효율이 극히 낮을 수 있다

#### 🚩MyVector 구현

> List인터페이스를 상속받는 객체를 직접 구현해보는 연습을 더 많이 해봐야함

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/MyVector.java)

`Object remove(int index)`메서드는 지정한 위치에 있는 객체를 삭제하고 삭제한 객체를 반환하도록 작성한다

삭제할 객체의 바로 아래에 있는 데이터를 한칸씩 위로 복사해서 삭제할 객체를 덮어쓰는 방식으로 처리한다

만일 삭제할 객체가 마지막 객체라면 그냥 null로 바꿔주기만 하면된다

## 3.LinkedList

배열(ArrayList)의 장점과 단점

* 장점: 접근시간이 빠르다

* 단점

  * 크기를 변경할  수 없다

    크기를 변경하지 못하기 때문에 새로운 배열을 생성해서 복사해줘야됨

    또는 미리 배열의 크기를 충분히 크게 만들어놔야되는데 이땐, 메모리 낭비가 생길 수 있음

  - 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸림

    차례대로 데이터를 추가하고 마지막부터 삭제하면 큰 부하가 없지만 중간에 데이터를 삽입한다거나 지우게되면 삽입한 이후 요소를 모두 밀어야된다거나 당겨붙여야되기 때문에 비효율이 발생함

어쨋든 이러한 단점을 보완하기 위해 LinkedList가 나옴

배열은 모든 데이터가 연속적으로 존재하지만 링크드리스트는 불연속적으로 존재하면서 그냥 연결만 갖는 형태임

즉, **링크드 리스트의 각 요소(node)는 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성됨**

```java
class Node{
	Node next;	//다음 요소의 주소
	Object obj;	//데이터
}
```

그러므로 중간 데이터를 삽입하거나 지울때 앞,뒤 주소값만 바꿔주면 됨

참고로 링크드 리스트의 이동방향은 단방향으로 다음 요소에 대한 접근은 쉽지만 이전요소에 대한 접근은 어려움

이런 단점을 보완한 것이 더블 링크드 리스트이다.

```java
class Node{
    Node next;		//다음 요소
    Node previous;	//이전 요소
    Object obj;		//데이터
}
```

또한 더블 링크드 리스트보다 더 접근성을 향상시킨 형태인 더블 써큘러 링크드 리스트도 있다

더블 링크드 리스트와 똑같은데 첫번째 요소와 마지막 요소를 서로 연결시킨 형태이다

그리고 **🚩실제 LinkedList 클래스는 더블 링크드 리스트로 구현**되어 있다

#### ArrayList와 LinkedList 간 성능 예제

[예제 - 추가/삭제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/ArrayListLinkedListTest.java)

* 순차적인 추가/삭제는 ArrayList가 빠르다

  참고로 순차적인 삭제란 마지막 데이터부터 역순으로 삭제하는 것을 말함

  그래야 데이터 재배치 없이 삭제가 되므로

* 중간 데이터를 추가/삭제하는 경우엔 LinkedList가 빠르다

  LinkedList는 요소간의 연결만 변경하면 되지만 ArrayList는 데이터 재비치로 인한 손실이 발생함

[예제 - 접근속도](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/ArrayListLinkedListTest2.java)
$$
인덱스가 n 인 데이터의 주소 = 배열의 주소 + ( n * 데이터 타입의 크기)
$$

* 배열은 각 요소들이 연속적인 메모리상에 존재하기 때문에 간단한 계산으로 원하는 요소의 주소를 얻을 수 있음

- LinkedList 는 불연속적으로 위치한 각 요소들이 서로 연결된 것이라 처음부터 n번째 데이터까지 차례대로 따라가야만 원하는 값을 얻을 수 있음

## 4.Stack 과 Queue

### Stack

LIFO(last in first out)

먼저 넣는게 밑에 깔려서 나중에 나오게 되는 형태로 척척 쌓아올리는 지층같은 느낌

순차적으로 데이터를 추가하고 삭제하는 스택은 **ArrayList**로 구현되어 있음

### Queue

FIFO(first in first out)

먼저 넣는게 먼저 나오는 파이프 느낌

데이터의 추가/삭제가 쉬운 **LinkedList**로 구현됨

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/StackQueueEx.java)

#### Stack 직접 구현

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/MyStack.java)

Stack 의 `int search(Object o)` 메서드의 인덱스값은 가장 마지막에 입력한 객체의 인덱스가 1로 나옴

즉, Stack의 인덱스 =  size - 내부 배열의 인덱스

> 스택과 큐 활용 예
>
> 스택 - 수식계산,수식괄호검사,워드프로세서의 undo/redo,웹브라우저의 뒤로/앞으로 등
>
> 큐 - 최근사용문서,인쇄작업 대기목록,버퍼 등

#### PriorityQueue

저장한 순서에 관계없이 우선순위가 높은 것부터 꺼내게 됨

객체를 저장하는 경우, 객체의 크기를 비교할 수 있는 방법을 제공해야함

> compareTo,Comparator 랑 관련이 있을 듯

#### Deque(Double-Ended Queue)

양쪽 끝에서 추가/삭제가 가능한 Queue

스택과 큐를 하나로 합쳐놓은 것과 같으며 스택으로 사용할 수도 있고, 큐로 사용할수도 있음

## 5.Iterator,ListIterator,Enumeration

컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스

컬렉션에 저장된 요소를 표준화된 방식으로 접근할 수 있도록 해줌

즉,코드의 재사용성을 높여줌 => 객체지향적 특징

### Iterator

컬렉션 각 요소에 접근하는 기능을 가진 Iterator인터페이스를 정의하고 Collection인터페이스에서는 Iterator를 반환하는 iterator()를 정의함

즉, Collection인터페이스를 상속받는 클래스들(컬렉션 클래스들)은 iterator() 메서드를 구현해야하고 iterator의 반환형은 Iterator를 구현한 클래스의 인스턴스임

ArrayList에 저장된 요소들을 출력하기 위한 코드

```java
Collection c = new ArrayList();	//다른 컬렉션으로 변경시 이 부분만 고치면 됨
Iterator it = c.iterator();
while(it.hasNext()){
    System.out.println(it.next());
}
```

> 참조변수를 ArrayList가 아니라 Collection으로 선언한 이유
>
> Collection에 없고 ArrayList에 있는 메서드를 사용하는게 아니라면 Collection타입의 참조변수로 선언하는 것이 좋음
>
> * 코드 재사용성을 올라감 ArrayList가 아니라 linkedList로 바꿔야한다면 new 이후만 바꾸면 됨
> * 참조타입이 Collection이라는 것의 의미는 Collection 에 선언된 멤버만 사용하겠다는 뜻을 내포하고 있음

### Enumeration 과 ListIterator

* Enumeration -  Iterator의 구버젼

* ListIterator - Iterator에 양방향 조회기능 추가

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/ListIteratorEx1.java)

> Iterator의 remove()는 단독으로 쓰일 수 없고 next() 와 같이 써야함
>
> 특정위치의 요소를 삭제하는 것이 아니라 읽어 온 것을 삭제하는 메서드임
>
> next() 호출없이 remove()를 호출하면 IllegalStateException 예외 발생

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/IteratorEx2.java)

#### Iterator구현 예제

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/MyVector2.java)

cursor는 앞으로 읽어올 요소의 위치를 저장하는데 사용되고, lastRet은 마지막으로 읽어온 요소의 위치를 저정하는데 사용된다

remove()를 호출하면 이미 next()를 통해서 읽은 위치의 요소인 lastRet에 저장된 값을 읽어 그 위치에 있는 요소를 삭제하고 lastRet을 -1로 초기화한다

그리고 커서는 1 감소시킨다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/MyVector2Test.java)

## 6.Arrays

배열을 다루는데 유용한 메서드를 담고있는 클래스

#### 배열의 복사 - copyOf(),copyOfRange()

#### 배열 채우기 - fill(),setAll()

#### 배열의 정렬과 검색 - sort(),binarySearch()

#### 배열의 비교와 출력 - equals(),toString(),deepEquals(),deepToString() 

#### 배열을 List로 변환 - asList(Object... a)

매개변수의 타입이 가변인자임, 즉 매개변수 개수 제한 없이 저장할 요소들만 나열하는 것도 가능 

#### parallelXXX(),spliterator(),stream() 등

## 7.Comparator와 Comparable

Comparator와 Comparable은 모두 인터페이스로 컬렉션을 정렬하는데 필요한 메서드를 정의하고 있다

즉, 이 두 인터페이스를 구현하고 있는 클래스라면 컬렉션에 담았을 때 정렬이 가능하다

```java
public interface Comparator{
    int compare(Object o1, Object o2);
}

public interface Comparable {
    public int compareTo(Object o);
}
```

compare(),compareTo() 의 반환값

* 비교하는 두 객체가 같으면 0
* 비교하는 값보다 작으면 음수
* 비교하는 값보다 크면 양수

#### Comparable - 기본 정렬기준을 구현하는데 사용

#### Comparator - 기본 정렬기준 외에 다른 기준으로 정렬하고자할 때 사용

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch11/ComparatorEx.java)

첫번째 정렬구문 `Arrays.sort(strArr);`은 따로 정렬기준을 정해주지 않았다

이 경우엔 strArr 인스턴스에 구현된 내용에 따라 정렬된다.

즉, 이 경우엔 String 클래스가 comparable을 상속받아 구현한 메서드가 내부적으로 작동하면서 정렬이 구현되는 것임

따로 정렬기준을 정해주지 않은 경우엔 대부분 comparable 을 구현한 경우이다

두번째 정렬구문 `Arrays.sort(strArr,CASE_INSENSITIVE_ORDER)`는 Comparator를 상수의 형태로 제공한 것임

마지막 정렬구문 `Arrays.sort(strArr,new Descending());`의 경우 지정한 comparator구현 클래스의 메서드에 의해서 정렬이 수행된다

## 8.HashSet



