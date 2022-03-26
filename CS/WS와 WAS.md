# WS와 WAS 



## Web Server (WS) 란

**Web Server란 웹 브라우저로부터 HTTP 요청을 받아들이고 HTML 따위를 반환해주는 프로그램**을 말한다. 이미지, CSS, JavaScript를 포함한 HTML 문서가 클라이언트로 전달된다. Apache, nginx가 Web Server의 예시이다. 추가적으로, Web Server가 하드웨어적인 의미로 사용될 때는 Web Server가 설치되어 있는 컴퓨터 그 자체를 말한다.

WAS와 비교할 때 주로 "HTTP 요청이 오면, 정적 콘텐츠만 요구하면 WS에서 처리하고 동적 콘텐츠를 요구하면 WAS까지 가서 처리하여 자원을 제공한다" 처럼 비교한다. 그 이외에 다음과 같은 기능들도 제공한다.

- **서버 부하 방지** : 정적 콘텐츠는 Web Server, 동적 콘텐츠는 WAS 담당하여 부하를 분산
  - 정적 콘텐츠 제공 : WAS 서버를 거치지 않고 바로 자원(html, css, javascript, img 등)을 전달한다. 
  - 동적 콘텐츠 제공 : WAS 서버를 거쳐서 동적 콘텐츠를 만들어 자원을 전달한다. 
- Load Balancing : WAS의 일을 여러 대의 WAS가 나누어 처리하도록 설정 가능, 무중단 운영
- 보안 강화 : SSL 보안, Web Server를 WAS 앞 단에 둠으로써 WAS의 설정 파일을 숨김
- Health check : 서버에 주기적으로 HTTP 요청을 보내 서버의 상태 확인



<img src="WS와 WAS.assets/image-20220326205319305.png" alt="image-20220326205319305" style="zoom: 50%;" />

<br/>

## Web Applicaition Server (WAS) 란

WAS는 인터넷 상에서 HTTP를 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어로 볼 수 있다. **WAS 서버는 동적 서버 콘텐츠를 수행하는 것으로 일반적인 WS와 구별되며 주로 DB 서버와 같이 수행된다.** WS의 기능들을 구조적으로 분리하여 처리하고자 하는 목적으로 제시되었다.

웹 애플리케이션 서버의 기본 기능은 다음 3가지이다.

- 프로그램 실행 환경과 DB 접속 기능을 제공한다.
- 여러 개의 트랜잭션을 관리한다.
- 업무를 처리하는 비즈니스 로직을 수행한다.

<br/>

## WS or WAS만 쓰면 안 되나요

하나만 써도 된다. 꼭 저 둘을 같이 쓸 필요는 없다. WS에 모듈을 설치해서 동적 처리를 할 수도 있고, WAS가 정적 자원을 처리 해도 된다. 그럼에도 둘을 나눠 쓰는 이유는 그것이 더 효율적이기 때문이다.



**WAS는 기본적으로 동적 콘텐츠를 수행하고자 만들어졌는데, 정적 콘텐츠 요청까지 직접 처리하게 된다면 서버의 부하가 커질 것이다.** 그러니 단순한 정적 콘텐츠는 WS에서 빠르게 처리하고 복잡한 비즈니스 로직을 WAS에서 처리하는 것이다. 

클라이언트에 이미지 파일을 보내는 과정을 생각해보면, 이미지 같은 정적 파일은 HTML과 함께 가는 것이 아니다. 클라이언트는 HTML파일을 먼저 받고 필요한 이미지 파일 같은 것을 다시 서버로 요청하면 그때서야 받는다. 그러한 파일 요청을 WAS까지 가지 않고 WS에서 해줄 수 있는 것이다.



WS는 WAS보다 더 가볍고, 서버 부하 방지 이외에 Load Balancing, 보안 강화 등 더 다양한 기능을 제공하기도 한다. 그래서 보통 **WS - WAS - DB 구조의 3 Tier 구조로 개발**을 진행한다.

Presentation Tier를 클라이언트(사용자 화면)으로 두고 Logic Tier에 WS + WAS로 보거나, 이들을 모두 나눠 4 Tier로 보는 경우도 있긴 하다. 하지만 WS + WAS를 뭉쳐서 보면 한 쪽이 다운됐을 때 다른 쪽에 영향을 주기 때문에 WS - WAS - DB 구조로 보는 것이 합당할 것 같다.

![image-20220326221813910](WS와 WAS.assets/image-20220326221813910.png)



## 참고자료

- [[Web] Web Server와 WAS의 차이와 웹 서비스 구조](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)
- [[10분 테코톡] 👳‍♂️ 알리의 Web Server vs WAS](https://www.youtube.com/watch?v=mcnJcjbfjrs&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9CTech)
- [3계층 (3 tier) 구조](https://dbknowledge.tistory.com/78)
