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
  
