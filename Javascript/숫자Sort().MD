# 숫자Sort()

숫자도 문자로 인식하기에 숫자를 sort() 하면 다르게 나온다 그렇기에 이런식으로 해야함

```html
let arrNumber = [17, 2, 119, 55, 410, 6];
arrNumber.sort((a,b)=>a-b);
console.log(arrNumber); // [2, 6, 17, 55, 119, 410]
```
