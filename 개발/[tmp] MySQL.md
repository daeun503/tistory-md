# MySQL

## 1. 설치하기

1. [MySQL 홈페이지](https://downloads.mysql.com/archives/installer/)에 접속하여 다운로드 합니다.

   ![image-20220103150204105](MySQL.assets/image-20220103150204105.png)

2. 개발자 모드로 설치를 진행합니다.

   ![image-20220103150334045](MySQL.assets/image-20220103150334045.png)

3. 필요한 설치 요소들을 설치합니다. 그 후 next 버튼을 누릅니다.

   ![image-20220103150441668](MySQL.assets/image-20220103150441668.png)

4. 다음 설치 요소 또한 설치한 후, next 버튼을 누릅니다.

   ![image-20220103150714432](MySQL.assets/image-20220103150714432.png)

5. next 버튼을 누릅니다.

   ![image-20220103150913816](MySQL.assets/image-20220103150913816.png)

6. 포트 번호가 3306인 것을 기억하고 next 버튼을 누릅니다.

   ![image-20220103151000382](MySQL.assets/image-20220103151000382.png)

7. 비밀번호 작성 후, next 버튼을 누릅니다.

   ![image-20220103151139455](MySQL.assets/image-20220103151139455.png)

8. next 버튼을 누릅니다.

   ![image-20220103151228597](MySQL.assets/image-20220103151228597.png)

9. execute 버튼을 누릅니다.

   ![image-20220103151308482](MySQL.assets/image-20220103151308482.png)

10. finish 버튼을 누릅니다.

    ![image-20220103151415569](MySQL.assets/image-20220103151415569.png)

11. next 버튼을 누릅니다.

    ![image-20220103151508166](MySQL.assets/image-20220103151508166.png)

12. finish 버튼을 누릅니다.

    ![image-20220103151554074](MySQL.assets/image-20220103151554074.png)

13. next 버튼을 누릅니다.

    ![image-20220103151631012](MySQL.assets/image-20220103151631012.png)

14. 앞서 설정했던 비밀번호를 입력한 후, check를 누릅니다. 초록색 체크 표시가 뜨면 next를 누릅니다.

    ![image-20220103151741998](MySQL.assets/image-20220103151741998.png)

15. execute 버튼을 누릅니다.

    ![image-20220103151826101](MySQL.assets/image-20220103151826101.png)

16. finish 버튼을 누릅니다.

    ![image-20220103151907827](MySQL.assets/image-20220103151907827.png)

17. next 버튼을 누릅니다.

    ![image-20220103151939122](MySQL.assets/image-20220103151939122.png)

18. finish 버튼을 누릅니다.

    ![image-20220103152020774](MySQL.assets/image-20220103152020774.png)

19. workbench의 경우, MySQL connections에 있는 탭을 누르면 연결 창이 뜹니다. 기존에 설정했던 비밀번호를 입력하면 접속이 가능합니다.

    ![image-20220103152111332](MySQL.assets/image-20220103152111332.png)
    
20. cmd에서 MySQL을 사용하기 위해서는 환경 변수를 추가해야 합니다. 환경 변수 탭으로 접근하여 시스템 변수의 Path에 환경 변수를 추가하도록 합니다. 

    ![image-20220103163710439](MySQL.assets/image-20220103163710439.png)

21. 새로 만들기를 통해 새로운 환경 변수를 추가해줍니다. 경로를 따로 수정하지 않았다면 C:\Program Files\MySQL에 있습니다. 해당 폴더 안에 bin 파일, 즉 C:\Program Files\MySQL\MySQL Server (버전)\bin 을 Path에 추가해줍니다.

    ![image-20220103163858092](MySQL.assets/image-20220103163858092.png)

<br/>

# 참고 자료

- [﻿MySQL 다운로드 및 설치 방법](https://velog.io/@joajoa/MySQL-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-%EB%B0%8F-%EC%84%A4%EC%B9%98-%EB%B0%A9%EB%B2%95)
- [[mysql] MySQL 환경 변수 설정 방법 (윈도우 10 기준)](https://hoho325.tistory.com/163)
