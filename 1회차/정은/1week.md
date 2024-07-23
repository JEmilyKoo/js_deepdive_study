# 1.프로그래밍
## 1.3 구문과 의미

> 프로그래밍이란, 요구사항의 집합을 분석해서 적절한 자료구조와 함수의 집합으로 변환한 후, 그 흐름을 제어하는 것.

---

# 2. 자바스크립트란?
## 2.1 자바스크립트의 탄생

> 자바스크립트
- 넷스케이프 커뮤니션즈가 개발(1995)
- 웹 페이지의 보조적 기능을 수행하기 위해 브라우저에서 동작하는 경량 프로그래밍 언어
- 모든 브라우저의 표준 프로그래밍 언어

## 2.2 자바스크립트의 표준화

- 1996 : JScript와 자바스크립트의 **크로스 브라우징 이슈** 발생
- 1996 : ECMA 인터내셔널에 표준화 요청
- 1997 : ES1 초판 등장. ECMAScript 명명
- 1998 : ES2 ISO / IEC 16262 국제 표준과 동일한 규격 적용
- 1999 : ES3 정규표현식, try ... catch
- 2009 : ES5 JSON, strict mode, 접근자 프로퍼티, 프로퍼티 어트리뷰트 제어, 향상된 배열 조작 기능
- 2015 : ES6 let/const, 클래스, 화살표 함수, 템플릿 리터럴, 디스트럭처링 할당, 스프레드 문법, rest 파라미터, 심벌, 프로미스, Map/Set, 이터러블, for...of, 제너레이터, Proxy, 모듈 import/export
- 2016 : ES7 지수연산자, Array includes, String includes
- 2017 : ES8 async/await, Object 정적 메서드
- 2018 : ES9 Object rest/spread 프로퍼티, Promise finally, async generator, for await... of
- 2019 : ES10 Object.fromEntries, Array flatMap, optional catch binding
- 2020 : ES11 String matchAll, BigInt, globalThis, Promise.allSettled, null 병합 연산자, 옵셔널 체이닝 연산자, for ... in enumeration order, 동적 import 추가
- 2021 : ES12 논리 할당 연산자, String replaceAll, WeakRefs, FinalizationRegistry
- 2022 : ES13 최상위 await, private Class Fields, RegExp Match Indices, at()
- 2023 : ES14 배열 관련 메소드, findLast(), findLastIndeX(), Hashbang
- 2024 : ES15 Temporal API, 파이프 연산자, 레코드, 튜플

## 2.3 자바스크립트 성장의 역사

#### 렌더링

> HTML, CSS, 자바스크립트로 작성된 문서를 해석해 브라우저에 시각적으로 출력하는 것. 서버에서 데이터를 HTML로 변환해 브라우저에 전달하는 과정(SSR)을 가리키기도 함.
-> 38장 브라우저의 렌더링 과정

### 2.3.1 Ajax

> 서버와 브라우저가 **비동기 방식**으로 데이터를 교환할 수 있는 통신기능. Asynchronous Javascript and Xml(1999)


|이전|변경점|Ajax|
|:---|:---:|---:|
|전체 다|렌더링|변경하는 부분만 한정적으로|
|불필요한 데이터 통신 발생|데이터 통신|빠름|
|있음|화면 깜빡임|없음|


### 2.3.2 jQuery

> DOM(Documnet Object Model)을 쉽게 제어. 크로스 브라우징 이슈 상당수 해결(2006)

### 2.3.3 V8 자바스크립트 엔진

> 빠르게 동작하는 자바 스크립트 엔진(구글, 2008)

- 데스크톱애플리케이션과 유사한 UX(User eXpreience)를 제공할 수 있는 웹 애플리케이션 프로그래밍 언어
- 프런트엔드가 주목받는 계기

### 2.3.4 Node.js

> V8 자바스크립트 엔진으로 빌드된 자바스크립트 런타임 환경(라이언 달, 2009)

