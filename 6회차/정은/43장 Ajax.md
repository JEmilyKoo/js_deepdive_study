# 43장 Ajax
## 43.1 Ajax란?
#### Ajax: Asyncronous Javascript and Xml
> 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 데이터를 동적으로 갱신하는 프로그래밍 방식
- 브라우저의 Web API인 XMLHttpRequest 객체를 기반으로 동작

#### XMLHttpRequest
> HTTP 비동기 통신을 위한 메서드와 프로퍼티

#### 전통적 방식의 단점
1. 불필요한 데이터 통신 발생 : 변경 없는 부분까지 포함한 완전한 HTML을 서버로부터 매번 다시 전송
2. 화면 전환하는 순간 깜빡임 : 전부 처음부터 다시 렌더링
3. 블로킹 : 동기 방식으로 동작해 서버로부터 응답이 있을 때까지 다음 처리 블로킹

#### Ajax의 장점
1. 필요한 데이터만 전송 받음 -> 불필요한 데이터 통신 발생 x 
2. 변경할 필요가 있는 곳만 렌더링 -> 화면 깜빡임 X
3. 비동기 방식 -> 블로킹 X

-> 브라우저에서도 데스크톱 애플리케이션과 유사한 빠른 퍼포먼스와 부드러운 화면 전환 가능해짐

## 43.2 JSON
#### JSON : JavaScript Object Notation
> 클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷.
- 자바스크립트에 종속 X -> 대부분의 프로그래밍 언어에서 사용 가능

### 43.2.1 JSON 표기 방식
#### JSON
- 자바 스크립트의 객체 리터럴과 유사
- 키와 값으로 구성된 순수한 텍스트
- 키는 반드시 큰따옴표 (작은 따옴표 사용 X)로 묶어야 함 
- 값은 객체 리터럴과 같은 표기법

```json
{
  "name": "Lee",
  "age": 20,
  "alive": true,
  "hobby": ["traveling", "tennis"]
}
```

### 43.2.2 JSON.stringify
- 객체를 JSON 포맷의 문자열로 변환

#### 직렬화
> 클라이언트가 서버로 객체를 전송하기 위해 객체를 문자열화하는 것

```javascript
const obj = {
  name: 'Lee',
  age: 20,
  alive: true,
  hobby: ['traveling', 'tennis']
};

const json = JSON.stringify(obj);
// string {"name":"Lee","age":20,"alive":true,"hobby":["traveling","tennis"]}

const prettyJson = JSON.stringify(obj, null, 2); // JSON 포맷 문자열로 변환, 들여쓰기 2칸
console.log(typeof prettyJson, prettyJson);
/*
string {
  "name": "Lee",
  "age": 20,
  "alive": true,
  "hobby": [
    "traveling",
    "tennis"
  ]
}
*/

// replacer 함수. 값의 타입이 Number이면 필터링되어 반환X
function filter(key, value) {
  // undefined: 반환하지 않음
  return typeof value === 'number' ? undefined : value;
}

// JSON.stringify 메서드에 두 번째 인수로 replacer 함수를 전달
const strFilteredObject = JSON.stringify(obj, filter, 2);
console.log(typeof strFilteredObject, strFilteredObject);
/*
string {
  "name": "Lee",
  "alive": true,
  "hobby": [
    "traveling",
    "tennis"
  ]
}
*/
```

- 배열도 JSON 포맷의 문자열로 변환함

### 43.2.3  JSON.parse
- JSON 포맷의 문자열을 객체로 변환

#### 역직렬화
> 서버로부터 클라이언트에게 전송된 JSON 데이터를 객체로 사용하기 위해 문자열을 객체화하는 것

```javascript
const todos = [
  { id: 1, content: 'HTML', completed: false }
];
const json = JSON.stringify(todos);
const parsed = JSON.parse(json); // JSON 포맷의 문자열을 배열로 변환. 배열의 요소까지 객체로.
```

## 43.3 XMLHttpRequest
- 브라우저는 주소창이나 HTML의 `<form>` 또는 `<a>`를 통해 HTTP 요청 전송 기능을 기본 제공
- 자바스크립트를 사용해 HTTP 요청을 전송하려면 `XMLHttpRequest` 객체를 사용
- HTTP 요청 전송과 HTTP 응답 수신을 위한 다양한 메서드와 프로퍼티 제공

### 43.3.1 XMLHttpRequest 객체 생성
- `XMLHttpRequest` 생성자 함수를 호출하여 생성
- 브라우저 환경에서만 정상적으로 실행

```javascript
const xhr = new XMLHttpRequest();
```

### 43.3.2 XMLHttpRequest 객체 프로퍼티와 메서드
#### XMLHttpRequest 객체의 프로토타입 프로퍼티
|프로토타입 프로퍼티|HTTP 요청|값|
|:---:|:---:|:---:|
|*readyState*|현재 상태:number||
||UNSENT|0|
||OPENED|1|
||HEADERS_RECEIVED|2|
||LOADING|3|
||DONE|4|
|*status*|응답 상태(HTTP 코드):number||
||정상|200|
||에러 발생|그 외|
|*statusText*|응답 메시지:string|ex)"OK"|
|*responseType*|응답 타입|ex) json, text, blob|
|*response*|응답 몸체. responseType에 따라 값 다름||
|responseText|서버가 전송한 응답 문자열||

#### XMLHttpRequest 객체의 이벤트 핸들러 프로퍼티
|이벤트 핸들러 프로퍼티|HTTP 요청에 대한 설명|
|:---:|:---:|
|*onreadystatechange*|readyState 프로퍼티 값이 변경됨|
|onloadstart|응답 받기 시작|
|onprogress|응답 받는 도중 주기적으로 발생|
|onabort|`abort` 메서드에 의해 중단|
|*onerror*|에러 발생|
|*onload*|성공적 완료|
|ontimeout|시간 초과|
|onloadend|모든 완료|

