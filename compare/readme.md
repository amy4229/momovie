# 바닐라js와 리액트, 리액트의 jsx의 차이를 보기 위한 구현

\*\* 리액트 프로젝트시
리액트 참고주소:https://nomadcoders.co/react-for-beginners/lectures/3260

리액트 CDN주소

<script src="https://unpkg.com/react@17/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js" crossorigin></script>

리액트는 HTML소스를 직접 생성하지 않는다.
React.createElement(something) 으로 컴포넌트를 생성한다.

const label = React.createElement(
      "h3",
      {
        id: "title",
        onMouseEnter: () => {
          console.log("mouse enter");
        },
      },
      "Hello I'm a title"
    );
  const container = React.createElement("div", null, [label, button]);
    ReactDOM.render(container, root);

ReactDOM.render()함수로 브라우저 화면에 컴포넌트를 출력하게 해준다.

react js library는 interactive한 UI, UX들을 제공하는 엔진같은 라이브러리
reactDOM은 react element를 HTML에 붙여주는 라이브러리 혹은 패키지

바닐라js
HTML에 먼저 컴포넌트를 정의하고, javascript가 HTML의 컴포넌트를 찾아가서 이벤트를 추가하고 핸들러를 달아 변화를 준다면

 <script>
    let cnt = 0;
    const button = document.getElementById("button");
    const label = document.getElementById("label");

    function handleClick(){
        cnt+=1;
        label.innerText=`TotalCLick: ${cnt}`;
    }
    button.addEventListener("click",handleClick);
  </script>


react는
javascript에서 요소를 만들고 HTML이 되는 흐름이다.
const label = React.createElement(
      "h3",
      {
        id: "title",
        onMouseEnter: () => {
          console.log("mouse enter");
        },
      },
      "Hello I'm a title"
    );
  const container = React.createElement("div", null, [label, button]);
    ReactDOM.render(container, root);

즉, 다시말해 기존의 바닐라가 이벤트를 정해진 HTML구조에서 이벤트라는 행위를 위한 역할이었다면, 

리액트는 HTML을 직접 만들고, 이벤트도 하는 역할로 비중이 커졌다.



jsx : javascript의 확장된 문법
React의 createElement와 같은 자바스크립트 유사 문법보다는 HTML의 문법과 유사하게 해서 개발자에게 HTML구성을 더익숙한 환경에서 구현할 수 있도록 해주는 문법

jsx로 씌여진 코드를 react문법으로 바꿔주기 위해서 Babel과 같은 툴을 사용해 브라우저가 이해할 수 있는 언어로 변환해주어야한다.

bable
https://babeljs.io/
cdn :

<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

cdn으로 바벨이용시 코드를 작성한 스크립트의 여는 태그에

<script type="text/babel"> 타입지정이 필요 

바벨은 우리가 쓴 스크립트를 브라우저가 읽을 수 있는 코드로 변환해 head에 담아 놓는다. 

jsx를 이용해 작성해놓은 컴포넌트들을 넣기 위해서는 
기존에 태그가 달린 문자열을 함수형으로 바꿔야한다. 
그리고 컴포넌트는 반드시 대문자로 시작해야함!!!!!!!!
왜냐하면 소문자라면 react와 jsx는 컴포넌트로 인식하지 않고 HTML의 태그라고 인식하기 때문


const Title = (
      <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
        Hello I'm a title
      </h3>
    );

변경
 const Title = () => (
      <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
        Hello I'm a title
      </h3>
    );

Container가 

 const Container = ()=> (
      <div>
        <button onClick={() => console.log("I'm hello clicked")}>Hello</button>
        <Title /> 
        <Button />
      </div>
    );
  함수형으로 선언한 컴포넌트를 태그화 해주면 렌더링이 되는 마법!!!!!!!
