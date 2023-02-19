# Study-React
리액를 공부해보아요

## 엘리먼트 만들고, 이벤트 추가하기


- 강의는 React 17버전 기준, cdn에서 React 18버전을 사용하니 에러메세지가 떴다.

![image](https://user-images.githubusercontent.com/112043767/219855017-90d59984-7337-4ce4-86de-d75fdc951c7e.png)

- ReactDOM.render 대신 createRoot를 권장하는 이유
  - 더 나은 Root API의 사용
  - Hydration
  - Render Callback
  
```Javascript
const root = document.getElementById("root");
const title = React.createElement("h3", 
                                  { id: "cute-span", 
                                    style: {color : 'pink'},
                                    onMouseEnter: () => console.log("mouse enter"),
                                   }, 
                                    "Hello I'm a span");
const btn = React.createElement("button",{
    onClick: () => console.log("i'm clicked"),
}, "Click me");
const container = React.createElement("div", null, [title, btn] );
ReactDOM.createRoot(root).render( [btn, title])
```


  
![image](https://user-images.githubusercontent.com/112043767/219856628-e831bd17-c2a9-4cc0-bce3-853a2a426a8b.png)
![image](https://user-images.githubusercontent.com/112043767/219856902-425a0825-3d37-4f78-82f7-c949cd1439bc.png)

- 😎 쨘, 이벤트가 달린 엘리먼트가 만들어졌다.
- React의 장점 중 하나는 vanila js로 엘리먼트를 만들고, 이벤트를 추가하는 방식이 완전히 뒤집힌다는 것이다.
- Vanila JS로 엘리먼트를 만들때에는 HTML으로 엘리먼트를 만들고 👉🏻 그 후에 DOM을 조작하여 해당 엘리먼트를 가져오고 👉🏻 그 이후 이벤트를 등록 하는 순서이지만
- React에서는 react 문법을 통해서 엘리먼트를 생성함과동시에 이벤트, 속성을 자유롭게 추가할 수 있다. 👉🏻 그 후에 body에 포함된다 (react DOM 을 이용)


- 이렇게 만들고 나니 오류가 떴는데 🤔 공식문서를 찾아보니 key를 사용하는 이유는 아래와 같다.
- Keys : Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity:

```Javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

- 📌 Key의 필요성은 이해하는데, 매번 꼭 사용해야하는 건지 궁금해져서 이건 나중에 적용해보도록 한다.

## createElement() 대체 👉🏻  JSX

- JSX: HTML의 문법과 비슷하게 Javascirpt문법으로 element를 생성해준다.

```Javascript
        const Title = <h3 id="title" 
                        onMouseEnter={() => console.log("mouse enter!")}>
                        Hello I'm a title</h3>
        const Button = <button id="btn"
                        style = {{
                            backgorundColor: "pink",
                        }}
                        onClick = {() => console.log("button clicked")}>
                        Click me
                        </button>
```

- 이렇게 까지만 하면, \브라우저가 jsx를 완전히 이해하지 못했기 때문에 error
- babel을 사용해서 createElement() 를 이용하는구문으로 변환
- 똑같이 사용하되, script에 text/babel 명시만 해주면된다.
- JSX 문법으로 작성후, 함수로 만들면 컴포넌트화가 가능해져서 HTML 태그처럼 사용가능하다.

```Javascript
<script type="text/babel">
      const root = ReactDOM.createRoot(document.getElementById('root'));
        const Title = () => ( <h3 id="title" 
                        onMouseEnter={() => console.log("mouse enter!")}>
                        Hello I'm a title</h3>
        )
        // 함수로 만들어서 컴포넌트화 시키고, 태그처럼 포함가능하다
        const Button = () => ( <button id="btn"
                        style = {{
                            backgorundColor: "pink",
                        }}
                        onClick = {() => console.log("button clicked")}>
                        Click me
                        </button>)
                        //일반 HTML태그는 소문자로 시작, 컴포넌트는 대문자로
        const Container = () => ( <div>
                <Title />
                <Button />
            </div> )
        root.render(<Container />)
    </script>
```

## 화면에서 필요한 부분만 다시 render하고 싶을 때, state!

- 자동으로 render를 해야하는 trigger가 되어주는것이 state
- React.userState()를 사용하면 내가 바꾸고싶은 데이터와 그 데이터를 바꿀 때 사용하는 함수 정의가 가능
- const data = React.userState(0); -> 이름을 다시 붙이려면 귀찮아진다 ex) const counter = data[0]
- 조금 더 직관적인 코드는 const [counter, setCounter] = React.userState(0)


```Javascript
  const root = ReactDOM.createRoot(document.getElementById('root'));
        function App() {
            // Array를 받게됨 [undefined, f]
            // undefined -> 내가 사용할 data / f -> data를 바꿀 때 사용하는 함수 / 초기값 설정가능
            // const data = React.useState(0);
            //Better way
            const [counter, setCounter] = React.useState(0);
            const onClick = () => {
                setCounter(counter+1);
            };
            return (
                <div>
                    <h3>Total clicks: {counter}</h3>
                    <button onClick={onClick}>Click me</button>
                </div>
            )
        }
        root.render(<App />)
```
