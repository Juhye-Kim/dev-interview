# HTML

1.  CSS \<link> 태그를 \<head>에, JS \<script> 태그를 </body>에 위치시키는 이유?

    - **\<link>를 \<head>에 두는 이유**
      - HTML, CSS는 파싱되어 각각 DOM, CSSOM 만듦 ⇒ 렌더트리 생성하려면 두 가지 모두 완성되어야 함
        - 렌더트리가 없으면 렌더링 차단됨
      - 그리고 DOM은 파싱 중 태그를 발견할 때마다 순차적으로 구성할 수 있지만, CSSOM은 CSS를 모두 해석해야 구성 가능
        → 렌더트리 빨리 구성하려고 CSS를 head에 넣음
        - @import는 병렬 다운 불가!
    - **\<script>를 \</body>에 두는 이유**
      - HTML을 위에서 아래로 파싱하다 \<script>를 만나면 일시정지, JS 파싱이 끝나면 재개
      - head같이 앞 부분에 넣으면, 무거운 파일인 경우에는 한참동안 미완성의 화면을 보여주게 됨 ⇒ DOM 구조가 필요한 script면 에러도 날 수 있음
      - body 앞에 넣으면, DOM은 완성된 상태라 이런 일을 방지할 수 있음

1.  \<script> \<script async> \<script defer>의 차이점은?

    - \<script> : html 파싱을 중지했다가 js 파싱 끝난 후 재개
    - \<script async> : html, js 파싱 병렬 진행
    - \<script defer> : html 파싱 중 js파일 병렬적으로 fetch, 실행은 html파싱 후
      - 여러개 존재하면 순서대로 수행됨

1.  시맨틱 태그에 대해 설명해주세요.

    > 의미 전달 목적의 태그 (내용 유추 가능)

    - ex. nav, table, header, footer, address, form, img, section, article..
    - HTML5에 도입
    - SEO에 유리, 코드 가독성 높아짐

1.  \<section>, \<article>의 차이점?

    - \<section>
      - 비슷한 특성의 컨텐츠를 담는 구역을 설정할 때 사용
      - ex. header, footer 사이에 sidebar나 content를 담는 식
    - \<article>
      - 관련성 없는 독립적인 컨텐츠들을 담을 때 사용
      - ex. section 안에서 서로 다른 글들을 각각 나열할 때

1.  Attribute, property의 차이점?
    > HTML의 attribute → DOM의 property
    - attribute : 정적, 변하지 않음
      - html 초기 상태 지정하는 역할
    - property : 동적으로 값이 변할 수 있음
      - setter, getter 존재하는 접근자 프로퍼티 (참조, 변경 가능)
    - ex. \<checkbox>
      - 체크시 attribute는 변하지 X, property는 checked로 변함
1.  data- 속성에 대해 설명해주세요.

    - HTML5
    - html 요소에 정의한 사용자 정의 어트리뷰트(data-\*)와 js가 데이터 교환 가능
      - 데이터를 DOM 요소에 저장해두는게 목적
      - 브라우저는 데이터 속성에 관여 X
      - dataset 프로퍼티로 값 취득 가능 - ex. user.dataset.userId === '1';
    - **장점**

      - 데이터 속성의 장점은 이전과 같이 hidden으로 태그를 숨여두고 데이터를 저장할 필요 X
      - 따라서 훨씬 HTML 스크립트가 훨씬 간결해짐
      - 하나의 HTML 요소에는 여러 데이터 속성을 동시에 사용할 수도 있음

    - **주의할 점**
      - 관찰 해야하는, 접근 가능해야하는 중요한 내용은 데이터 속성에 저장하지 않는 것이 좋다.
        - 접근 보조 기술이 접근할 수 없기 때문
      - 검색 크롤러가 데이터 속성의 값을 찾지 못하는 문제도 가지고 있음
      - 반대로 HTML에 데이터를 넣는 것은 누구에게나 보이고, js로 접근 가능하기 때문에 누구나 수정할 수 있음
        - 민감한 데이터는 넣지 않는 것이 좋음
      - IE는 표준을 지원하지만, 이전 버전들은 dataset을 지원X
        - IE10 이하 버전을 지원하기 위해서는 getAttribute()를 통해서 데이터 속성을 접근해야 한다.
      - JS 데이터 저장소에 저장하는 것과 비교해서 데이터 속성 읽기의 성능이 저조

