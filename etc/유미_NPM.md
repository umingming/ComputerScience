# NPM

## Node.js

22/11/06

📎 Node.js

- 브라우저 밖에서도 자바스크립트를 실행할 수 있는 환경
- 버전 확인; node -v
    
    ![Untitled](NPM%201c043629ba804a43bf1b66ae369616dd/Untitled.png)
    

📎 Node.js 맛보기

- js 파일에서 내용 추가
    
    ```jsx
    console.log('hi');
    ```
    
- 명령어 입력으로 텍스트 출력 확인
    
    ```bash
    node app.js
    ```
    

📎 NPM

- **자바스크립트 라이브러리**를 설치하고 관리할 수 있는 패키지 매니저
- 라이브러리를 명령어로 편하게 다운로드 받을 수 있음.
- node.js 설치하면 같이 설치됨.

📎 NPM 미사용

- 필요한 라이브러리를 html 태그 주변에 선언해줘야 하며, 버전이 변경된 경우 연관 라이브러리의 버전을 수정해야 함.
    
    ```html
    <script src="https://jquery/jquery.v4.js"></script>
    <script src="https://jquery-ui.com/data-picker-v2.js"></script>
    <div class="data-picker"></div>
    ```
    
- CDN 검색하는데 시간이 들고 번거로움.
    
    ![Untitled](NPM%201c043629ba804a43bf1b66ae369616dd/Untitled%201.png)
    

📎 NPM 사용

- `npm init -y` 로 package.json 파일을 생성하면 라이브러리 정보를 쉽게 확인/변경 가능
    
    ![Untitled](NPM%201c043629ba804a43bf1b66ae369616dd/Untitled%202.png)
    
- 필요한 라이브러리를 `npm install`로 추가할 수 있음.
    
    ![node_modules에 하위 폴더 생김.](NPM%201c043629ba804a43bf1b66ae369616dd/Untitled%203.png)
    
    node_modules에 하위 폴더 생김.
    

## npm install

📎 NPM 명령어

- 지역 설치(install); node_modules 폴더 하위에 해당 라이브러리 파일 설치
    
    ```bash
    npm install gulp
    npm i gulp
    ```
    
- 전역 설치(global); 프로젝트가 아닌 시스템 레벨에서 사용할 라이브러리 설치
    
    ```bash
    npm install gulp --global
    npm i gulp -g
    ```
    
- 제거; uninstall
    
    ```bash
    npm uninstall gulp
    ```
    

📎 NPM 지역 설치 옵션

- dependencies; DOM 조작을 도와주며 화면 로직과 직접적인 연관있는 배포용 라이브러리 ex) react, angular, vue
    - npm run build로 최종 코드 안에 포함됨.
    
    ```bash
    npm install gulp --save-prod
    npm i gulp
    ```
    
- devDependencies; 개발용 라이브러리로 어플리케이션 배포 시, 코드에 포함되지 않음. ex) webpack, js-compression, eslint, imagemin
    
    ```bash
    npm install gulp --save-dev
    npm i gulp -D
    ```