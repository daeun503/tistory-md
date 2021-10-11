https://zerozero7bang.tistory.com/7



# [JavaScript] Axios.all 사용법

[Axios](https://github.com/axios/axios)는 브라우저, Node.js를 위한[Promise API](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)를 활용하는 HTTP 비동기 통신 라이브러리이다. 엊그제까지 원래 보던 러닝 가이드 번역이 있었는데(이듬님?) 오늘 작성하려고 보니 터진건지 사라졌다. 대신 다른 분의 러닝 가이드를 찾았다. 내용은 같은 듯

-   axios 러닝 가이드 번역 [https://yamoo9.github.io/axios/](https://yamoo9.github.io/axios/) 
-   axios 멀티 요청 [https://yamoo9.github.io/axios/guide/usage.html#post-%EC%9A%94%EC%B2%AD](https://yamoo9.github.io/axios/guide/usage.html#post-%EC%9A%94%EC%B2%AD)

<br/>

<br/>

### axios.all 사용법

**여러 개의 요청을 동시에 수행할 경우** axios.all() 메서드를 사용한다. 여러 개의 axios 요청이 필요할 때 **forEach문**을 사용해도 되지만 결과가 오는 타이밍도 다르고, 요청의 완료 시점을 알 수 없는 단점이 있다. 그럴 때 사용하면 좋다. 또, 당연하지만 axios.all에서 첫 번째 요청의 결과를 두 번째 요청에서 사용할 수는 없다. 동기 처리를 할거면 .then이나 await/async 를 사용해야 한다. 

```javascript
// 러닝 가이드 번역
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // Both requests are now complete
  }));
```

<br/>

나는 email, nickname 중복 체크할 때 사용했다. 러닝 가이드처럼 return 으로 써도 되고, 풀어서 써도 되고.

```javascript
// user/emailck 으로 post 요청 보내서 res1을 결과로 받고,
// user/nicknameck 으로 post 요청 보내서 res2를 결과로 받는다.
axios.all([axios.post('user/emailck', this.credentials), axios.post('user/nicknameck', this.credentials)])
  .then(axios.spread((res1, res2) => {
    ...
    // user/emailck의 post 요청의 결과 res1
    // user/nicknameck의 post 요청 결과 res2
}))
```