1.  DOCTYPE
    - DOCTYPE 이란?
      > 문서의 HTML버전이 뭔지 브라우저에 알려주는 역할을 하는 선언문
      - 어떤 문서형식 정의(DTD)를 따르는지
        - 각 형식마다 적용되는, 적용되지 않는 태그가 있음
        - 마크업 문서의 요소와 속성등을 처리하는 기준
      - Doctype 선언 O → 표준모드로 렌더링 → 브라우저 별로 같은 레이아웃으로 결과물 출력
      - Doctype 선언 X → 쿼크모드로 렌더링 → 브라우저마다 다른 결과물 출력
      - **문서형 정의(DTD, Document Type Definition)**
        - HTML5, XHTML, HTML 세가지 문서 유형 존재
          - 기술한 유형에 따라 마크업 문서의 요소, 속성 등을 처리, 유효성 검사에 이용
    - DOCTYPE 유형이 무엇이 있을까오?
      - **Strict**
        - 엄격한 규격으로 구조와 표현을 분리, 단계적으로 없어질 요소와 속성을 제외 시킨 문서 타입
          - 비표준 태그인 center, font.. 사용 불가 → css로 대체해야 동작
      - **Transitional**
        - 표준이 정립되기 전, 문서들과의 호환성을 유지하려고 만들어진 문서 타입
          - iframe, 새창 띄우기 target="\_blank".. 사용 가능
      - **Frameset**
      - 프레임셋을 지원하기 위한 문서타입
        - 지금은 거의 사용하지 않음, 프레임셋 사용 가능 - Transitional과 유사 (프레임셋 지원 차이)
          > HTML5에서는 단 한 가지 방법으로도 DOCTYPE을 선언할 수 있습니다.
          - 이전 버전의 HTML(2~4)은 **SGML(Standard Generalized Markup Language)** 기반이라 DTD 참조가 필요 → DOCTYPE 선언시 공개 식별자, 시스템 식별자가 포함된 긴 문자열을 작성해야 했음
            - SGML : 마크업 언어를 정의하기 위한 메타 언어, 문서의 마크업 언어나 태그 셋을 어떻게 정의할 것인가에 대한 표준
          - HTML, XHTML은 각 버전에서 사용 가능한 태그나 속성 등을 DTD로 상세히 정의
            - DTD: XML 문서들의 클래스에 논리적인 구조를 강요하는 법칙
              - 모든 적법한 마크업을 쓰고 마크업이 문서에 포함될 수 있는 장소와 그 방법을 지정
          - HTML5는 SGML 기반이 아니라 DTD 참조가 필요 없고, 간단히 선언 가능
          ```
          <!DOCTYPE html>
          ```
    - MIME, DOCTYPE의 차이점?
      - MIME : 콘텐츠 타입
        - HTTP head에 명시
        - 지정한 콘텐츠 타입에 따라 문서 처리 방식 결정
          - text/html이어야 HTML로 렌더링
      - DOCTYPE : HTML 버전을 선언하는 역할
1.  \<meta>

    - meta 태그란?

      > 웹페이지의 메타 데이터 정보를 제공할 때 사용 → 검색엔진이 활용

      - **메타태그 속성**
        - http-equiv : 웹 브라우저 서버에 명령 내리는 속성
          - html문서가 응답헤더와 함께 서버에서 브라우저로 전송될 때만 의미를 가짐
        - name : 메타정보 이름 지정
        - content : 메타정보 내용 지정
          - name, http-equiv 속성 명시 → content 속성도 명시 필요
          - 두 속성 명시X → content도 명시X
      - **메타태그 종류**
        1. keyword
           ```jsx
           <meta name="keyword" content="HTML, meta, tag, element, reference">
           ```
        1. description (검색 결과 표시되는 문자)
        1. author
        1. 5초 뒤 다른 페이지로 redirect
        1. robots (검색 로봇 제어)
        1. viewport 설정(모든 장치에서 웹 사이트가 잘 보이도록)

    - meta 태그로 검색엔진최적화하는 방법?

      - name = keywords(키워드), description(요약)
      - 로봇이 keywords, description 기반으로 검색하는 경우가 있음
        ```html
        <meta name="keywords" content="html, CSS, JS" />
        <meta name="description" content="요약" />
        ```

    - 웹 크롤러가 문서를 검색하지 못하게 하려면?
      1. meta 태그 robots로 제어
         - <meta name="robots" content="noindex, nofollow" />
             - 이문서X + 링크된 문서X 긁어감
                 - noindex : 웹 크롤러가 수집시 index하지 않도록 함
                 - nofollow : 문서에 링크된 다른문서를 긁어가는 것 방지
      2. robots.txt 파일로 제어
