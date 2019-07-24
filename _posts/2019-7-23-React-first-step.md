---
layout: post
title: React first step
tags:
  - React
---
<h1>React에 대한 초록</h1>

React를 위해서 선행해야할 공부는 다음과 같다.

1. <b>HTML</b>
2. <b>CSS</b>
3. <b>JavaScript</b>

 html은 도화지와 그 위에 그리는 글, 선 그리고 그림이다. css는 도화지에 표현된 것들의 색, 모습 그리고 크기를 나타낸다. 마지막으로 javascript는 도화지에 여러가지 기능을 추가해준다. 쉽게 얘기해 우리는 기본적으로 도화지를 사용하고 그 위에 건물들을 세우는 연습이 필요하다. 

 필자 역시 한동안 계속 헤매이고 있는 점이며, 자바스크립트에 대한 이해없이 react를 시작하여 제자리걸음을 했다. 물론 현재까지도 온전히 다 안다라고 말하기는 어렵지만, javascript의 선행 없이는 jslint, babel,  등등 이해가 가지 않는 점들이 많다. 그리고 이게 익숙해졌을때 react를 하는편이 좋다고 생각한다.

https://www.w3schools.com/react/default.asp

기본적으로 나의 글을 읽어서 무언가를 따라한다기 보다는 위의 링크에서 튜토리얼을 하는 것이 좋다고 생각한다. 다만 이 글은 주로 쉽고 빠르게 읽는 단순 메뉴얼정도라고 생각해주면 감사하겠습니다!!!

<h2>그렇다면 나는 왜 <b>React</b>를 굳이 공부하는가?</h2>

 다른 이유는 없다. 인기가 있기 때문이다. 대세인것은 이유가 있다고 생각한다. 프로그래밍은 간편하고 쉽게 접근하고 누구나 만들 수 있어야 한다는게 요즘 트렌드인것 같다는 점에서, react를 이용하면 쉽고 빠르게 웹을 만들 수 있을 거라고 생각했기 때문에 시작하였다. 마찬가지로 Angular, vue.js 등등이 있지만, react를 해본것은 온전히 첫 관심이 꽂혔기 때문에 그대로 해본것이다. 빠르고 간편하다면 배우는데도 쉽지 않겠는가? 빠른 시일내로 배울 수 있을 것이다.



<h2>React 설치</h2>

1. node.js 설치

2. npm 설치 (nodejs package module)

3. 실행을 위한 라이브러리 설치

4. 
   ```
   1. create-react-app를 설치(터미널에서 설치가능)
   npm install -g create-react-app
   2. create-react-app를 이용해 myfirstreact라는 이름의 react를 설치 
   npx create-react-app myfirstreact
   ```

![스크린샷 2019-07-23 오후 2.02.56](/images/190723screenshot1.png)

5. myfirstreact 실행

6. 
   ```
   cd myfirstreact
   npm start
   ```



7. 웹에서 localhost:3000 으로 접속시 다음과 같은 화면이 나온다

![스크린샷 2019-07-23 오후 2.04.09](/images/190723screenshot2.png)



<h1>위와 같이 나왔다면 일단 첫걸음은 내딛은 것이다.</h1>

