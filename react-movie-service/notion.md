# (React) 영화 웹 서비스 만들기_2021 of nomadcoders
last update: 30.oct.2023

## 1. Introduction

브라우저 chrome
텍스트에디터 vscode

## 2. Basics of React

**0. Introduction**
    
  ReactJS의 point를 알아보자. 어떤 문제를 해결하기 위한 솔루션인지. 
  그래서 Vanilla JS와 React JS를 비교해 볼것이다. 버튼을 클릭할 때 마다 텍스트를 업데이크하는 어플리케이션을 만든다고 가정해보자.  
  - 바닐라JS에서는 HTML에 버튼을 하나 만들고, 버튼을 찾기위해 id나 class를 부여한다. 그리고 Javascript에서 document.getElementById 나 querySelector를 사용해서 버튼을 찾고, button.addEventListener를 통해 function을 실행시킨다.
  - ReactJS는 이러한 작업에서 필요한 것들을 알고, 지름길을 만들어주었다.

**1. Before React : `create JavaScript -(render)→ show HTML`**
    
  Vanilla JS로 application을 만들면서, ReactJS에서 개선할수 있는 점들을 알수있다.     
  
  in Vanilla JS 
  1. HTML에서 button 만들고
  2. Javascript에서 button을 가져와
  3. click event 감지
  4. 데이터 업데이트
  5. HTML 업데이트
    
  ```html
  <html>
    <body>
      <button id="btn">Click Me</button>
      <span>total clicks: 0</span>
    </body>
    <script>
      let counter = 0;
      const button = document.getElementById("btn");
      const span = document.querySelector("span");
      function handleClick() {
        //console.log("i have been clicked");
        counter = counter + 1;
        span.innerText = `total clicks: ${counter}`;
      }
      button.addEventListener("click", handleClick);
    </script>
  </html>
  ```
    
  React code를 쓰기 위해서 두가지를 import해야한다. 
    
  ```html
    <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  ```
    
**2. Our First React Element : `const element = React.createElement("html tag", {props}, [content]);`**
    
  ReactJS의 규칙 중 하나는 HTML을 HTML > body 에 작성하지 않는다. 대신 javascript code에 직접 작성한다. 
    
  ***ReactJS로 element를 생성하는 방법 (어려운거 먼저 - 어려워서 개발자들은 잘 사용하지 않는다.)***
    
  > 🆙 reactJS은 application이 매우 interactive하도록 만들어주는 library이고, react-dom은 library 또는 package인데, 모든 react element들을 HTML body에 둘수 있도록 해준다. react와 react-dom은 완전히 다른 역할을 하는 것이다. **react js는 interactive한 UI를 만들어주는 엔진과 같은 것**이다. **react-dom은 react element를 html에 두는 역할**을 하는 것이다.
    
  (1) `React.createElement("span", {id:"special-span"}, "Hello, I'm a span");`  
  - 첫번째 Argument는 ***tag name***. HTML tag와 같은 이름으로 element를 생성.
  - 두번째 Argument는 element의 ***property들***(class name or id). ***props***가 포함된 object.
  - 세번째 Argument는 element의 ***content***. 
    
  > 🆙 props에서 id나 class를 바꿀수 있어, style도 바꿀수 있어. HTML tag가 input이라면 placeohlder등 무엇이들 바꿀수 있어. !!!!!중요한 것은, event listener를 추가할수 있다는 것이다!!!!!
    이것이 reactJS가 태어난 이유이다. interactive application을 위해서 제작된 library이다.
    
  (2) `ReactDOM.render(span, root)` render의 의미는 react element를 가지고 HTML로 만들어 배치한다는 것.
      render(무엇을, 어디에) 두고 사용자에게 보여줘라.
    
  > 🆙 바닐라JS에서는 HTML을 먼저 만들고, 그걸 Javascript로 가져와서, HTML을 수정. ReactJS에서는 JavaScript에서 시작해. 그 다음에 render()로 HTML이 되는 거야. 이것이 React JS의 핵심이다. javascript에서 유저에게 보여질 내용을 모두 컨드롤할 수 있다는 것이다. 
    
    
