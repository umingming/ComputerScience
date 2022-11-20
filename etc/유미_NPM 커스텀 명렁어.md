# NPM

## 커스텀 명령어

22/11/20

📎 NPM 커스텀 명령어

- 사용자가 임의로 명령어의 이름과 동작을 정의해서 사용할 수 있는 기능을 의미
- NPM 패키지 관리 파일인 `package.json`에 `scripts` 속성 추가
    
    ```json
    "scripts": {
    	"hello": "echo hi"
    }
    ```
    
- 명령어 실행 창에 긴 명령어를 입력할 필요 없이 커스텀 명령어 이용해 원하는 동작 실행
    
    ```bash
    npm run hello
    ```
    
- test, start 명령어는 run 없이 실행할 수 있음.
    
    ```bash
    npm test
    npm start
    ```
    

📎 Node.js 적용

- 서버를 실행하는 명령어
    
    ```bash
    node server.js
    ```
    
- 웹팩으로 빌드하는 명령어
    
    ```bash
    webpack --mode=none
    ```
    
- 커스텀 명령어 정의
    
    ```json
    "scripts": {
      "dev": "node server.js",
      "build": "webpack --mode=none",
    }
    ```
    
- 사용자는 이를 간단하게 입력할 수 있음.
    
    ```bash
    npm run dev
    npm run build
    ```
    
- 명령어가 길 수록 더 유용함.
    
    ```json
    "scripts": {
    	"build": "cross-env NODE_ENV=production webpack --progress --hide-modules"
    }
    ```
    

📎 실전 활용

- 다른 커스텀 명령어를 조합할 수 있음.
    
    ```json
    "scripts": {
      "build": "webpack",
      "deploy": "npm run build -- --mode production"
    }
    ```
    
- 명령어가 길수록 더 유용함.
    
    ```bash
    npm run deploy
    ```