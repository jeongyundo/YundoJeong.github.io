---
layout: post
title: PuzzleReact-3
tags:
  - React
---
<h1>도화지 위의 퍼즐, React [3]</h1>
어떻게 퍼즐조각을 만드는가?

<h2>번거로움을 쉽게 조각들로만 대체</h2>

![20190801screenshot1](/Users/jeong-yundo/Desktop/20190801screenshot1.png)

위의 화면을 예시로 들어 얘기를 하겠다.

현재 이 화면은 필자가 좋아하는 뮤지컬과 연극 그리고 콘서트에 대한 예매까지 시간을 남겨놓은 웹사이트이다. 이 작업을 하기 위해서 앞서 말했듯이 HTML, CSS, JavsScript에 대한 이해가 필요하다. 그리고 위의 코드는 굉장히 지저분하다. 일부로 이해를 위해서 노가다로 하나하나 작업을 했다. 얼마나 보기 껄끄러운지는 맨밑에 파일 코드를 올려놨으니 보면은 '정말 지저분하게 했구나'라는 생각을 하며 이 작업이 얼마나 귀찮은지 알 수 있다.

상단의 이미지파일에서 우리는 크게 2가지로 나누어서 확인할 수 있다. 상단의 time left구역과 그리고 공연정보가 표시된 구역으로 나눌 수 있다. 그리고 공연정보 구역은 4가지 다른 공연들로 나눌 수 있으며 이는 다시 나머지 화면의 포스터, 공연정보, 그리고 남은 시간을 표시해주는 화면들로 구성되어 있다. 이렇게 나누어진 정보들을 하나하나 입력하는것은 굉장히 귀찮다. 일일이 정보를 기입해준다면, 화면은 하나의 값만 가지고 멈춰있는 모습을 갖추게된다. 

위에는 나타나지 않지만 우리가 여기서 뮤지컬만 보고싶다면, 혹은 연극만 아니면 8월행사만 보고싶다면, 우리는 화면을 변동해주어야 한다. 그렇다면 그때그때마다 html을 수정해주어야한다.  그럴떄 우리는 react를 이용해 퍼즐조각을 만들어놓고 원하는 모습때마다 값을 불러오게 할 수 있다. 이는 추후에 다루도록 하겠으며, 이 글에서는 일단 퍼즐을 나누어 만드는것부터 보여주도록 하겠다.

---

html파일

```html
<!doctype html>
<html>
  <head>
    <link rel="stylesheet" href="test0731.css">
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <title>Hello HTML</title>
    
  </head>
  <body>
    
    <div class="Title">Time Left</div>
    <div class="App">
        <div class="Content"> 
            <div class="Content__Column">
                <img src="img/poster2.jpg" class="Content__Poster" />
            </div>
            <div class="Content__Column">
                <h1>스위니토드</h1>
                <div class="Content__Genres">
                    뮤지컬
                </div>
                <div className="Content__Synopsis">
                        2019년 8월 7일(수) 오후 2시
                        <p id="demo1">2019년 8월 7일(수) 오후 2시</p>
                </div>
            </div>
        </div>
        <div class="Content">  
            <div class="Content__Column">
                <img src="img/poster1.jpg" class="Content__Poster" />
            </div>
            <div class="Content__Column">
                <h1>마리 앙투아네트</h1>
                <div class="Content__Genres">
                    뮤지컬
                </div>
                <div className="Content__Synopsis">
                        2019년 8월 6일(목) 오후 2시
                        <p id="demo2">2019년 8월 6일(목) 오후 2시</p>
                </div>
            </div>
        </div>
        <div class="Content"> 
            <div class="Content__Column">
                <img src="img/poster3.jpg" class="Content__Poster" />
            </div>
            <div class="Content__Column">
                <h1>BTS WORLD TOUR ＇LOVE YOURSELF: SPEAK YOURSELF＇</h1>
                <div class="Content__Genres">
                    콘서트
                </div>
                <div className="Content__Synopsis">
                        2019년 9월 26일(목) 오후 8시
                        <p id="demo3">2019년 9월 26일(목) 오후 8시</p>
                </div>
            </div>
        </div>
        <div class="Content"> 
                <div class="Content__Column">
                    <img src="img/poster4.jpg" class="Content__Poster" />
                </div>
                <div class="Content__Column">
                    <h1>〈장수상회〉 - 수원</h1>
                    <div class="Content__Genres">
                        연극
                    </div>
                    <div className="Content__Synopsis">
                            2019년 8월 12일(월) 오전 9시
                        <p id="demo4">2019년 8월 12일(월) 오전 9시</p>
                    </div>
                </div>
            </div>
    </div>
    <script src="practice.js"></script>
  </body>
</html>
```

