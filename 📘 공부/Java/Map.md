#collection #java #자료구조 

> 자바에서 Map은 **Key-Value 쌍을 저장하는 자료구조** 

## Map

+ `Map`은 `Key-Value` 쌍을 저장하는 자료구조
+ `Key`는 중복 불가하다. 
+ `Value`는 중복 가능
+ `Key`를 이용해서 `Value`를 빠르게 조회 가능
+ 순서를 보장하지 않는 구현체도 있고, 순서를 유지하거나 정렬하는 구현체도 있다.
+ Map의 주요 메서드

| 메서드                           | 설명                          |
| ----------------------------- | --------------------------- |
| `put(K key, V value)`         | 새로운 엔트리 추가 (동일 키가 있으면 값 갱신) |
| `get(Object key)`             | 키에 해당하는 값 조회                |
| `remove(Object key)`          | 특정 키 삭제                     |
| `containsKey(Object key)`     | 해당 키 존재 여부 확인               |
| `containsValue(Object value)` | 해당 값 존재 여부 확인               |
| `size()`                      | 엔트리 개수 반환                   |
| `isEmpty()`                   | 비어있는지 확인                    |
| `keySet()`                    | 모든 키 집합(Set) 반환             |
| `values()`                    | 모든 값 컬렉션(Collection) 반환     |
| `entrySet()`                  | 모든 엔트리(키-값 쌍) 집합(Set) 반환    |
## Map 주요 구현체

1. HashMap
	+ 가장 많이 사용된다.
	+ 순서가 보장되지 않는다.
	+ Null key는 1개 허용된다.
	+ Null value는 여러 개 허용된다.
	+ 조회 속도가 빠르다.

2. LinkedHashMap
	+ 삽입 순서를 보장한다.
	+ 순서가 있는 Map이 필요할 때 사용한다.
	+ 캐시 구현 시 자주 활용한다.

3. TreeMap
	+ 키 기준 정렬 (기본적으로 오름차순, 혹은 Comparator 지정 가능하다.)
	+ 내부적으로 레드-블랙 트리(Red-Black Tree)를 사용한다.
	+ 범위 검색에 유리하다.  (subMap, headMap, tailMap 등 지원)

4. ConcurrentHashMap
	+ 멀티스레드 환경에서 안전하면서 성능도 고려할 때 사용한다.
	+ 동시성 높은 환경에서 HashMap 대신 사용한다.

## 반복 (Iteration 방법)

`Map`은 바로 for-each로 돌릴 수 없고, `entrySet()`, `keySet()`, `value()`를 통해 순회해야한다.

```java

// entrySet() 사용
for (Map.Entry<String, Integer> entry : map.entrySet()) {
	System.out.println(entry.getKey() + " : " + entry.getValue());
}

// keySet() 사용
for (String key : map.keySet()) {
	System.out.println(key + " : " + map.get(key));
}

// value() 사용
for (Integer value : map.values()) {
	System.out.println(value);
}

```

## Map 장단점

+ 장점
	+ 키 기반의 접근 → 빠른 조회 가능
	+ 다양한 구현체 제공 → 상황에 맞게 선택해서 사용할 수 있다.
+ 단점
	+ 인덱스 기반 접근 불가
	+ 데이터 순서 유지 보장이 필요하면 구현체를 선택할 때 신중해야한다.
	+ 값(Value) 검색은 느리다. (ContainsValue 사용 시)

## Map - Key와 Value의 `equals` / `hashCode` 규칙

+ Map의 동작에서 핵심은 Key 비교 방식이다.
+ Key의 유일성은 `hashCode()`와 `equals()` 메서드에 의해 보장된다.
+ 규칙
	+ 동일한 객체라면 동일한 해시코드여아 한다.
	+ 해시코드가 같더라도 `equals()` 비교까지 같아야 동일한 key로 간주한다.
+ Map의 key로 사용할 객체는 반드시 `hashCode()`와 `equals()`를 재정의해야 한다.

```java
class Person {
    String name;
    int age;

    // equals & hashCode 오버라이딩 필수!
}
```

## Map - Null 허용 여부

+ HashMap
	+ null key → 1개 가능
	+ null value → 여러 개 가능
+ ConcurrentHashMap
	+ null key, null value 모두 불가능 (멀티스레드 환경에서 혼동을 방지하기 위함)

## Map의 고급 메서드

1. `getOrDefault` - key 없으면 기본값 반환

	```java
	// V getOrDefault(Object key, V defaultValue)
	int count = map.getOrDefault("apple", 0);
	```

2. `putIfAbsent()` - key가 없을 때만 추가

	```java
	// V putIfAbsent(K key, V value)
	map.putIfAbsent("banana", 10);
	```

3. `compute`, `computeIfAbsent`, `computeIfPresent` - 동적으로 값 계산 가능

```java
// V compute(K key, BiFunction<? super K, ? super V, ? extends V> remappingFunction)
// V computeIfAbsent(K key, Function<? super K, ? extends V> mappingFunction)
// V computeIfPresent(K key, BiFunction<? super K, ? super V, ? extends V> remappingFunction)

map.computeIfAbsent("apple", k -> 0);
map.computeIfPresent("apple", (k,v) -> v + 1);
```

4. `merge` - 값 병합 로직을 지정할 수 있다.

```java
// V merge(K key, V value, BiFunction<? super V, ? super V, ? extends V> remappingFunction)
map.merge("apple", 1, Integer::sum); 
//빈도 수 세기 같은 경우 코드가 훨씬 깔끔해짐.
```
