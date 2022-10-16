# Jenkins

## Jenkins란?

                                                                                                                                                        22/10/09

📎 Jenkin란 무엇인가?

- 젠킨스는 소프트웨어 개발 시 지속적으로 통합 서비스를 제공하는 툴이다. CI(Continuous Integration) 툴 이라고 표현한다.다수의 개발자들이 하나의 프로그램을 개발할 때 버전 충돌을 방지하기 위해 각자 작업한 내용을 공유영역에 있는 저장소에 빈번히 업로드함으로써 지속적 통합이 가능하도록 해준다.원래 허드슨 프로젝트로 개발되었고, 허드슨의 개발은 2004년 여름 썬 마이크로시스템즈에서 시작되었다. 그리고 2005년 2월에 java.net에 처음 출시되었다.

📎 Jenkin가 주는 이점

- 개발중인 프로젝트에서 커밋은 매우 빈번히 일어나기 때문에 커밋 횟수만큼 빌드를 실행하는 것이 아니라 작업이 큐잉되어 자신이 실행될 차례를 기다리게 된다코드의 변경과 함께 이뤄지는 이 같은 자동화된 빌드와 테스트 작업들은 다음과 같은 이점들을 가져다 준다.
    - 프로젝트 표준 컴파일 환경에서의 컴파일 오류 검출
    - 자동화 테스트 수행
    - 정적 코드 분석에 의한 코딩 규약 준수여부 체크
    - 프로파일링 툴을 이용한 소스 변경에 따른 성능 변화 감시
    - 결합 테스트 환경에 대한 배포작업
    

<aside>
💡 이 외에도 젠킨스는 500여가지가 넘는 플러그인을 온라인으로 간단히 인스톨 할 수 있는 기능을 제공하고 있으며 파이썬과 같은 스크립트를 이용해 손쉽게 자신에게 필요한 기능을 추가 할 수도 있다.

</aside>

## 각종 배치 작업의 간략화

                                                                                                                                                        22/10/09

📎 어떻게?

- 프로젝트 기간 중에 개발자들은 순수한 개발 작업 이외에 DB셋업이나 환경설정, Deploy작업과 같은 단순 작업에 시간과 노력을 들이는 경우가 빈번하다.
- 데이터베이스의 구축, 어플리케이션 서버로의 Deploy, 라이브러리 릴리즈와 같이 이전에 CLI로 실행되던 작업들이 젠킨스 덕분에 웹 인터페이스로 손쉽게 가능해졌다.

## Build 자동화의 확립

                                                                                                                                                        22/10/09

📎 빌드 툴?

- 빌드 툴의 경우 Java는 maven과 gradle이 자리잡고 있으며, 이미 빌드 관리 툴을 이용해 프로젝트를 진행하고 있다면 젠킨스를 사용하지 않을 이유가 하나도 없다.
- 젠킨스와 연동하여 빌드 자동화를 통해 프로젝트 진행의 효율성을 높일 수 있다.

## 자동화 테스트

                                                                                                                                                        22/10/09

📎 자동화 테스트란

- 자동화 테스트는 젠킨스를 사용해야 하는 가장 큰 이유 중 하나이며, 사실상 자동화 테스트가 포함되지 않은 빌드는 CI자체가 불가능하다고 봐도 무방하다. 젠킨스는 Subversion이나 Git과 같은 버전관리시스템과 연동하여 코드 변경을 감지하고 자동화 테스트를 수행하기 때문에 만약 개인이 미처 실시하지 못한 테스트가 있다 하여도 든든한 안전망이 되어준다. 제대로 테스트를 거치지 않은 코드를 커밋하게 되면 화난 젠킨스를 만나게 된다.

## 빌드 파이프라인 구성

                                                                                                                                                        22/10/09

📎 파이프 라인?

- 2개 이상의 모듈로 구성되는 레이어드 아키텍처가 적용 된 프로젝트에는 그에 따는 빌드 파이프라인 구성이 필요하다. 예를 들면, 도메인 -> 서비스 -> UI와 같이 각 레이어의 참조 관계에 따라 순차적으로 빌드를 진행하지 않으면
- 안된다. 젠킨스에서는 이러한 빌드 파이프라인의 구성을 간단히 할 수 있으며, 스크립트를 통해서 매우 복잡한 제어까지도 가능하다.

```java
node {
  stage 'Setting'
  def javaHome = tool name: 'jdk8', type: 'hudson.model.JDK'
  env.JAVA_HOME = "${javaHome}"
  env.PATH = "${env.PATH}:${env.JAVA_HOME}/bin"

  // github에서 소스 얻어오기
  stage 'Checkout'
  git branch: 'master', credentialsId: 'Your Credentials ID', url: 'Your GitHub URL'

  // Maven으로 빌드 실행하기
  stage 'Build'
  def mvnHome = tool 'M3'
    sh "'${mvnHome}/bin/mvn' -Dmaven.test.skip=true clean install"
  // 패키지 저장
  step([$class: 'ArtifactArchiver', artifacts: '**/target/*.jar', fingerprint: true])
  
  // 서버실행 
  //stage 'Start'
    //sh "java -jar C:/ProgramData/Jenkins/.jenkins/workspace/test-pipeline/target/hr-0.0.1-SNAPSHOT.jar"
}
```

## 플러그인 종류

                                                                                                                                                        22/10/09

📎 대표적인 플러그인 5개를 알아보자

- Jira
    
    ![Untitled](Jenkins%202b451f8a0b8142c48e3ed7b5e3c923b9/Untitled.png)
    
    - 애자일 작업 추적 템플릿
    
    ![Untitled](Jenkins%202b451f8a0b8142c48e3ed7b5e3c923b9/Untitled%201.png)
    

- Github/GitLab CICD
- 퍼포먼스 플러그인
    - 말 그대로 퍼포먼스를 위한 것
    - 그래프, 보고서등을 제공한다
- 빌드 플러그인
- Job DSL
    - Jenkins에서 플러그인을 사용할 수 있다.
    -