## Javascript 질문 모음

1.  스코프란?
    > 식별자(변수, 함수, 클래스...)가 다른 코드에서 참조될 수 있는 유효 범위
    - js 엔진이 식별자를 찾을 때 검색하는 범위
    - 전역, 지역 스코프
      - 전역 : 어디서든 접근 가능한 범위
      - 지역 : block, function 스코프로 나뉨
    - js에서는 함수가 태어날 때, 내부슬롯에 상위 스코프에 대한 참조를 저장하고 태어남
2.  function, block scope의 차이?

    > - fuctional scope : 함수를 기준으로 스코프 (범위)를 나눔 (var)
    > - block scope : 중괄호({ })를 기준으로 나눔 (let, const)

    - ex. for문에서 이 점을 주의해야한다. for문의 중괄호는 block scope라 초기화식에 var를 쓰면, function scope내에서 var로 선언된 변수가 변경되어 의도치 않은 결과가 나올 수도 있다.

3.  lexical, dynamic scope의 차이점?

    > Lexical scope : 변수, 함수가 **선언된 곳**에 따라 정의되는 스코프

    - lexing time에 정의되는 스코프 (작성된 위치에 따라)
    - Static Scope라고도 함
    - ex. C/C++, Java, JavaScript 등 대부분의 언어들은 Lexical Scope를 사용

    > Dynamic Scope: 변수나 함수가 **호출된 곳**에 따라 정의되는 스코프

    - ex. Perl, Bash Shell, APL 등의 언어들이 사용

4.  호이스팅이란 무엇이고, 왜 일어나는지?
    > 코드 실행 보다 선언부가 먼저 `메모리`에 저장되는 과정
    - 변수, 함수가 스코프 최상단으로 끌어올려지듯이 보임
    - 선언문은 해당O, 할당은 해당X
    - 호이스팅 발생 이유
      - 변수 생성과 초기화(선언, 할당)가 따로 진행되기 때문
      - js는 코드가 실행되면 코드를 파싱하는데, 이때 전역 컨텍스트에 전역 변수 및 함수를 등록
      - 이때 코드를 해석해 변수, 함수 선언문을 코드의 상단으로 끌어올리는 효과가 발생
5.  TDZ란?
    > let, const 로 선언한 변수가 **초기화**되기 전까지 대기하는곳
    - 선언부가 메모리에 저장될 때, var로 선언한 경우는 undefined로 초기화되는데, let, const로 선언되면 초기화가 되지 않음
      - 호이스팅은 되었지만, 초기화는 안된 상태!
      - 초기화 안되었는데 호출 → TDZ에서 대기중 → Reference error
    - TDZ는 선언 전에 변수를 사용하는 것을 허용X → 실수 방지에 도움
6.  전역 스코프 사용시 장단점은?

    - **장점**
      - Reference Error 안남
        - 정말 필요한 변수인 경우, 안전하게 사용 가능
    - **단점**
      - 코드 어디서든 참조가 가능해 의도치 않은 결과 발생
        - 동일 이름으로 만들면 큰일
      - 생명주기가 길어서 메모리 리소스도 오래 소비
        - 전역 변수 생명주기 = 전역객체 생명주기
        - 스코프 체인 상위에 존재해서, 변수 검색시 속도 느림

7.  var, let, const 차이점?

    <img width="624" alt="스크린샷 2021-11-29 오후 8 00 14" src="https://user-images.githubusercontent.com/63178953/143856263-cf0fe9f7-11ad-416d-abbc-9213e9317ac2.png">

8.  클로저란 무엇인가요?

    > 함수와 함수가 선언된 어휘적 환경의 조합, 외부함수의 변수에 접근 가능한 내부함수

    - 외부함수보다 중첩함수가 더 오래 유지될 때, 이미 생명주기가 종료된 외부함수 변수를 참조할 수 있는 구조
      - 이미 실행 종료된 함수의 변수, 함수를 참조할 수 있는 내부함수
        - 외부함수 호출이 종료되어도 외부함수의 변수를 참조하거나, 스코프 체인 관계를 유지
    - 함수가 렉시컬 스코프를 기억하고 접근할 수 있는 특성
      - JS는 선언된 환경(렉시컬)을 기준으로 변수를 조회
      - 참조되고 있기 떄문에 가비지 컬렉션 대상이 되지 않음

