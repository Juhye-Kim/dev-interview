### **CSS**

1.  SCSS/SASS의 장점

    1. nesting
       - html처럼 구조적으로 관리가능, 가독성 좋음
    2. 변수 사용
       - 유지보수 쉬워짐
    3. 조건문, 반복문, 간단한 연산 가능
       - CSS도 프로그래밍 하듯이 다룰 수 있음

2.  id, class의 차이점

    - id는 유일한 요소, class는 복수 요소에 적용시 사용
    - 하나의 id는 한 문서에서 한 번만 사용이 가능하지만, 하나의 class는 여러 번 사용 가능
    - id 는 #, class는 . 으로 표현
    - 우선순위는 id가 class보다 높다.

3.  px, em, rem, vh, vw 차이점
    - px
      - 가장 기본으로 사용되는, 절대적 단위
      - 픽셀단위라는 고정값에 따라 정해짐 → 화면 크기, 확대 등 사용자가 임의로 정의할 수 없음
    - em
      - 부모요소를 기준으로 자식요소 크기가 정해짐 (배수)
      - ex. 부모 10px, 자식 1.2rem → 12px
    - rem
      - root em, 최상단요소 기준으로 크기 정해짐 (html)
    - vh, vw
      - 뷰포트 높이, 너비에 비례하는 크기
        - 100vh = 디스플레이에 꽉차는 높이
      - 반응형 페이지 만들때 유용
4.  box model

    - CSS 박스 모델에 대해 설명하세요.
      > 모든 HTML 요소는 박스모양으로 구성되는데, 이걸 박스모델이라고 함
      - **구성요소**
        - 실제 내용부분인 content를 중심으로, 테두리인 border,
          내용과 테두리 사이 간격인 padding,
          이웃하는 다른 요소와의 간격인 margin 네 가지 영역으로 구분
    - inline vs block vs inline-block
      - block
        - 요소 추가시 줄바꿈 발생
        - w/h O, padding/margin/border O
        - ex. \<div>, \<h1>, \<p>
      - inline
        - 요소 추가시 나란히 배치됨
        - w/h X
        - margin 상하 X, padding 상하는 시각적으로만 추가, 공간차지 X
          - 인라인 요소의 상하 여백은 `line-height` 속성에 의해 발생
        - ex. \<span>, \<a>
      - inline-block
        > 기본적으로 inline + 너비높이 지정 가능
        - 줄바꿈 X
        - w/h/margin O
          - width/height 지정X시 inline처럼 컨텐츠만큼 차지

