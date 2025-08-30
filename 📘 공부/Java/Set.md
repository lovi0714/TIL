#collection #java #자료구조 

> 자바에서 Set은 중복을 허용하지 않고, 순서가 보장되지 않는 자료구조

## Set

+ `Set`은 중복을 허용하지 않고, 순서가 보장되지 않는 자료구조이다.
+ 같은 요소를 두 번 이상 `add`, 추가하려고 하면 자동으로 중복이 제거된다.
+ 주요 메서드

| 메서드                         | 설명                     |
| --------------------------- | ---------------------- |
| `add(E e)`                  | 요소 추가 (중복이면 무시)        |
| `addAll(Collection c)`      | 다른 컬렉션의 모든 요소 추가 (합집합) |
| `remove(Object o)`          | 특정 요소 제거               |
| `removeAll(Collection c)`   | 다른 컬렉션의 요소 제거 (차집합)    |
| `retainAll(Collection c)`   | 교집합 (공통 요소만 유지)        |
| `contains(Object o)`        | 특정 요소 포함 여부 확인         |
| `containsAll(Collection c)` | 다른 컬렉션의 모든 요소 포함 여부 확인 |
| `size()`                    | 요소 개수 반환               |
| `isEmpty()`                 | 비어있는지 여부 확인            |
| `clear()`                   | 모든 요소 제거               |
| `iterator()`                | 반복자 반환 (for/while 순회)  |
| `stream()`                  | Stream 생성 (Java 8+)    |
| `toArray()`                 | 배열로 변환                 |

## Set 주요 구현체

1. HashSet
	+ 가장 많이 쓰인다.
	+ 내부적으로 HashMap을 사용하여 구현된다. (마찬가지로 `hashCode()`와 `equals`가 중요하다)
	+ 순서가 보장되지 않는다.
	+ 검색, 추가, 삭제 성능이 빠르다.
	+ 실무에서는 중복 제거, 빠른 검색 용도로 자주 사용한다.

2. LinkedHashSet
	+ `HashSet`을 상속하면서, `LinkedList`로 연결하여 삽입 순서를 보장한다.
	+ 성능은 `HashSet`과 비슷하거나, 약간 느릴 수 있다.
	+ 중복 제거 + 입력 순서 유지가 필요할 때 사용한다.
	+ ex) 로그 기록 순서, 사용자 입력 순서를 유지하면서 중복을 제거 할 때 등

3. TreeSet
	+ 내부적으로 Red-Black Tree (이진 탐색 트리) 기반
	+ 요소를 자동으로 정렬한다. (기본 : 오름차순)
	+ 정렬된 상태를 유지 + 중복 제거가 필요할 때 사용한다.
	+ `Comparator`를 사용하여 커스텀 정렬이 가능하다.

## 반복 

#### 1. 향상된 for문 (for-each)

```java
Set<String> set = new HashSet<>();
set.add("A");
set.add("B");
set.add("C");

for (String s : set) {
    System.out.println(s);
}
```

#### 2. Iterator 사용

+ `Set`은 `iterator`를 제공한다.
+ 순회 중 `remove()` 사용할 때 유용하다.
	⚠️ `for-each`문에서 `set.remove()` 하면 `ConcurrentModificationException` 발생할 수 있다.  
	👉 요소 제거하면서 순회할 땐 `Iterator.remove()` 사용해야 한다.


```java
Iterator<String> it = set.iterator();
while (it.hasNext()) {
    String s = it.next();
    System.out.println(s);
}
```


## Set의 장단점

#### ✅ 장점

1. **중복 허용하지 않는다**
    - 자동으로 중복 제거 → 코드가 단순해진다 
    - `List`에서 중복 제거하려면 `contains()` 검사 + 로직 필요하지만, `Set`은 `add()`만으로 해결된다.
        
2. **빠른 검색 성능 (특히 HashSet)**  
    - `contains()`, `add()`, `remove()`가 평균 O(1) (Hash 구조 덕분)
    - "존재 여부 확인" 작업에 최적화됨
        
3. **집합 연산 지원**
    - `retainAll()` (교집합), `addAll()` (합집합), `removeAll()` (차집합) 제공
    - 데이터 전처리, 필터링 작업에 유용
        
4. **다양한 구현체 제공**
    - HashSet → 빠른 성능
    - LinkedHashSet → 순서 유지 + 중복 제거
    - TreeSet → 자동 정렬 + 중복 제거

---

#### ❌ 단점

1. **인덱스 접근 불가**
    - `List`처럼 `get(0)` 불가능 → 특정 위치 요소 접근이 필요하면 불편하다.
    - 필요할 경우 `List`로 변환해야한다. (`new ArrayList<>(set)`)
        
2. **순서 보장 안 됨 (HashSet)**
    - 데이터 입력 순서대로 나오지 않음 → UI 출력 등 순서가 중요한 경우 부적합하다.
    - 삽입 순서 유지가 필요하다면 `LinkedHashSet` 사용해야 한다.
        
3. **메모리 사용량 증가 가능**
    - Hash 구조를 사용하므로 같은 데이터 양이라도 `List`보다 메모리를 더 차지할 수 있다.
        
4. **equals()/hashCode() 올바른 구현 필요**
    - 사용자 정의 객체를 `Set`에 넣을 경우, `equals`와 `hashCode`를 잘못 구현하면 중복 제거가 제대로 안 된다.
        
5. **정렬 성능 이슈 (TreeSet)**
    - `TreeSet`은 정렬 유지 때문에 성능이 O(log n) → 대량 데이터 삽입 시 HashSet보다 느리다.
      

