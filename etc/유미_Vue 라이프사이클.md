# Vue 라이프사이클

## 인스턴스란?

22/09/18

📎인스턴스

- 뷰로 개발할 때 필수로 생성해야 하는 코드이자 단위
- **인스턴스** 생성; 기본적으로 Root 컴포넌트가 됨.
    
    ```jsx
    new Vue();
    ```
    

📎 인스턴스 사용

- html 내에 `div` 태그 선언
    
    ```html
    <div id="app"> {{ message }} </div> 
    ```
    
- 스크립트 소스 설정
    
    ```html
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    ```
    
- 스크립트 내에서 인스턴스 생성
    
    ```jsx
    var vm = new Vue();
    ```
    
- el 속성에 태그 지정해주고, 메시지 입력함.
    
    ```jsx
    var vm = new Vue({
        el: '#app',
        data: {
            message: 'hi'
        }
    });
    ```
    
- vue 개발자 도구에서 확인할 수 있음.
    
    ![Untitled](Vue%20%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%91%E1%85%B3%E1%84%89%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8F%E1%85%B3%E1%86%AF%20317c04cd34f8490380eecb83463f9ac5/Untitled.png)
    

📎 인스턴스 속성

```jsx
new Vue({
    el: '#app',
    data: {
        message: 'hi'
    },
    methods: {
    },
});
```

- `el`; 인스턴스가 그려지는 화면의 시작점(특정 HTML 태그), body에서 element를 찾아 인스턴스와 연결함.
- `data`; 뷰의 반응성(Reactivity)가 반영된 데이터 속성
- `methods`; 화면의 동작과 이벤트 로직을 제어하는 메소드

📎 라이프사이클

- create; 인스턴스가 생성되고 reactivity 구현
    - reactivity; 뷰의 핵심으로, **데이터의 변화**를 라이브러리에서 감지해서 알아서 **화면**을 자동 **구현**해주는 것
- mount; 생성된 인스턴스가 DOM에 부착되는 것
- update; 데이터 변화 시, Virtual DOM이 리렌더링 되는 것
- destroy; 마지막 과정으로, 인스턴스가 없어지는 것

## 라이프사이클 속성

📎 beforeCreate

```jsx
var app = new Vue({
    el: '#app',
    data() {
        return {
            msg: 'hello';
        }
    },
    beforeCreate(function() {
        console.log(this.msg); // undefined
    })
})
```

- 가장 먼저 실행되며, Vue 인스턴스가 초기화 된 직후 발생
- el, data, methods에 접근할 수 없음.

📎 created

```jsx
var app = new Vue({
    el: '#app',
    data() {
        return {
            msg: 'hello';
        }
    },
    created(function() {
        console.log(this.msg); // hello
    })
})
```

- data를 반응형으로 추적할 수 있게 되며, computed/methods/watch 활성화
- 이벤트 리스너 선언할 경우 이 단계에서 하는 것이 가장 적절함.

📎 beforeMount

```jsx
var app = new Vue({
    el: '#app',
    beforeMount(function() {
        console.log('beforeMount');
    })
})
```

- 템플릿 렌더링 후, 가상 DOM이 생성되어 있으나 실제 DOM에 부착되지는 않은 상태

📎 mounted

```jsx
var app = new Vue({
    el: '#app',
    data() {
        return {
            msg: 'hello';
        }
    },
    mounted(function() {
				this.msg = 
        console.log('mounted');
    })
})
```

- 가상 DOM의 내용이 실제 DOM에 부착되고 난 이후 실행
- el, data, computed, methods, watch 등 모든 요소에 접근 가능
- 부모와 자식 간 순서; parent created → child created → child mounted → parent mounted

📎 beforeUpdate

```jsx
var app = new Vue({
    el: '#app',
    data() {
        return {
            msg: 'hello';
        }
    },
    beforeUpdate(function() {
				this.msg = "HELLO2";
        console.log('beforeUpdate');
    })
})
```

- data 값이 변해서 DOM에 그 변화를 적용시켜야 할 경우 변화 직전 호출되는 것
- 가상 DOM을 렌더링하기 전이지만, 이 값을 이용해 작업 가능
- 값을 추가적으로 변화시키더라도 랜더링 추가 호출하지 않음.

📎 updated

```jsx
var app = new Vue({
    el: '#app',
    beforeUpdate(function() {
				this.msg = "HELLO2";
        console.log('beforeUpdate');
    })
    updated(function() {
        console.log(this.msg);  //HELLO2
				this.msg = hello3;
    })
})
```

- 실제 DOM이 변경된 이후 호출되며, 변경된 data가 DOM에도 적용된 상태
- 데이터를 직접 변경할 경우 무한 루프 가능성이 있어 직접 바꾸어서는 안 됨.

📎 beforeDestroy

```jsx
var app = new Vue({
    el: '#app',
    beforeDestroy(function() {
        console.log('beforeDestroy');
    })
})
```

- 해당 인스턴스 해체되기 직전에 호출되는 훅으로 인스턴스는 완전하므로 모든 속성에 접근 가능
- 이벤트 리스너를 해제하는 등 인스턴스가 사라지기 전에 해야할 일들을 처리

📎 destroyed

```jsx
var app = new Vue({
    el: '#app',
    data() {
        return {
            msg: 'hello';
        }
    },
    destroyed(function() {
        console.log(this.msg);  //undefined;
    })
})
```

- 인스턴스가 해체되고 난 직후 호출되어, 모든 인스턴스 속성에 접근할 수 없음.
- 하위 인스턴스 역시 삭제