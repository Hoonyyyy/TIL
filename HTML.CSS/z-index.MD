# z-index

https://www.daleseo.com/css-z-index

```
z-index 속성을 사용하면 위에서 다룬 기본적인 규칙을 무시하고 HTML 문서 상에서 먼저 나온 요소를 나중에
나온 요소보다 앞으로 나오게 할 수 있는데요. 브라우저는 z-index 속성값이 낮은 요소를 먼저 그리고, z-index 속성값이 높은
요소를 나중에 그리기 때문에 요소가 겹쳐있을 경우 z-index 속성값이 큰 요소가 z-index 속성값이 작은 요소의 일부를 가리거나
전체를 덮을 수 있습니다. (물감을 계속 덫칠한다고 생각하시면 이해가 쉬우실 것 같네요
```

# z-index를 너무 남용하면 유지보수가 매우 힏믈어지기에 가급적 사용하지 않는편이 좋긴하다.

## 물감을 덫칠한다.

### position 속성이 static인 요소에는 z-index 속성이 아무 효력을 내지 못한다.
- 왜냐하면 position 속성이 static인 요소는 z-index 속성이 auto, 즉 0으로 고정되어 있음
- 두번째 요소에 position: reliative를 제거하면 다시 첫번째 상자가 앞으로 나옴

### z-index
~~~
HTML의 기본적인 규칙을 무시하고 HTML 문서 상에서먼저 나온 요소를 나중에 나온 요소보다 앞으로 나오게 한다.
브러우저는 z-index 속성값이 낮은 요소를 먼저 그리고, z-index 속성값이 높은 요소를 나중에 그리기에
요소가 겹쳐 있을 경우 z-index 속성값이 높은 요소를 나중에 그리기 때문에 요소가 겹쳐 있을 경우 z-index속성
값이 큰 요소가 z-index 속성값이 작은 욧의 일부를 가리거나 전체를 덮을 수 있더.
~~~


## 예제 1)
~~~HTML
.first.box {
  z-index: 1;
  background: yellow;
  position: relative;
  top: 50px;
  left: 50px;
}

.second.box {
  z-index: 2;
  background: tomato;
  position: relative;
}

.box {
  width: 200px;
  height: 200px;
  border: 2px solid;
  font-size: 2rem;
  text-align: center;
  line-height: 200px;
}
~~~

## stacking context : z-index가 비교되는 범위
- z-index가 HTML 문서 전체 범위에서 비교된다고 생각하면 안됨
- 특정 범위 내에서 비교되며, 이것을 CSS에서는 ***stacking context***

예제 2)
~~~html

<div class="wrapper">
  <div class="first box">1</div>
</div>
<div class="second box">2</div>


.wrapper {
  z-index: 1;
  position: relative;
}

.first.box {
  z-index: 100;
  background: yellow;
  position: relative;
  top: 50px;
  left: 50px;

.second.box {
  z-index: 2;
  background: tomato;
  position: relative;
}

}
~~~