9.  클로저를 사용한 경험, 혹은 예시는?
    > 의도치 않게 변경되지 않도록 은닉, 특정함수에게만 상태변경을 허용해서 안전하게 변경, 유지하기 위해 사용
    - ex. 모듈 패턴
      - 모듈 = 재사용 가능한 코드모음, 외부에서 접근 불가
    - ex. 커링패턴
    - ex. private 변수 (캡슐화)
      - 캡슐화 = 외부에서 접근할 수 없도록
      - 실제로 접근하지 못하도록
10. 클로저의 장단점?

    - 장점 : 모듈화, 은닉화
    - 단점 : 생명주기가 길어짐
      - 가비지컬렉터가 수거하게 하기
        - 참조끊기, 이벤트핸들러 → null로 없앰

11. 실행 컨텍스트란?

    > 콜스택에 실행컨텍스트 단위로 담김, 코드들의 순서를 보장하기 위해 사용

    - js엔진은 코드가 실행(함수 호출)될 때 해당 컨텍스트 관련 정보들을 수집하는데, 이 정보들을 **실행 컨텍스트 라고 한다**.
    - 저장되는 정보들
      - **VariableEnvironment :** 최초로 수집되는 정보
      - **LexicalEnvionment :** 이후 변경사항이 생기면 VariableEnvironment를 복사해 생성, 변경된 정보가 담김
        - **environmentRecord** : Variable, Lexical 모두에 포함됨, [식별자](https://joooing.tistory.com/entry/%EB%B3%80%EC%88%98Variable%EB%9E%80)(매개변수, 함수, 변수)
        - **outerEnvironmentReference** : 선언 당시 참조했던 LexicalEnvionment의 정보
      - **ThisBinding** : this로 지정된 객체 (지정되지 않은 경우 전역객체 저장)

    ***

    1. 코드실행에 필요한 환경을 제공
       - 환경에서 실행될 코드들에 대한 온갖 정보를 모아둔 객체
       - 스코프 관리 (by 렉시컬 환경)
    2. 코드실행 순서 관리
       - by 콜 스택

    - 함수 → 선언, 초기화, 할당 모두됨
    - 변수는 키워드따라 다름
      ```jsx
      실행 컨텍스트: {
        렉시컬 환경 컴포넌트: {
          렉시컬 환경: {
            환경 레코드: {
              선언적 환경 레코드: { // 현재 스코프에 선언된 식별자 (변수, 함수...) }
            },
            외부 렉시컬 환경 참조 : 상위 스코프 참조  // 전역에서는 null
          },
        },
        변수 환경 컴포넌트: {
          // 렉시컬 환경 컴포넌트에 설정된 '렉시컬 환경'을 복사한 것
          // 실행 단계에서 참조하는건 렉시컬 환경 컴포넌트, 변수 환경 컴포넌트는 이후 초기값으로의 환원을 위한 컴포넌트이다.
        },
        this바인딩
      }
      ```

12. Lexical Environment란?

    - 현재 컨텍스트 관련 식별자 정보 저장
      - 매개변수, 함수, 변수 ...
      - 식별자(key) : 바인딩(value) 형태로 관리 (?)
    - 외부환경 참조 정보
      - 선언되었던 당시의 렉시컬 환경 참조 → 덕분에 스코프 체인 가능!
      - 스코프를 구분해, 식별자를 등록/관리

13. 일급객체(first-class citizen)란?

    - 조건
      1. 변수나 데이터에 담을 수 있다.
      2. 파라미터로 전달 가능
      3. 리턴 값으로 사용 가능
    - 프로그래밍 언어에서 type을 전달, 반환, 할당 할 수 있으면, 해당 type을 1급 객체로 간주
    - Javascript의 함수는 일급객체
      - 하나 이상의 함수를 인자로 받거나, 함수를 반환하는 고차 함수 만들 수 있음!
      - 함수형 프로그래밍으로 Javascript가 인기가 있어지는 이유

14. 콜백함수, 고차함수란?
    - 콜백 함수
      - 함수의 매개변수로 전달되는 함수
    - 고차 함수(Higher-Order Function, HOF)
      - 함수를 인자로 받거나, 함수를 반환하는 함수
15. 데이터 타입

    - JS 배열의 타입은 왜 object인가요?
      - _일반적인 배열 : 동일한 크기의 메모리 공간이 연속적으로 나열된 밀집 배열_
        - 메모리 공간 동일 = 데이터 타입이 같다
      - JS 배열 : 일반적인 배열의 동작을 흉내낸 특수한 **객체**
        - 요소들의 메모리 크기가 같지 않아도 되고, 연속적이지 않을 수도 있음
        - index를 키로 가지며, length 프로퍼티를 갖는 특수한 객체
          - JS의 모든 타입은 객체의 값이 될 수 있기 때문에, 어떤 타입이든 배열의 요소가 될 수 있음
        - Prototype이 Object.prototype
    - null, undefined, undeclared의 차이점
      - **undefind**
        - 값이 정의되지 않았다.
        - 변수를 선언만 하면 자동으로 할당
        - 선언만 되고, 값은 정의되지 않은 상태
          - 자체가 data type
      - **null**
        - 값이 비었다.
        - 선언후, 수동으로 null을 담아줘야함
        - 명시적으로 값이 비었음을 나타낼 때 사용
          - object (버그..)
      - **undeclared**
        - 선언조차 되지 않았다.
          - 접근 가능한 스코프에 변수 선언조차 되어있지 않은 상태
    - 원시, 참조 자료형의 차이점
      - **원시**
        - 할당시 메모리에 고정된 크기로 저장되고, 변수에 값이 담김
        - 선언, 초기화, 할당 시 값이 저장된 메모리에 직접 접근 (access by value)
        - 복사 시에도 값을 복사 → 한 변수를 변경해도 다른변수에 영향 X
        - ex. number, string, boolean, undefined, symbol, bigint
      - **참조**
        - 데이터 크기가 정해지지 않고, 변수에는 값이 저장된 주소가 담김
          - heap 메모리 주소
          - js 엔진이 주소를 이용해서 값에 접근
        - 복사도 주소를 복사함 → 복사 후 변경하면 다른변수에 영향 O
        - ex. array, object, function
    - Set, Map의 차이점
      - **Set**
        - 값 중복X, 순서 의미X, index X
        - iterable → 순서에 의미는 없지만, 추가된 순서로 순회
      - **Map**
        - 키, 값 쌍으로 이루어진 컬렉션 (키 중복 X)
        - iterable → 순서에 의미는 없지만, 추가된 순서로 순회
        - Object와 유사
          - Object: Key Type은 string, symbols, number
            - not iterable
          - Map: Key Type으로 모든 datatype 사용 가능 (array,object...) - iterable
      - **Set,Map이 필요한 이유**
        - object는 string, symbol 만 키값으로 들어감
        - 객체 프로퍼티 개수를 size로 바로 알 수 있음
        - object는 not iterable
          - for of, spread syntax 사용 안됨
    - 정적타입, 동적타입의 차이는? Javascript는 무슨 타입?
      - 정적타입
        - 타입을 컴파일 시에 결정, 변수의 타입지정 필요
        - C, C#, C++, Java
      - 동적타입
        - 타입지정없이 변수에 값 할당
        - 런타임때 값의 타입에 따라 자동 결정
          - JavaScript, Ruby, Python, SmallTalk
          - 변수에 여러타입의 값 할당 가능
    - Javascript 자료형 중 객체와 다른타입들 간에 차이점은?
      > 원시형을 제외한 나머지(함수, 배열, 정규 표현식 등)는 모두 객체
      - 원시형
        - 하나의 값만 나타냄
        - 원시값은 변경 불가능 (immutable)
      - 객체
        - 다양한 값들을 하나로 구성한 복합적인 자료구조
        - 객체는 변경 가능한 값(mutable)
    - 유사배열객체란?
      - 배열처럼 index로 프로퍼티 값에 접근 가능
      - length 프로퍼티를 갖는 객체
        - for 문으로 순회 가능
      - ex. arguments, NodeList
    - Symbol이란 무엇이고, 어떻게 활용할 수 있는지?

      > 유일한 값을 만들 때 사용하는 primitive type 값

      ```jsx
      const sym = Symbol("hi"); // Symbol함수로 생성
      typeof sym; // 'symbol'

      // 전역 심볼 레지스트리 이용
      const sym = Symbol.for("hi");
      Symbol.keyFor(sym); // hi
      ```

      **활용**

      1. 유일무이한 키 값
      2. 외부에 노출할 필요가 없는 프로퍼티 은닉
         - for…in 문, Object.keys, Object.getOwnPropertyNames 등으로 접근 불가
         - ES6 Object.getOwnPropertySymbols()로 찾을 수 있긴함
      3. 표준 빌트인 객체 확장
         - 보통 표준 빌트인 객체에 메서드를 직접 추가하여 확장하는 것은 권장 X
           - 미래에 표준 사양으로 추가될 메서드의 이름이 중복될 수 있기 때문
         - 심벌 값으로 프로퍼티 키를 생성해 확장하면 충돌 X, 안전하게 확장 가능

16. 연산자

    - ==(동치연산자), ===(일치연산자) 차이점?
      - ==
        - 값만 비교
        - 강제 형 변환 (비교전 두 피연산자를 공통 타입으로 바꾸고 시작)
          - ex. 문자열 1 = 숫자 1 = true
          - valueOf, toString
      - ===
        - 값 + 데이터타입 비교
    - function() {} 표현식, 화살표함수의 차이점
      - thisBinding 유무
        - function은 실행 컨텍스트에 thisBinding 존재
        - 화살표함수는 thisBinding이 없어 호이스팅처럼 가장 가까운 this를 참조
      - args 유무
        - function은 인자로 모든 인자들을 담은 argument 배열을 가짐
        - 화살표함수는 argument object가 없음
      - constructable
        - function은 생성자 키워드 (new)로 인스턴스 생성 가능
        - 화살표함수는 호출만 가능
      - generator 가능 여부
        - function은 제너레이터로 사용 가능
        - 화살표함수는 불가능
      - prototype 유무
        - 화살표함수는 prototype 프로퍼티가 없음
    - 삼항식(Ternary statement)을 사용하는 이유와, 표현하기 위한 연산자 단어는?
      - 세가지 피연산자 → 테스트 조건문, "then"표현식, "else"표현식을 받습니다.
        - `조건문 ? 선택문1 : 선택문2`
      - 동작시킬 코드가 여러개면 ; 말고 , 로 구분해야함
      - **장점**
        - 결과값을 바로 변수에 할당 가능 (if문은 조건식 안에서 할당 처리 필요)
          → 할당이 가능하다? 왜 장점?
          return 문을 매번 작성하지 않아도됨
        - if, else문은 삼항연산자를 사용하면 한줄로 간결하게 정리
        - if문과 달리 체이닝으로 중첩X, 직선적으로 쓸 수 있음
      - **단점**
        - if문은 block scope 생성, 삼항은 X ⇒ if문은 지역변수 생성 가능, 더 다양한 제어 가능
    - optional chaining은 무엇인가요?
      - `?.`
      - ES11(ECMAScript2020)
      - 좌항이 null, undefined이면 undefined 반환
        - 아니면 우항의 프로퍼티 참조를 이어감
        - 체이닝 이어갈건지 확인
      - && 대신 사용
        ```jsx
        let user = {};
        user && user.address && user.address.street; // undefined
        user?.address?.street; // undefined
        ```
    - null 병합 연산자는 무엇인가요?

      - `??`

        - 여러 피연산자 중, 값이 존재하는 변수를 찾을 수 있음
        - 좌항이 null, undefined이면 우항의 피연산자 반환

          - 아니면 좌항 피연산자 반환
          - || 대신 사용
            - `||`는 *truthy* 값을 반환, `??`는 *정의된(defined)* 값을 반환

          ```jsx
          let firstName = null;
          let lastName = null;
          let nickName = "바이올렛";

          firstName ?? lastName ?? nickName ?? "익명"; // 바이올렛
          ```

17. event loop란?

    > 브라우저는 특정 이벤트가 발생하면 이를 감지해 미리 정해둔 작업을 수행한다.여러 이벤트가 동시 발생할경우, 이벤트루프가 실행 순서를 정해준다.

    - event loop은 콜스택에 처리중인 태스크가 없는지, 태스크 큐에 대기중인 태스크가 있는지 반복 확인
      - 콜스택이 비고, 태스크 큐에 대기중인 함수가 있으면 콜스택으로 이동시킴
    - 마이크로 태스크(Promise) > animation frame > 태스크(setTimeout)

      _1. Macro Task Queue 작업 하나를 실행_

      _2. Micro Task Queue 모든 작업을 실행 (1, 2 반복)_

      - **_Macro Task Queue_**

        _: setTimeout, requestAnimationFrame, I/O, UI Rendering_

      - **_Micro Task Queue_**

        _: Promise, process.nextTick, Object.observe, MutationObserver_

        - 마이크로태스크는 이벤트 핸들러, 렌더링, 매크로 실행 전에 처리됨

18. 호스트 객체, 네이티브 객체의 차이점
    - **네이티브 객체**
      - ECMAScript 사양에 정의된 JavaScript 객체
        - 런타임에 상관 X 사용 가능
    - **호스트 객체**
      - 런타임이 제공하는 객체
      - window, XMLHTTPRequest, DOM, BOM...
