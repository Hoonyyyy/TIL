# List와 ArrayList 차이

https://velog.io/@dnwlsrla40/List-ArrayList-%EB%B0%B0%EC%97%B4-%EC%84%A0%EC%96%B8-%EC%8B%9C-List%EC%99%80-ArrayList-%EC%B0%A8%EC%9D%B4

- list : 인터페이스 ( 도형 )
- ArrayList : 클래스 ( 정사각형 )

### List
```java
List<Integer> list = new ArrayList<Integer>();

list = new LinkedList<Integer>(); // 요구사항 변경 등의 이유로 구현체가 바뀌어도 호환 가능
```

### ArrayList
- 클래스이므로 자료형으로 생성한 경우  LinkedList로 새롭게 구현체를 만들거나 형변환을 할 수 없다.

```java
public class ArrayList<E> extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable

ArrayList<Integer> list = new ArrayList<Integer>();
list = new LinkedList<Integer>(); // error 발생

```

