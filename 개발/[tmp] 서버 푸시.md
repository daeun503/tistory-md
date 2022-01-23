# 서버 푸시 (Server Push)

## 서버 푸시

푸시 기법은 정보를 가지고 있는 웹 사이트에서 사용자에게 원하는 정보를 밀어내 준다(Push)는 의미로, 인터넷 상에서 **어떤 전송 요청이 중앙 서버에서 시작되는 정보 전달 방식**입니다. 클라이언트가 요청을 할 때에만 응답을 주는 풀 기법과는 정 반대입니다.

푸시 기법은 매일 아침 우유나 신문이 집 앞에 배달되듯 이미 등록돼있는 서버에서 원하는 시간에 원하는 내용을 클라이언트의 PC, 모바일 기기 등에 정기적으로 배달되도록 하는 방식입니다. 서버 푸시를 구현하기 위한 전통적인 방법으로는 Polling, Long Polling, Streaming 기법이 있으며 요즘은 WebSocket을 사용합니다. 웹 소켓을 포함하여 해당 기법들은 여기서 간략히 소개합니다.

이 게시글에서는 FCM, SSE에 대해서 이야기합니다.

<br/>

## SSE (Server Sent Events)

웹 소켓이 서버와 클라이언트 사이의 양방향 통신이라면, SSE는 **서버에서 클라이언트로의 단방향 통신**입니다. 

SSE는 클라이언트에서 데이터를 전송하지 않고, 뉴스 피드처럼 서버에서만 데이터를 전송할 때 유용하게 사용될 수 있습니다. 클라이언트에서 서버로 데이터를 전송하고 싶을 때는 Ajax를 활용합니다.

SSE의 장점은 다음과 같습니다.

- HTTP5 웹 표준으로 어느 정도 웹 소켓의 역할을 하면서 더 가볍습니다.
- HTTP를 통해 통신하므로 특별한 프로토콜이나 서버 구현이 필요 없습니다.
- 접속에 문제가 있으면 자동으로 재연결을 시도합니다.
- IE제외 대부분의 브라우저에서 지원되며, IE역시 polyfill을 통해 지원 가능합니다.

<br/>

## FCM (Firebase Cloud Messaging)

Firebase Cloud Messaging(FCM)은 **무료로 메시지를 안정적으로 전송할 수 있는 교차 플랫폼 메시징 솔루션**입니다. 교차 플랫폼 메시징 솔루션이기 때문에 FCM을 이용하여 개발을 하면 안드로이드, iOS, Mobile Web 등 플랫폼에 종속되지 않고 메시지를 보낼 수 있습니다. 주요 기능은 다음과 같습니다.

- 사용자에게 표시되는 알림 메시지를 전송합니다. 또는 데이터 메시지를 전송하고 애플리케이션 코드에서 임의로 처리합니다. 자세한 내용은 [메시지 유형](https://firebase.google.com/docs/cloud-messaging/concept-options?hl=ko#notifications_and_data_messages)을 참조하세요.
- 단일 기기, 기기 그룹, 주제를 구독한 기기 등 3가지 방식으로 클라이언트 앱에 메시지를 배포할 수 있습니다.
- FCM의 신뢰성 높고 배터리 효율적인 연결 채널을 통해 기기에서 다시 서버로 확인, 채팅, 기타 메시지를 보낼 수 있습니다.



![이 페이지에 설명된 세 가지 아키텍처 레이어의 다이어그램](https://firebase.google.com/docs/cloud-messaging/images/diagram-FCM.png?hl=ko)

1. 메시지 요청을 작성하거나 구현하는 도구입니다. 알림 작성기는 알림 요청을 만들기 위한 GUI 기반 옵션을 제공합니다. 모든 [메시지 유형](https://firebase.google.com/docs/cloud-messaging/concept-options?hl=ko#notifications_and_data_messages)을 완벽하게 자동화하고 지원하려면 Firebase Admin SDK 또는 FCM 서버 프로토콜을 지원하는 신뢰할 수 있는 [서버 환경](https://firebase.google.com/docs/cloud-messaging/server?hl=ko)에서 메시지 요청을 구현해야 합니다. 이 환경은 Firebase용 Cloud Functions, App Engine 또는 자체 앱 서버일 수 있습니다.
2. FCM 백엔드는 다른 여러 기능 중에서 메시지 요청을 수락하고, 주제를 통해 메시지를 확장하고, 메시지 ID와 같은 메시지 메타데이터를 생성합니다.
3. 기기로 타겟팅된 메시지를 라우팅하고, 메시지 전송을 처리하고, 필요한 경우 플랫폼별 구성을 적용하는 플랫폼 수준의 전송 레이어입니다. 이 전송 레이어에는 다음이 포함됩니다.
4. 알림이 표시되거나 앱의 포그라운드/백그라운드 상태 및 관련 애플리케이션 로직에 따라 메시지가 처리되는 사용자 기기의 FCM SDK입니다.

<br/>

## 참고자료

1. SSE
   - [[웹개발] SSE ( Server-Sent Events) 란 무엇인가](https://hamait.tistory.com/792)
   - [SSE를 이용한 실시간 웹앱](https://spoqa.github.io/2014/01/20/sse.html)
2. FCM
   - [Firebase 공식 문서](https://firebase.google.com/docs/cloud-messaging?hl=ko)
3. 기타
   - http://www.itdaily.kr
   - [Building with server-sent events with React and Node.js](https://dev.to/4shub/building-with-server-sent-events-13j)
   - [node.js, FCM, 웹앱(서비스워커) 으로 푸시 구현하기](https://medium.com/@sejongdekang/node-js-fcm-%EC%9B%B9%EC%95%B1-%EC%84%9C%EB%B9%84%EC%8A%A4%EC%9B%8C%EC%BB%A4-%EC%9C%BC%EB%A1%9C-%ED%91%B8%EC%8B%9C-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-43c49b761dba)
