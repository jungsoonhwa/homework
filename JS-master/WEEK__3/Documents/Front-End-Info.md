### 1. [흔한 2017년의 Front-end 기술 스택](http://seokjun.kr/front-end-dev-stack-2017/)

#### Front-end libraries

프론트엔드 개발자가 어려운 역할이라는건 시장에 정말 많은 기술이 나와있는데 대부분 각각의 장단점을 지니고 있기 때문이다. React 가 조금 과장해서 사실상의 de-facto standard 라고 할만하지만, 그렇다 해도 모든 케이스에 딱 맞아들어가는 선택은 아니다.

__최근 잘나가는 Vue.js__ 나 Aurelia 같은 녀석들을 써보고 싶은 것도 사실이지만, 프론트엔드 웹 개발자가 많지 않은 회사의 엔지니어로서 러닝 커브가 들어가야 하는 새로운 라이브러리를 소화하기는 어려웠다.

2016년 10월 쏘카에 입사한 후 기존의 php, jQuery, css 기반에서 웹 프론트엔드 스택에 React 와 Sass 로 전환하는 작업을 시작했는데, 이 때 역시 __도입 및 전파까지 적지 않은 시간을 들인 것도 사실이다.__ 지금은 쏘카 앱의 네이티브로도 개발되고 있어서 상대적으로 웹 어플리케이션 엔지니어링에 큰 시간을 들이지는 않지만, 지금까지 그리고 앞으로도 쏘카 기술 스택에서 큰 부분을 차지할 것이 확실하다.

#### Server Side Renderning

__검색 엔진 최적화와 첫 페이지 로딩 속도 이슈 떄문에 SSR 은 반드시 염두에 두고 개발해야 했다.__ 직접 설정하기는 시간도 없고, 어렵기도 해서 Universal Redux Template 이라는 프로젝트를 클론하여 필요한 것들을 추가하거나 뺴는 방식으로 설정했다. 위의 스택 중 많은 부분이 이 템플릿에 자체적으로 포함되어 있는 것이 많았다. 굳이 잘 돌아가는 바퀴를 새로 발명할 이유는 없다.

#### Style

인간적으로... 사실적으로... 볼때 __프론트 엔드에서 제일 어려운게 스타일이다.__ Postcss 나 stylejs 같은 애들을 고려 했지만, 템플릿 고치는게 귀찮아서 그냥 쓰기로 했다. Sass Mixin 은 가져다 쓸 수 있는게 많기도 했고.

#### 프론트엔드 개발자는 솔직히 월급 두배로 줘야 된다!

이렇게 길게 썼는데도 백엔드 관련된 건 한줄도 들어가 있지 않다. 일주일 정도 시간을 써서 설정한 것 같고, AWS t2.small 기준으로 첫페이지 로딩 타임 1.2~1.4 초 정도로 쾌적하게 로드 되고 있다. (라이브 사양임) 실제 오픈 전에는 서버를 몇개 더 만들어서 로드밸런서에 올린 후에 ci 에 추가해주면 높은 사양의 서버를 사용하지 않아도 큰 문제없이 운영 가능할 것이라고 생각 한다.


### 2. [JavaScript in 2017: 옛날 사람 탈출하기](http://meshlabs.ghost.io/javascript-in-2017/)

"옛날 사람"이 된 프론트엔드 개발자가 "요즘 사람"이 되기 위해 어떤 일을 겪어야 했는지 여기에 소개하겠다.

#### jQuery가 한물갔대..

2010년대 초반, 프론트엔드에서 '핫한' 것은 역시 jQuery였다. 모든 플러그인이 다 jQuery 위주로 나왔다. 그럴법도 했다. DOM이라는 핵폐기물을 그럴듯하게 쓸 수 있는 가장 좋은 방법이었으니까.

하지만 jQuery는 태생적으로 큰 한계가 있다. 타이밍. 무슨 인생도 아니고. DOM이 수정되어도 jQuery 객체는 그것을 알지 못한다. 그러니 Ajax로 콘텐츠가 추가되면 (때에 따라 중복 이벤트 바인딩을 막기 위해 기존 이벤트 바인딩을 unbind, 즉, 제거하고) 이벤트를 다시 바인드 해야 한다.

따라서 Ajax 처리 로직이 거대해진다. 그래도 컴포넌트라는 개념을 어떻게든 만들어 쓸 수는 있었다. 그게 너무 힘들었을 뿐이다. (사실 jQuery의 가장 큰 문제는 함수형처럼 보이지만 side-effect가 여기저기에서 튀어나오는 위험한 물건이라는 거다. 그래서 코드가 복잡해진다.)

