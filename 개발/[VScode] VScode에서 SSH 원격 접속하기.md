# [VScode] VScode에서 SSH 원격 접속하기

VScode에서도 SSH를 이용해 원격 서버에 접속할 수 있습니다.



<img src="[VScode] VScode에서 SSH 원격 접속하기.assets/image-20220225111744527.png" alt="image-20220225111744527" style="zoom:80%;" />

`Extension` 에서 `Remote Development` 를 설치합니다.



<img src="[VScode] VScode에서 SSH 원격 접속하기.assets/image-20220225113029219.png" alt="image-20220225113029219" style="zoom:80%;" />

`F1`을 누르고 ssh를 입력하여 `Remote-SSH: Connect to Host...` 를 찾아 클릭합니다.



<img src="[VScode] VScode에서 SSH 원격 접속하기.assets/image-20220225113014330.png" alt="image-20220225113014330" style="zoom:80%;" />

`Configure SSH Hosts...`를 클릭합니다. 위에 server, test는 기존에 제가 미리 만들어둔 것 입니다.

`C:\Users\사용자명\.ssh\config`를 클릭합니다.

<img src="[VScode] VScode에서 SSH 원격 접속하기.assets/image-20220225122331561.png" alt="image-20220225122331561" style="zoom:80%;" />

```
Host <서버 별명>
    HostName <서버 IP주소>
    User <사용자명>
    IdentityFile <Pem키 경로>
```

그럼 config 폴더가 열리는데, 위와 같은 형태로 작성하고 저장해줍니다.



<img src="[VScode] VScode에서 SSH 원격 접속하기.assets/image-20220225122526829.png" alt="image-20220225122526829" style="zoom:80%;" />

다시 `F1` - `Remote-SSH: Connect to Host...` 을 누르면 config 파일에서 작성한 서버 별명들이 나타납니다.

연결할 서버를 선택하면 새로운 창이 열립니다. `Linux` 와 `continue`를 순서대로 클릭하면 연결이 완료됩니다.

<img src="[VScode] VScode에서 SSH 원격 접속하기.assets/image-20220225122831915.png" alt="image-20220225122831915" style="zoom:80%;" />

좌측 하단에 SSH:test로 연결된 것을 확인할 수 있으며 사이드 바 버튼을 눌러 탐색할 수 있습니다.



VScode로 원격 접속을 하면 vim으로 파일을 열지 않아도 눈으로 쉽게 코드를 확인할 수 있습니다.

하지만 파일 업로드/수정 시엔 권한이 따로 필요할 수 있습니다.