- 자바스크립트 엔진을 브라우저에서 독립시킨 자바 스크립트 실행 환경
- SSR 개발에 주로 사용
- 모듈, 파일 시스템, HTTP 등 빌트인 API 제공
- 동형성 : 프런트엔드와 백엔드 영역에서 자바스크립트 사용 가능
- **비동기 I/O 지원** , **싱글 스레드 이벤트 루프** 기반 동작 -> 요청 처리 우수
- 실시간 처리를 위해 I/O가 빈번하게 발생하는 SPA(Single Page Application)에 적합
- CPU 사용률이 높은 애플리케이션에는 부적합
- 웹 프로그래밍 언어의 표준 : 서버 사이드 애플리케이션에서도 사용 가능한, 프런트엔드와 백엔드를 아우르는 언어
- **크로스 플랫폼** 을 위한 가장 중요한 언어 : 모바일 하이브리드 앱(PhoneGap, Iconic), 서버 사이드(Node.js), 데스크톱(Electron), 머신 러닝(Tensorlow.js), 로보틱스(Johny-Five)

#### 싱글 페이지 애플리케이션(single-page application, SPA, 스파)

> 서버로부터 완전한 새로운 페이지를 불러오지 않고 현재의 페이지를 동적으로 다시 작성함으로써 사용자와 소통하는 웹 애플리케이션이나 웹사이트

#### 크로스 플랫폼

> 컴퓨터 프로그램, 운영 체제, 컴퓨터 언어, 프로그래밍 언어, 컴퓨터 소프트웨어 등이 여러 종류의 컴퓨터 플랫폼에서 동작할 수 있다는 것

###  2.3.5 SPA 프레임 워크

- 개발 규모와 복잡도가 상승 -> 패턴과 라이브러리 출현
- 변경에 유연하며 확장하기 쉬운 애플리케이션 아키텍처의 구축 -> 프레임 워크 등장 
- CBD 방법론을 기반으로 하는 SPA가 대중화
- Angular, React, Vue.js, Svelte 등

#### 컴포넌트 기반 개발(component-based development, CBD)
> 기존의 시스템이나 소프트웨어를 구성하는 컴포넌트를 조립해서 하나의 새로운 응용 프로그램을 만드는 소프트웨어 개발방법론

## 2.4 자바스크립트와 ECMAScript

#### ECMAScript
- 자바스크립트의 표준 사양인 ECMA-262
- 프로그래밍 언어의 값, 타입, 객체, 프로퍼티, 함수, 표준 빌트인 객체 등 핵심 문법 규정
- 각 브라우저 제조사는 ECMAScript 사양을 준수해서 브라우저에 내장되는 자바 스크립트 엔진을 구현

#### JavaScript
- 프로그래밍 언어
- 기본 뼈대를 이루는 ECMAScript, 브라우저가 별도로 지원하는 클라이언트 사이드 Web API, DOM, BOM, Canvas, XMLHttpRequest, fetch, requestAnimationFrame, SVG, Web Storage, Web Component, Web Worker 등을 아우르는 개념

ECMAScript ⊂ JavaScript

클라이언트 사이드 Web API의 자세한 내용 : [MDN web docs의 Web API 페이지](https://developer.mozilla.org/ko/docs/Web/API)

## 2.5 자바스크립트 특징

- 웹 브라우저에서 동작하는 유일한 프로그래밍 언어
- 인터프리터 언어

|컴파일러 언어|구분|인터프리터 언어|
|:---|:---:|---:|
|컴파일 타임 : 전체를 머신 코드로|코드 변환|런타임 : 문 단위로 한 줄씩 중간코드인 바이트 코드로|
|O|실행 파일|X|
|컴파일 - 실행 분리 O|단계 분리|인터프리트 - 실행 분리 X |
|한 번|컴파일 횟수|코드가 실행될 때마다 인터프리트 과정이 반복 수행|
|빠름|속도|느림|

- 멀티 패러다임 프로그래밍 언어 : 명령형, 함수형, 프로토타입기반, 객체 지향 프로그래밍을 지원
- 프로토타입 기반의 객체지향 언어

## 2.6 ES6 브라우저 지원 현황
인터넷 익스플로러11의 지원 종료로 인해 현행 모든 브라우저에서 사용 가능

---

# 3. 자바스크립트 개발 환경과 실행 방법

크롬 개발자 도구, Node.js, VSCode 설치법
