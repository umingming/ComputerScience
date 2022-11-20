# LinkedList

## LinkedList의 특징

                                                                                                                                                      22/11/20

📎 LinkedList란?

- 컴퓨터의 자료를 저장하는 구조 중 하나로써 일렬로 연결된 데이터를 이용할 때 사용한다.
- 데이터에 다음 데이터의 주소를 가지고 있다.

![Untitled](LinkedList%206389f26795804dbab2633f4236cf0fcc/Untitled.png)

📎 배열과의 차이

- 배열은 배열의 주소가 물리적으로 정해져있다.
- 따라서 길이를 늘리거나 줄일수가 없다.

![Untitled](LinkedList%206389f26795804dbab2633f4236cf0fcc/Untitled%201.png)

- 그러나 Linked List는 값이 추가될 시 Node가 가르키는 위치만 바꿔주면 된다.

![Untitled](LinkedList%206389f26795804dbab2633f4236cf0fcc/Untitled%202.png)

- 반대로 빼고 싶을때는 내 앞의 Node에게 주소를 주면 된다.

![Untitled](LinkedList%206389f26795804dbab2633f4236cf0fcc/Untitled%203.png)

<aside>
💡 우리가 사용하는 언어 기준으로는 Node 연관관계에서 제외된 데이터는 GC가 알아서 수거한다.
C나 C++을 사용할 경우 메모리를 삭제해줘야 한다.

</aside>

📎LinkedList의 특징

- 주소를 일일이 찾아다녀야 하기 때문에 배열보다 속도가 느릴 수 있다.
- 그러나 삽입과 삭제등과 같은것을 배열로 구현할 시 Node가 하나 추가될 때마다 배열을 다시 만들어준 후 복사해줘야 하는 수고로움이 있다.

구현해보기

```java
package datastruct.linkedList;

/*
* 1. static class로 Node를 선언한다.
*   1.1. Node의 필드 변수는 Object 자료형의 data와 next라는 Node 객체가 있다.
* 2. MyLinkedList의 필드 변수인 Node 객체의 header를 선언한다.
* 3. 생성자로 header를 인스턴스화 해준다.
* 4. append 메소드
*   4.1. 매개변수는 Object data이다.
*   4.2. Node 객체의 end라는 변수를 선언한다. 해당 객체의 data 프로퍼티에 파라미터 data를 할당한다.
*   4.3. Node n = header이다.
*   4.4. while문을 돌면서 n.next가 null이 아니라면 n=n.next처리를 해준다.
*   4.5. while문이 다 끝났으면 마지막 노드의 바로 앞 노드에 정지하므로 n.next = end로 값을 할당해준다.
* 5. delete 메소드
*   5.1. 매개변수는 Object data이다.
*   5.2. Node n = header.next로 할당해준다.
*       * header는 지워지면 안되는 기준값이기 때문이다.
*   5.3. while문을 돌면서 n.next != null로 끝까지 돌아준다.
*       5.3.1. while문 내에서 조건문을 분기해주고 만약 n.next.data가 data가 아니라면 n.next = n.next.next이다.
*       5.3.2. 아니라면 (else) n = n.next이다.
* 6. retrieve 메소드
*   6.1. 돌면서 뿌려준다.
*/
public class LinkedList {

    Node header;

    static class Node {
        Object data;
        Node next = null;
    }

    LinkedList() {
        header = new Node();
    }

    public void append(Object data) {
        Node end = new Node();
        end.data = data;

        Node n = header;

        while(n.next != null) {
            n = n.next;
        }
        n.next = end;
    }

    public void delete(Object data) {
        Node n = header;
        while(n.next != null) {
            if (n.next.data == data) {
                n.next = n.next.next;
            } else {
                n = n.next;
            }
        }
    }

    public void retrieve() {
        Node n = header.next;

        while(n.next != null) {
            System.out.println(n.data);
            n = n.next;
        }

        System.out.println(n.data);
    }

    public static void main(String[] args) {

        LinkedList temp = new LinkedList();
        temp.append(1);
        temp.append(2);
        temp.append(3);
        temp.append(4);
        temp.delete(2);

        temp.retrieve();

    }
}
```