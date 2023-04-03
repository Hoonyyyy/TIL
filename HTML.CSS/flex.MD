## flexgrow와 flex-shrink
유연한 레이아웃을 가능하게 하는 중요한 속성 2가지

### flex-grow
- 레이아웃 안에서 알맞게 들어가게 해줌
```html
.flexbox{
    display: flex;
    flex-wrap: nowrap;
    gap: 0;
    padding: 10px;
    background-color: #e8e8e8;
}
.item{
    min-height: 150px;
    flex-basis: 100px;
}

.item:nth-child(1){flex-grow: 1;}
.item:nth-child(2){flex-grow: 1;}
.item:nth-child(3){flex-grow: 0;}
.item:nth-child(4){flex-grow: 2;}


<div class="layout">
    <div class="flexbox">
        <div class="item">content1</div>
        <div class="item">content2</div>
        <div class="item">content3</div>
        <div class="item">content4</div>
    </div>
</div>
```

### flex-shrink
- 속성이 레이아웃을 벗어난 아이 너비를 분배해서 줄이는방
```html
.layout{
    max-width: 600px;
    margin: 0 auto;
    padding: 0;
}
.flexbox{
    display: flex;
    flex-wrap: nowrap;
    gap: 0;
    padding: 10px;
    background-color: #f0f0f0;
}
.item{
    min-height: 150px;
    flex-basis: 200px;
    flex-shrink: 0;
}

.item:nth-child(1){flex-shrink: 1;}
.item:nth-child(2){flex-shrink: 0;}
.item:nth-child(3){flex-shrink: 1;}
.item:nth-child(4){flex-shrink: 2;}

<div class="layout">
    <div class="flexbox">
        <div class="item">content1</div>
        <div class="item">content2</div>
        <div class="item">content3</div>
        <div class="item">content4</div>
    </div>
</div>
```

출처: https://blogpack.tistory.com/863
