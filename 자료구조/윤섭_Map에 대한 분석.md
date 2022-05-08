# Map에 대한 분석

<aside>
💡 정의: Key와 Value가 쌍을 이루는 자료구조

</aside>

### ⚙️Java Document에서의 **Map**

([https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html))

```java
public interfaceMap<K,V>
```

An object that maps keys to values. A map cannot contain duplicate keys; each key can map to at most one value.

 → 키를 값에 매핑하는 개체임

This interface takes the place of the `Dictionary` class, which was a totally abstract class rather than an interface.

 → 이 인터페이스는 Dictionary랑 비슷하다 

The `Map` interface provides three *collection views*, which allow a map's contents to be viewed as a set of keys, collection of values, or set of key-value mappings. The *order* of a map is defined as the order in which the iterators on the map's collection views return their elements. Some map implementations, like the `TreeMap` class, make specific guarantees as to their order; others, like the `HashMap` class, do not.

---

### ⚙️Java Document에서의 Dictionary

[https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Dictionary.html](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Dictionary.html)

```
public abstract classDictionary<K,V>
extends Object
```

The Dictionary class is the abstract parent of any class, such as Hashtable , which maps keys to values.

 → dictionary는 hashtable처럼 값을 매핑하는 모든 자료구조의 부모임

Every key and every value is an object. In any one Dictionary object, every key is associated with at most one value. Given a Dictionary and a key, the associated element can be looked up. Any non-null object can be used as a key and as a value.

 → 모든 Key와 모든 value는 1대1 대응한다 (Null제외 모든 값 사용 가능)

As a rule, the `equals` method should be used by implementations of this class to decide if two keys are the same.

 → Key가 같은지 확인하려면 equals메소드 쓰셈(우리에겐 너무 당연한 것)

**NOTE: This class is obsolete. New implementations should implement the Map interface, rather than extending this class.**

 → 이제 안써연!

<aside>
💡 의문 1: 왜 인터페이스가 아니라 추상 클래스로 구현된걸까?

</aside>

<aside>
💡 의문 2: Dictionary클래스가 사장된 경위는 어떤게 있을까?

</aside>

---

### Map의 종류

<aside>
💡 HashMap
1. Key-value Null값 허용
2. 내부적으로 Hash함수를 사용하여 메모리 성능 굿

</aside>

<aside>
💡 TreeMap
1. Key값이 오름차순으로 정렬됨
2. Null값 미허용

</aside>

![Untitled](Map%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A1%E1%86%AB%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%2097500d2956c847c48708d946b04aeb02/Untitled.png)

<aside>
💡 HashTable
1. Null값 미허용
2. 동기화 제공

</aside>

<aside>
💡 linkedHashMap
linkedList → 들어간 순서대로 순서를 보장

</aside>

---

### 그럼 HashTable과 HashMap의 차이는 무엇일까?

<aside>
💡 힌트: vector와 ArrayList의 차이와 동일

</aside>

- 정답
    
    HashMap은 Thread-safe하지 않고, HashTable은 Thread-safe하다.
    
    즉 HashMap은 멀티 스레딩한 상황이 생겼을 때 동기화를 지원하지 않아 값의 오류가 날 수 있다!