css파일

```css
body {
    background-color: white
}

.App {
    padding: 50px;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    font-size: 14px;
}

.Title {
    color: black;
    text-align: center;
    font-size: 8em;
    margin-block-start: 0em;
    margin-block-end: 0em;
    background: whitesmoke;
}

.Content{
    background-color:white;
    width:40%;
    display: flex;
    justify-content: space-between;
    align-items:flex-start;
    flex-wrap:wrap;
    margin-bottom:50px;
    text-overflow: ellipsis;
    padding:0 20px;
    box-shadow: 0 8px 38px rgba(133, 133, 133, 0.3), 0 5px 12px rgba(133, 133, 133,0.22);
}

.Content__Column{
    width:30%;
    box-sizing:border-box;
    text-overflow: ellipsis;
}

.Content__Column:last-child{
    padding:20px 0;
    width:60%;
}

.Content h1{
    font-size:20px;
    font-weight: 600;
}

.Content .Content__Genres{
    display: flex;
    flex-wrap:wrap;
    margin-bottom:20px;
}

.Content__Genres .Content__Genre{
    margin-right:10px;
    color:#B4B5BD;
}

.Content .Content__Synopsis {
    text-overflow: ellipsis;
    color:#B4B5BD;
    overflow: hidden;
}

.Content .Content__Poster{
    max-width: 100%;
    position: relative;
    top:-20px;
    box-shadow: -10px 19px 38px rgba(83, 83, 83, 0.3), 10px 15px 12px rgba(80,80,80,0.22);
}

@media screen and (min-width:320px) and (max-width:667px){
    .Content{
        width:100%;
    }
}

@media screen and (min-width:320px) and (max-width:667px) and (orientation: portrait){
    .Content{
        width:100%;
        flex-direction: column;
    }
    .Content__Poster{
        top:0;
        left:0;
        width:100%;
    }
    .Content__Column{
        width:100%!important;
    }
}
```

Javascript파일

```javascript
function setDate(needs) {
    let nowDate = new Date();
    let dueDate = new Date(needs.year, needs.month, needs.days, needs.hours, needs.minutes);
    let countDate = new Date(dueDate-nowDate);
    let minutes = parseInt((dueDate-nowDate)/(1000*60));
    let hours = parseInt(minutes/60);
    let dividedHours = hours%24;
    let dividedDays = parseInt(hours/24)-31;
    let divededMinutes = minutes%60;
    console.log(nowDate, dueDate, countDate);
    let result = {"days": dividedDays, "hours": dividedHours, "minutes": divededMinutes}
    return result
}

var a = {"year": 2019, "month": 8, "days": 7, "hours": 14, "minutes": 00};
var b = {"year": 2019, "month": 8, "days": 6, "hours": 14, "minutes": 00};
var c = {"year": 2019, "month": 9, "days": 26, "hours": 20, "minutes": 00};
var d = {"year": 2019, "month": 8, "days": 12, "hours": 9, "minutes": 00};

var a1 = {"day":setDate(a),"id":"demo1"};
var a2 = {"day":setDate(b),"id":"demo2"};
var a3 = {"day":setDate(c),"id":"demo3"};
var a4 = {"day":setDate(d),"id":"demo4"};

function writedata(value) {
    console.log(value);
    console.log(document.getElementById(value.id));
    document.getElementById(value.id).innerHTML = "남은시간 : "+value.day.days+"일"+value.day.hours+"시간"+value.day.minutes+"분";
}

window.onload=writedata(a1);
window.onload=writedata(a2);
window.onload=writedata(a3);
window.onload=writedata(a4);
```