5.  position, display

    - position vs display
      - **position**
        - 상대적, 절대적 위치 지정할 수 있게됩니다. 즉, 요소의 위치 결정
      - **display**
        - 요소가 어떻게 표현될지를 결정
        - 근본적으로 배치 방식에는 영향을 주지 못함
    - position의 종류?

      - static (default)
        - 웹 페이지의 흐름에 따라, 원래 위치해야 하는 곳에 차례대로 위치
        - top, right, bottom, left 값에 영향을 받지 않음
      - relative
        - 요소의 기본 위치(static 위치)를 기준으로 상대적인 위치를 설정
      - absolute
        - 위치가 설정된 조상 요소를 기준으로 위치를 설정
          - 위치가 설정된 조상이 없으면 body 기준
      - fixed
        - viewport를 기준으로 위치 설정
          - 스크롤 되어도 항상 같은 곳에 위치
      - sticky
        - 평소에는 static + 스크롤이 임계점에 이르면 fixed

    - CSS 레이아웃 기법의 종류, 특징 (grid, flexbox)

      > 둘다 여러 요소들이 화면에서 어떤식으로 배치될지 레이아웃을 지정하는데 쓰이는 속성들

      - **flexbox**
        - 하나의 축만 가지고 요소들을 배치
        - 수직 정렬, 위치 고정 할 수 있음
      - **grid**
        - 두개의 축을 가지고 요소들을 배치
        - 그리드, 격자 기반의 레이아웃을 만들기 위해 사용

    - float이 무엇이고, 어떻게 해제하나요?
      > 이미지를 텍스트와 함께 배치하려고 등장했는데, 레이아웃용(강제 좌우배치)으로도 많이 사용
          - ex. img { float: left }
            - left, right 지정시 display는 무시됨
      - 해제방법
        - 주위에 다른 요소들이 흐르는걸 방지하려면 해제 필요
          1. 다음 형제요소 clear: (left, right, both)
             - 다음 형제요소가 없을 때 문제가 생길 수 있음
          2. 부모 요소 overflow: (hidden, auto)
             - float와 아무 관련없는 overflow → 편법이라 잘사용 X
          3. 부모요소에 clearfix클래스를 추가
    - flex, grid가 탄생하기 이전에는 어떻게 레이아웃을 설정했나요?
      - [mdn](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Supporting_Older_Browsers#%EB%8C%80%EC%B2%B4_%EB%A9%94%EC%84%9C%EB%93%9C)
      - float으로 강제지정, display: table 등 사용

6.  html \<img> vs CSS background-image
    - **\<img>**
      > 이미지가 사용자에게 컨텐츠 이해에 도움을 더 준다고 생각하면 img 태그
      - img 태그는 로드 실패 시 broken img + alt 텍스트가 기본적으로 보임
      - alt 지정 가능 → SEO 유리
    - **background-image**
      > 그렇지 않으면 background image
      - alt 못넣음, broken image도 없음
        - SEO 불리, 스크린 리더가 무시
7.  css 우선순위
    - !important > html style지정 > id > class > 상속
8.  reset.css vs normalize.css
    > 브라우저마다 tag들은 기본적으로 가지고 있는 스타일들이 있는데, 모든 브라우저가 통일된 스타일을 갖게하는 방법들
    - reset.css
      - 어떤 브라우저를 사용하든 동일한 서비스를 제공하기 위해 아예 스타일링을 초기화해버림
        - ex. margin: 0, h1 크기, <li> dot 등 모두 리셋
    - normalize.css
      - 태그들이 기본적인 style은 가지게 하면서, 하나의 기준으로 통일
        - ex. <h1> → font-size: 28px, li → list형식...
      - 단점 : 지속적인 업데이트 필요 (브라우저 업뎃시 같이업뎃)
9.  css in js, css in css?

    > CSS-in-JS → 필요한 컴포넌트의 스타일 요소만 로딩 → 개발 효율성에 중점을 둔 컴포넌트 위주의 프로젝트에 적합

    - **CSS-in-CSS**

      > CSS-in-CSS → 렌더링 시 모든 CSS 스타일 요소를 로딩 → 사용자 편의에 방점을 둔 인터렉티브한 웹 프로젝트

      1.  CSS 모듈 (.module.css 파일)
          - CSS를 모듈화 하여 사용하는 방식
          - 장점 : 클래스명 중복문제 해결
            - CSS 파일에 선언한 클래스명들은 모두 고유해짐
              - 모듈화된 CSS → 번들러로 불러오면 → 사용자 정의 네임 + 고유한 클래스네임으로 이뤄진 객체 반환
          - 단점 : 별도로 많은 CSS 파일을 만들어 관리해야 함
      2.  CSS 전처리기
          - Sass, Less, Stylus...
          - nesting, 변수, 조건/반복문

    - **CSS-in-JS**

      - js코드에서 CSS를 작성하는 방식
      - 장점 : js변수 등 반영해서 동적으로 스타일링하기 좋음
      - 클래스명이 build time에 유일한 값으로 변경 → 별도의 명명 규칙 필요 X
        - 컴포넌트 렌더링시 style 태그 생성 (전처리기 거침)
      - ex. Styled-Components(stylis 전처리기)
      - **장점**
        - 컴포넌트와 CSS가 동일한 구조로 관리됨 → 수정, 삭제 용이
        - 네임스페이스 충돌 방지로 BEM 같은 방법론을 사용하면 class 명이 길어짐 → 짧은 길이로도 유일한 이름 사용 가능
      - **단점**
        - 브라우저가 바로 해석하지 못함 → 별도 라이브러리 설치 필요 → 다운로드 시간 길어짐, 초기진입속도 느림
        - 인터랙션 성능 저하 → 인터랙션에 의해 상태 변경시, js의 css코드를 읽어와 파싱부터 해야해서 반응속도가 늦어짐

    - **비교**

      1. **컴포넌트 위주의 프레임워크**

         - CSS-in-CSS : 사용하지 않는 CSS 스타일 요소까지 로딩
         - CSS-in-JS : 필요한 컴포넌트 페이지의 CSS 스타일 요소만 로딩

      2. **인터렉티브한 웹 사이트**

         - CSS-in-CSS : 이미 CSS 스타일 요소가 로딩되어 있어서 컴포넌트 상태가 변해도 바로 적용 가능
         - CSS-in-JS : 상태 변경으로 렌더링될 때마다 CSS 코드 로딩 필요 (파싱 등) → 성능 저하 위험

      3. **콘텐츠가 많은 웹 사이트**
         - 초기 랜더링 시간이 김
         - CSS-in-JS → 라이브러리 설치로 번들링 크기가 커져 초기 속도가 늦어질 수 있음
           - html이 먼저 렌더링 되는 SSR를 사용해도 SSR를 위한 라이브러리를 설치해야함
