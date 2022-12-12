<2강>
npx: npm 패키지 설치 + 실행까지 한번에 해주는 명령어
(안그러면 직접 패키지 설치 위치 지정하고 해당 위치로 이동해서 실행해야 함)

<3강>
JSX
- a syntax extension to JavaScript: 자바스크립트의 확장문법
- JSX = JS + XML/HTML
ex) const element = <h1>Hello, world!</h1> <= jsx문법

JSX의 역할
- XML/HTML 코드를 내부적으로 js로 변환시켜준다
=> 따라서 jsx 코드로 작성해도 최종적으로는 js가 된다.
- jsx 코드를 js 로 변환시켜주는 함수가 React.createElement이다.

React.createElement의 구조는 아래와 같다.
React.createElement(
    type,
    [props],
    [...children]
)


React Component는 붕어빵 틀, Component로 만든 게 element다.
element는 immutable, 즉 바뀌지 않는다. 
리렌더링할 때마다 새로운 element가 생성되는 것이다.

React 컴포넌트는 반드시 대문자로 시작해야 한다.
그렇지 않으면 Dom tag랑 혼동되고 오류로 인식하는 등등 문제가 된다.

<State>
- React State는 하나의 js객체ㅇㅇ
- 렌더링이나 데이터 흐름에 사용되는 값만 State에 포함시켜야 함
=> state가 변경되면 Component가 재렌더링되기 때문에 위와 관련없는 것에 state를 포함시키면 불필요한 재렌더링이 발생해서 성능 저하ㅇㅇ
- state는 직접 수정하면 안된다(가능은 하지만 안된다. setState를 사용해야 함)

- function Component는 class Component와는 달리 life-cycle가 없어서 useState라는 훅(Hook)을 사용해야 한다.

<react Component의 life-cycle>

사람의 life-cycle
: 출생 -> 인생 -> 사망


<useEffect()>
: side effect를 일으키는 훅
(보통 부정적 의미로 쓰이지만, react에선 그냥 효과, 영향 정도를 뜻함)
=> 다른 컴포넌트에게 영향을 미칠 수 있으며, 렌더링이 끝난 이후에 실행됨ㅇㅇ
(Class Component에서의 ComponentDidMount, ComponentDidUpdate, ComponentWillUnMount의 기능들을 통합한 것같은 역할을 수행함)
 
useEffect(이펙트 함수, 의존성 배열)
useEffect(이펙트 함수, []) <- mount, unmount 시 단 한번씩만 실행(ComponentDidMount & ComponentWillUnMount)
useEffect(이펙트 함수) <- Component가 랜더링될때마다 반복 실행(ComponentDidMount & ComponentDidUpdate)

<useMomo()>
: Memoized value를 return하는 훅
- Memoizatnion: 비용이 높은(연산량이 많은) 함수의 호출 결과를 저장해놨다가 같은 입력 값으로 함수를 호출하면 새로 호추랗지 않고 이전에 저장해놨던 호출결과를 바로 반환.
=> 컴퓨터에서 최적화를 위해 사용하는 개념 
=> 시간 절약, 불필요한 중복연산 방지(컴퓨터 자원 절약)
=> 메모해뒀다가 나중에 다시 사용ㅇㅇ..

- useMemo 훅은 의존성 변수값이 바뀔 때에만 다시 연산을 하고, 그렇지 않으면 재연산 없이 이전 연산의 값을 return한다.(랜더링 속도 향상)

- useMemo로 전달되는 함수는 렌더링이 일어나는 동안에 실행됨.
=> 따라서 용도에 따라 useEffect랑 잘 구분해서 사용해야 함

- useMemo는 의존선 변수가 없으면 마찬가지로 렌더링 할 때마다 계속 실행되는데, 그렇게 되면 이 훅을 사용하는 의미가 X.

<useCallback()>
- useMemo() 훅과 비슷. 차이점은 value가 아닌 함수를 반환
- 의존성 값이 바뀔 때만 함수를 새로 정의해서 return.

<useRef()>
- 레퍼런스를 사용하기 위한 훅
react에서 레퍼런스란?
=> 특정 컴포넌트에 접근할 수 있는 객체

 reference에는 current라는 속성이 있다.
 => 현재 레퍼런스하고 있는 element를 의미.


 <훅 사용시 주의사항>
 - React 함수 컴포넌트에서만 Hook을 호출해야 한다.
 - Hook은 무조건 최상위 레벨에서만 호출해야 한다.

 eslint-plugin-react-hooks
 - 훅이 규칙을 따르도록 강제해주는 플러그인 <- 유용함.


<Custom Hook>
: 직접 만드는 훅
- 꼭 use로 시작해야 한다.

<react 이벤트 handling>
- class 컴포넌트에서 사용하려면 함수를 정의한 후 아래와 같이 바인딩해줘야 한다.
this.handleClick = this.handleClick.bind(this)
=> js에선 클래스 함수들이 바운드되지 않기 때문에 bind를 따로 안해주면 글로벌 스코프에서 호출되는데, 글로벌 스코프에서 this.handleClick은 undefined라고 함.
그래서 에러를 일으킴.

- function 컴포넌트에선 event handler를 정의하려면,
함수 안에 또다른 함수로 정의하거나 arrow function을 사용해 정의할 수 있음.


* truthy & falsy 개념 공부해보기(재밌음)


<React 렌더링이 두 번 발생하는 이유>

렌더링이 두 번 발생하는 이유는 React.StrictMode 때문이다.

npx create-react-app 으로 react App을 생성하면 해당 부분이 자동 설정이 돼있음.
따라서 index.js 에서 이 Wrapper를 제거해주면 컴포넌트가 두번씩 호출되지 않음.

StrictMode는 애플리케이션 내의 잠재적인 문제를 알아내기 위한 도구이다.
Fragment와 같이 UI를 렌더링하지 않으며, 자손들에 대한 부가적인 검사와 경고를 활성화함.
Strict 모드는 개발 모드에서만 활성화되기 때문에, 프로덕션 빌드에는 영향을 끼치지 않음.


StrictMode는 다음과 같은 부분에서 도움이 된다.

-안전하지 않은 생명주기를 사용하는 컴포넌트 발견
-레거시 문자열 ref 사용에 대한 경고
-권장되지 않는 findDOMNode 사용에 대한 경고
-예상치 못한 부작용 검사
-레거시 context API 검사