#### 수련의 시간: 새로운 자바스크립트

먼저, ECMAScript라는 단어에 익숙해져보자. ECMAScript는 브라우저에 따라 제멋대로이던 JavaScript의 표준을 정의하기 위해 만들어진 웹 스크립트 언어의 표준이다. 그 동안 JavaScript가 1.x대에서 놀았다면, 이번엔 2.0으로 올라왔다고 할 수 있을 정도로 큰 변화였다. '왜 이걸 이제서야' 하는 한숨과 함께, 웹 개발자들은 모두 다 함께 새로운 표준을 수련해야 했다.

#### 선택의 시간 1: 어떤 프레임워크를 사용할 것인가?

이제 선택의 시간이 왔다. 어떤 프레임워크를 사용할지. 어쨌든 규모 있는 웹사이트에서 바닐라 JS를 쓰진 않을 것 아닌가. 사실 조금만 돌아다녀도 요즘 자바스크립트 기술을 배울 때 드는 기분에 대한 회의감에 대한 글들이 자주 보이는데, 이런 글들은 하루가 멀다하고 새로운 프레임워크가 등장하는 요즘의 JS 생태계에 대한 피로감을 그대로 대변한다. 그렇다면 어떻게 해야 그 홍수 속에서 만족할만한 기술을 선택할 수 있을까?

이래저래 찾아보고 부딪혀본 결과, 우리는 나름의 원칙을 세울 수 있었다.

- 많이 사용돼야 한다. 그래야 많은 사람과 협업할 때 팀 전체의 러닝 커브를 완만하게 할 수 있다.
- 생태계가 건강해야 한다. 그래야 잘 작동하는 라이브러리를 손쉽게 쓸 수 있다.
- 프로젝트의 특징에 따라 다른 프레임워크를 선택해야 한다. 즉, 기술보다 프로젝트의 특징이 먼저다
  - SPA(Single Page Application)를 만들고 싶다? Vue.js, React.js나 Angular를 고려해보자.
  - 원 페이지(Intro Page)를 만들고 싶다? Vue.js도 좋고, 이런 상황에서는 여전히 jQuery가 현역이다.
  - 라우팅을 서버에서 해준다? 일단 왜 이 시대에 굳이 그래야 하는지 고민해보고, Vue.js를 고려해보자. 라우팅이 필요한 복잡한 웹사이트에서 jQuery 쓰기는 너무 귀찮다.
  - 모바일에서 돌아가는 웹앱을 만들고 싶다? 왜? 꼭 그래야 하나? 정말? 굳이 필요하면 React-native같은 친구들이 있는데, 왜?

#### 수련의 시간 2: Learning Curve

진입장벽이 얼마나 높았는지 감이 오시리라 믿는다. 어떻게 넘느냐? 쉬운 방법이 없다. 그냥 실제로 작동하는 코드를 보고 배우는 수밖에. 문서를 읽고, 검색하고, 튜토리얼이란 튜토리얼은 무조건 다 해보고. 그게 유일한 방법이다.

특히 중요한 점은, 하나의 프로젝트를 어떻게든 완결을 지어봐야 한다는 거다. 그냥 문서만 읽으면 아무 것도 배울 수 없더라. 여기에 구루 한 명이 붙어서 당신의 코드를 리뷰해줄 수 있다면, 학습 속도는 훨씬 빨라질 것이다. (사실 필자는 구루 덕을 많이 봤다.)

물론 이 방법에도 단점은 있다. 공부하면서 코드를 만들면 어느정도 숙달된 상황에서의 코드와 초기에 짠 코드가 굉장히 다른 스타일로 나온다. 리팩토링은 필수라는 뜻이다. 테스트를 짜거나, 리팩토링을 진행한 후 속출하는 버그를 보고 QA팀에게 비난을 받거나. 두 가지의 선택지가 있다. 필자는 어떻게 했을까? 이 자리를 빌려 QA팀에게 사과의 말씀을 드린다는 말로 답을 대신한다.

#### jQuery로 고통받기에 당신의 시간과 정신 건강은 너무 아깝지 않은가?

웹에 관심이 있으시다면 지금 당장 지금의 기술에 도전해보자. IE8 지원을 끊는 것을 심각하게 고민해볼 수 있는 지금같은 시점에, jQuery로 고통받기에 당신의 시간과 정신 건강은 너무 아깝지 않은가.
