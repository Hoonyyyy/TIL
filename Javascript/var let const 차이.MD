# var let const 차이.MD

### var
- 중복 선언 가능, 재할당 가능
```script
var title = 'book';
console.log(title); // book

var title = 'food';
console.log(title); //movie

title = 'music';
console.log(title);//music
```

### let
- 중복 선언 불가, 재할당 가능
```script
let title = 'book';
console.log(title); // book

let title = 'movie';
console.log(title); 
//Uncaught SyntaxError: Identifier 'title' has already been declared

title = 'music';
console.log(title);//music
```

### const
- 중복선언 불가, 재할당 불가
```script

const title = 'book';
console.log(title); // book

const title = 'movie';
console.log(title); 
//Uncaught SyntaxError: Identifier 'title' has already been declared

title = 'music';
console.log(title);
//Uncaught TypeError: Assignment to constant variable
```
