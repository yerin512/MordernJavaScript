
[Hello, world](https://ko.javascript.info/hello-world)

# Hello, world!

이 파트는 실행 환경에 독립적인 코어 자바스크립를 다룸.

코어 자바스크립트를 다루고 있긴하지만, 학습을 위해선 스크립트를 실행할 수 있는 환경이 필요함.

웹 페이지에 스크립트를 삽입하는 방법에 대해 알아보자.
참고로 Node.js와 같은 서버 사이드 환경에서 스크립트를 실행하고 싶다면 'node my.js'와 같은 명령어를 사용하면 된다.


## script 태그


`<script>` 태그를 이용하면 자바스크립트 프로그램을 HTML 문서 대부분의 위치에 삽입할 수 있음.
  

```js
<!DOCTYPE HTML>
<html>

<body>

  <p>스크립트 전</p>

  <script>
    alert( 'Hello, world!' );
  </script>

  <p>스크립트 후</p>

</body>

</html>
```

`<script>` 태그엔 자바스크립트 코드가 들어감. 브라우저는 이 태그를 만나면 안의 코드를 자동으로 처리함.


## 모던 마크업

`<script>` 태그엔 몇 가지 속성(attribute)이 있음. 요즘엔 잘 사용 안 하지만 에전 코드에선 발견할 수 있음..

```

type 속성: <script type=…>

HTML4에선 스크립트에 type을 명시하는 것이 필수였음. 이젠 명시가 필수가 아님.
그리고 모던 HTML 표준에서


language 속성: <script language=…>

이 속성은 현재 사용하고 있는 스크립트 언어를 나타냄. 지금은 자스가 기본 언어이므로 속성의 의미가 퇴색된 상황. 더는 사용할 필요 없음.


```