#### XMLHttpRequest 객체의 메서드
|메서드|설명|
|:---:|:---:|
|*open*|HTTP 요청 초기화|
|*send*|HTTP 요청 전송|
|*abort*|이미 전송된 HTTP 요청 중단|
|*setRequestHeader*|특정 HTTP 요청 헤더의 값을 설정|
|getResponseHeader|특정 HTTP 요청 헤더의 값을 문자열로 변환|

#### XMLHttpRequest 객체의 정적 프로퍼티
|정적 프로퍼티|값|설명|
|:---:|:---:|:---:|
|UNSENT|0|`open` 호출 이전|
|OPENED|1|`open` 호출 이후|

### 43.3.3 HTTP 요청 전송
1. XMLHttpRequest.prototype.`open`로 HTTP 요청 초기화
2. 필요에 따라 XMLHttpRequest.prototype.`setRequestHeader`로 특정 HTTP 요청의 헤더 값 설정
3. XMLHttpRequest.prototype.`send`로 HTTP 요청 전송
 
```
xhr.open('GET', '/users'); // HTTP 요청 초기화
xhr.setRequestHeader('content-type', 'application/json'); // HTTP 요청 헤더 설정
xhr.send(); // HTTP 요청 전송
```

#### XMLHttpRequest.prototype.`open`
`open` 메서드는 서버에 전송할 HTTP 요청을 초기화

|xhr.open(||
|:---:|:---:|
|method,|HTTP 요청 메서드(`GET`, `POST`, `PUT`, `DELETE` 등)|
|url|HTTP 요청을 전송할 URL|
|[, async]])|비동기 요청 여부. 기본값 true|

#### HTTP 요청 메서드
> 클라이언트가 서버에 요청의 종류와 목적(리소스에 대한 행위)를 알리는 방법
- CRUD 구현

|HTTP 요청 메서드|종류|목적|페이로드|
|:---:|:---:|:---:|:---:|
|GET|index/retrieve|모든/특정 리소스 취득|X|
|POST|create|리소스 생성|O|
|PUT|replace|리소스 전체 교체|O|
|PATCH|modify|리소스 일부 수정|O|
|DELETE|delete|모든/특정 리소스 삭제|X|

#### XMLHttpRequest.prototype.`send`
> `open` 메서드로 초기화된 HTTP 요청을 서버에 전송
- GET, POST 요청 메서드에 따라 전송 방식에 차이가 있음

`GET`
- 데이터를 URL의 일부분인 쿼리 문자열로 서버에 전송
- send 메서드에 페이로드로 전달한 인수는 무시, 요청 몸체(request body)는 null로 설정

`POST`
- 데이터(payload)를 요청 몸체에 담아 전송
- 페이로드가 객체인 경우 반드시 JSON.`stringify` 메서드를 사용해 직렬화한 다음 전달 
```javascript
xhr.send(JSON.stringify({ id: 1, content: 'HTML', completed: false }));
```

#### XMLHttpRequest.prototype.`setRequestHeader`
> 특정 HTTP 요청의 헤더 값 설정
- 반드시 `open` 호출 후 호출

`Content-type`
> 요청 몸체에 담아 전송할 데이터의 MIME 타입의 정보를 표현
- 자주 사용하는 HTTP 요청 헤더

|MIME 타입|서브 타입|
|:---:|:---:|
|text|text/plain, text/html, text/css, text/javascript|
|application|application/json, application/x-www-from-urlencode|
|multipart|multipart/formed-data|

```javascript
// 클라이언트가 서버로 전송할 데이터의 MIME 타입 지정: json
xhr.setRequestHeader('content-type', 'application/json');
```

`Accept`
서버가 응답할 데이터의  MIME 타입을 `Accept`으로 지정가능
- Accept 헤더 설정 X -> Aceept 헤더가 `*/*`로 전송

```javascript
// 서버가 응답할 데이터의 MIME 타입 지정: json
xhr.setRequestHeader('accept', 'application/json');
```

### 43.3.4 HTTP 응답 처리
- 서버가 전송한 응답을 처리하려면 `onreadystatechange`를 캐치하여 응답 처리
- 반드시 브라우저 환경에서 실행
- HTTP 요청을 전송하고 응답을 받으려면 서버 필요 

`onreadystatechange` 이벤트
- readyState 프로퍼티 값이 변경될 때마다 발생
- readyState 프로퍼티 값이 4(XMLHttpRequest.DONE)여야 서버 응답이 완료됨

```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1'); // HTTP 요청 초기화
xhr.send(); // HTTP 요청 전송

xhr.onreadystatechange = () => {
  // 만약 서버응답 아직 완료x -> 처리 X
  if (xhr.readyState !== XMLHttpRequest.DONE) return;

  // status 프로퍼티 = 응답 상태 코드 
  // 200 : 정상 응답
  // 그 외 : 에러 발생
  if (xhr.status === 200) { //  response 프로퍼티에 서버의 응답 결과가 담김.
    console.log(JSON.parse(xhr.response));
    // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
  } else {
    console.error('Error', xhr.status, xhr.statusText);
  }
};
```

`onload` 이벤트
> HTTP 요청이 성공적으로 완료된 경우 발생
- 캐치할 경우 `xhr.readyState`가 DONE인지 확인할 필요 X

```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');
xhr.send();

xhr.onload = () => {
    console.log(JSON.parse(xhr.response));
  } else {
    console.error('Error', xhr.status, xhr.statusText);
  }
};
```
