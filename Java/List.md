> 자바에서 List는 **`순서가 있는 요소의 모음`** 
> 크기가 동적으로 늘어나고 줄어들 수 있다는 점이 큰 장점이다.

## List

+ 인터페이스 (`java.util.List<E>`)
+ 순서 유지 → index 기반의 접근이 가능하다.
+ 중복 허용 (같은 값을 여러 번 저장할 수 있다)
+ 주요 메서드
	+ `add(E e)` → 요소 추가
	- `get(int index)` → 특정 위치 값 조회
	- `remove(int index or Object o)` → 요소 삭제
	- `size()` → 크기 확인
	- `contains(Object o)` → 값 포함 여부
	- `addAll(Collection c)` → 다른 컬렉션 요소 모두 추가

## List 주요 구현체 비교

1. ArrayList 
	+ 실무에서 가장 많이 쓰인다.
	+ 초기 용량이 인자로 전달되지 않으면 기본적으로 10으로 저장되며, 해당 용량을 초과하면 자동으로 저장 용량이 늘어나게 된다.
	+ 빠른 조회, 느린 삽입/삭제
2. LinkedList
	+ 체인처럼 연결된 구조를 가지고 있다.
	+ 데이터가 불연속적으로 존재하며, 데이터가 서로 연결되어있다.
	+ 빠른 삽입/삭제 , 느린 조회

ArrayList는 인덱스를 통해 바로 데이터에 접근할 수 있어 검색이 빠르다.
하지만, 데이터를 삽입, 삭제할 때 뒤에 위치한 값들을 뒤로 밀어주거나 앞으로 당겨주어야 한다.

LinkedList는 데이터를 삽입, 삭제할 때 Prev와 Next의 주소 값만 변경하면 되므로 다른 요소들을 이동 시킬 필요가 없어 ArrayList보다 삽입, 삭제 성능이 좋다.

결론적으로 데이터의 잦은 변경을 예상한다면 `LinkedList`
데이터 개수가 변하지 않는다면 `ArrayList`를 사용하는 것이 좋다.

그 외, `Vector`, `Stack` 이 있다.


##  주요 기능 예시


#### 기본

```java
List<String> foods = new ArrayList<>();

// 추가
foods.add("햄버거");
foods.add("피자");
foods.add("국밥");

// 사이즈 확인
System.out.println("foods.size() : " + foods.size()); // foods.size() : 3

// 조회
System.out.println(foods.get(0)); // 햄버거 (입력한 순서대로)

/* 전체 조회 : 리스트의 모든 요소를 차례대로 꺼낸다.*/
for (String food : foods) {
	System.out.println(food);
}

// 수정
foods.set(2, "파스타"); // 국밥 → 파스타로 변경

// 포함 여부
System.out.println(foods.contains("햄버거")); // true

// 삭제
foods.remove("피자"); // 값으로 삭제
foods.remove(0); // 인덱스로 삭제

```

#### 리스트 합치기 
+ 이번 프로젝트 작업에서 판정 결과를 합치는 기능에 많이 사용했다.
```java
list1.addAll(list2); // list2의 내용을 list1에 전부 추가
```


참고한 페이지
> https://pongic.tistory.com/3 