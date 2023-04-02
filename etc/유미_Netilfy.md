# Netilfy

## 배포하기

23/03/05

📎 Netlify [링크](https://app.netlify.com/) 

- Site에서 Git 레퍼지토리를 import 함.
    
    ![Untitled](Netilfy%20f2a64cbead1f4b9691be6fab4359ebf0/Untitled.png)
    
- GitHub 연결
    
    ![Untitled](Netilfy%20f2a64cbead1f4b9691be6fab4359ebf0/Untitled%201.png)
    
- 경로 및 build 입력
    
    ![Untitled](Netilfy%20f2a64cbead1f4b9691be6fab4359ebf0/Untitled%202.png)
    
- Build 중인 것을 확인할 수 있음.
    
    ![Untitled](Netilfy%20f2a64cbead1f4b9691be6fab4359ebf0/Untitled%203.png)
    
- 빌드 완료된 사이트 열기
    
    ![Untitled](Netilfy%20f2a64cbead1f4b9691be6fab4359ebf0/Untitled%204.png)
    

📎 라우터 설정

- 기본으로 build하면 url로 접근 시 에러 발생
    
    ![Untitled](Netilfy%20f2a64cbead1f4b9691be6fab4359ebf0/Untitled%205.png)
    
- public에 하위 파일 `_redirects` 생성해야 됨.
    
    ![Untitled](Netilfy%20f2a64cbead1f4b9691be6fab4359ebf0/Untitled%206.png)
    
- 경로 설정하는 내용 기입 [참고](https://cli.vuejs.org/guide/deployment.html#netlify)
    
    ```xml
    # Netlify settings for single-page application
    /*    /index.html   200
    ```