**3. Events in React : `event listenet in Props`**
    
  버튼을 만들고, 버튼에서 일어나는 event를 어떻게 감지하는지도 알아보자. 
    
  element(component)의 두번째 argument에 class name이나 sytle말고도 eventListener Function을 추가할수 있다. 
    
  ```jsx
  // react JS
  const btn = React.createElement(
    "button",
    { **onClick** : () => console.log("i'm clicked!"),},
    "Click Me!"
  ); 
  ```
    
  ```jsx
  // vanilla JS
  // body
  <button id="btn">Click Me</button>
  // script
  const button = document.getElementById("btn");
  button.addEventListener("**click**", handleClick);
  ```
    
  이것이 ReactJS의 Power이다. element를 만들면서 내부에 content도 넣고, event listener까지 장착. 
    
  vanillaJS에서는 `click` 이지만, reactJS에서는 앞에 `on` 을 씀으로써 event listener을 생성한다고 알린다. 
    
  (1) createElement
    
  (2) choose HTML tag, write event
    
**4. Recap**
    
  (1) import reactjs and react-dom: 
  - reactJS는 create element, add event listener. → **Power of Interactivity**! that’s POWER of reactjs
  - react-dom은 react element → html : `ReactDOM.render(container, root);`
    
  (2) create Elements
  - with (HTML Tag, {props(class, id, style, **eventlistener**, …)}, [content])
    
**5. JSX : `const element = () => (<span></span>);`**
    
  react.createElement로 element를 만들던 방법을 더—— 쉽게 바꿔보자.
    
  JSX는 javascript를 확장한 문법이다. 기본적으로 react element를 만들 수 있게 해주는데, html 문법과 유사한 문법을 사용한다. 
    
  ```
  // 어려운 방법, 그러나 원리를 이해하는데 도움
  const Title = React.createElement(
    "h3",
   	{onMouseEnter: () => console.log("mouse enter")},
    "Hello, I'm a span"
  );
  ```
    
  ```
  // 쉬운 방법, 주로 이렇게 사용
  const Title = (
  	<h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
  		Hello, I'm a span
  	</h3>
  );
  ```
    
  JSX는 React.createElement() call : 아래 왼쪽코드를 아래 오른쪽코드롤 바꿔주지. 그러기위해 babel을 사용한다. 
    
  ```
  const element = (
    <h1 className="greeting">
      Hello, world!
    </h1>
  );
  ```
  
  ```
  const element = React.createElement(
    'h1',
    {className: 'greeting'},
    'Hello, world!'
  );
  ```
  
  Babel은 코드를 변환해주는데(transformer), 우리가 JSX로 적은 코드를 브라우저가 이해할 수 있는 형태로 바꿔주는 것이다. 
  
  Babel을 import 해주고 웹페이지 검사 > elements를 보면,
  body > script에는 우리가 babel에 넘겨준 코드가 있고, 그걸 babel이 브라우저가 읽을 수 있는 코드로 바꿔서 head에 담아둔걸 확인할 수 있다. 
    
**6. JSX part 2 : our component inside in other component**
    
  ```
  const container = React.createElement("div", null, [Title, Button]);
  ```
  
  위의 코드를 JSX를 사용해서 작성해보자.  Title과 Button을 rendering 하는 (Component) Container .
  
  ```
  const Container = (
    <div>
      <Title />
      <Button /> //이건 내가 생성한 버튼
      <butten>hello</button> // 이건 HTML element
    </div>
  );
  ```
    
  > 🆙 중요한 것은, Component의 첫글자는 반드시 대문자여야 한다!! 소문자로 쓰면 html tag라고 생각한다. 
    

## 3. State 0 1 2 3 4 5 6 7 8 9

**0. Inderstanding State**
    
    

## 4. Props 0 1 2 3

## 5. Create React App 0 1

## 6. Effects 0 1 2 3 4

## 7. Practice Movie App 0 1 2 3 4 5 6 7 8 9 10
