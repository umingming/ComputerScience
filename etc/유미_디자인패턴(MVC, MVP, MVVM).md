# 디자인패턴

## MVC

22/08/14

📎 MVC 구조

- Model; 데이터와 그 데이터를 처리하는 부분
- View; 사용자에게 보여지는 UI
- Controller; 사용자의 Action을 받고 처리

![Untitled](%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%203e6b7e0896d04503b4c09f304748bcb5/Untitled.png)

📎 MVC 동작

1️⃣ 사용자의 Action이 Controller에 들어오게 됨.

2️⃣ Controller는 사용자의 Action을 확인하고, Model을 업데이트함.

3️⃣ Controller는 Model을 나타내줄 View를 선택

4️⃣ View는 Model을 이용하여 화면을 나타냄.

📎 장점

- 가장 단순함.
- 보편적으로 많이 사용됨.

📎 단점

- View와 Model 사이 의존성 높음.
- 유지보수 어려움.

## MVP

📎 MVP 패턴

- Model + View + Presenter로, MVC에서 파생
- Presenter; View에서 요청한 정보로 Model을 가공하여 View에 전달해주는 부분
- 여러 개의 View를 선택할 수 있는 Controller와 달리 Presenter와 View는 1:1관계

![Untitled](%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%203e6b7e0896d04503b4c09f304748bcb5/Untitled%201.png)

📎 MVP 동작

1️⃣ 사용자의 Action은 View를 통해 들어옴.

2️⃣ View는 데이터를 Presenter에 요청

3️⃣ Presenter는 Model에게 데이터 요청

4️⃣ Model은 Presenter가 요청한 데이터에 대해 응답함.

5️⃣ Presenter는 View에게 데이터를 응답함.

6️⃣ View는 Presenter가 응답한 데이터를 이용하여 화면을 나타냄.

📎 장점

- View와 Model 사이 의존성 해결

📎 단점

- View와 Presenter의 높은 의존성

## MVVM

📎 MVVM 패턴

- Model + View + View Model로, MVC에서 파생
- View Model; View를 표현하기 위해 만든 Model로, 데이터 처리 담당
- Command 패턴과 Data Binding 패턴 사용하여 구현

![Untitled](%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%203e6b7e0896d04503b4c09f304748bcb5/Untitled%202.png)

📎 **Command** 패턴

- 요청을 객체의 형태로 캡슐화하여 재사용성 증대
- 여러 객체들에서 발생하는 일들을 일괄적으로 Command에서 처리
- 정의한 클래스가 함수를 인자로 받을 수 있음.

📎 MVVM 동작

1️⃣ 사용자의 Action은 View를 통해 들어옴.

2️⃣ View는 Command 패턴으로 View Model에 Action을 전달

3️⃣ View Model은 Model에게 데이터 요청

4️⃣ Model은 View Model이 요청한 데이터에 대해 응답함.

5️⃣ View Model은 데이터를 가공하여 저장

6️⃣ View는 View Model과 Data Binding하여 화면을 나타냄.

📎 장점

- View와 Model 사이 의존성이 없음.
- View와 View Model 사이 의존성 없음.

📎 단점

- View Model의 설계가 어려움.