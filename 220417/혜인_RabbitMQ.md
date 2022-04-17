# RabbitMQ

## 정의

- AMQP(Advanced Message Queing Protocol, MQ 표준 프로토콜)를 따르는 오픈소스 메세지 브로커
- 메세지를 많은 사용자에게 전달하거나, 요청에 대한 처리 시간이 길 때, 해당 요청을 다른 API에게 위임하고 빠른 응답을 할 때 많이 사용
- MQ를 사용하여 애플리케이션 간 결합도를 낮출 수 있음

## 핵심 개념

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5d99ef1-d7dc-4b71-b132-afdc7edd57b4/Untitled.png)

### Message

- 처리해야 할 내용이 담겨있음

### Producer

- 메시지를 생성하고 발송하는 주체
- producer가 발송한 메시지는 Queue에 저장되는데, produce는 queue에 직접 접근하지 않고, Exchange를 통해 접근함

### Consumer

- 메시지를 수신하는 주체
- Queue에 직접 접근하여 메시지를 가져옴

### Queue

- Producer들이 발송한 메시지들이 Consumer가 소비하기 전까지 보관되는 장소
- Queue는 이름으로 구분됨
    - 같은 이름과 같은 설정으로 Queue를 생성하면 에러 없이 기존 Queue에 연결됨
    - 같은 이름과 다른 설정으로 Queue를 생성하려고 시도하면 에러 발생

### Exchange

- Producer들에게서 전달받은 메시지들을 어떤 Queue들에게 발송할지를 결정하는 객체
- 일종의 라우터 개념
- Exchange의 네 가지 타입
    
    
    | 타입 | 설명 | 특징 |
    | --- | --- | --- |
    | Direct | Routing Key가 정확히 일치하는 Queue에 메시지 전송 | Unicast |
    | Topic | Routing Key 패턴이 일치하는 Queue에 메시지 전송 | Multicast |
    | Headers | [key:value]로 이루어진 header 값을 기준으로 일치하는 Queue에 메시지 전송 | Multicast |
    | Fanout | 해당 Exchange에 등록된 모든 Queue에 메시지 전송 | Broadcast |
    - Headers 타입의 경우, 모든 header가 일치할 때, 하나라도 일치할 때 메시지 전송등의 옵션을 줄 수 있다.

### Binding

- Exchange들에게 메시지를 라우팅 할 규칙을 지정하는 행위
- 특정 조건에 맞는 메시지를 특정 큐에 전송하도록 설정할 수 있는데, 이는 해당 Exchange 타입에 맞게 설정되어야 한다
- Exchange와 Queue는 m:n binding이 가능
