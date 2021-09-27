---
layout: post
title:  "[Computer Science] Functional Programming"
subtitle:   "P"
categories: dev
tags: etc   
comments: true
---


## 개요
> Functional programming is a programming paradigm where programs are constructed by applying and composing functions.
  
- 목차
	- [함수형 프로그래밍이란](#함수형-프로그래밍이란) 
    - [함수형 프로그래밍의 특징](#함수형-프로그래밍의-특징)
    - [부수 효과란](#부수-효과란)
	- [순수 함수란](#순수-함수란)
	- [순수 함수의 특징](#순수-함수의-특징)
	- [함수형 프로그래밍의 예시](#함수형-프로그래밍의-예시)
    - [JS Collection Interface](#JS-Collection-Interface)


## 함수형 프로그래밍이란
부수 효과(side effect)를 없애고 순수 함수(pure function)를 만들어 모듈화 수준을 높이는 프로그래밍 패러다임입니다. 


## 함수형 프로그래밍의 특징
- 부수 효과가 없다.
- 순수 함수를 지향한다.
- 함수 외부 데이터에 의존하지 않는다.
- 함수 외부 데이터를 변경하지 않는다.


## 부수 효과란
함수로 들어온 인자의 상태가 변경되거나 함수 외부의 상태가 변경되는 효과이다.


## 순수 함수란
부수 효과가 없는 함수이다. 즉, 동일한 인자를 주었을 때 항상 동일한 값을 반환하는 함수이다.


## 순수 함수의 특징
- 작성한 함수가 반드시 하나 이상의 인자를 받아야 한다.
- 반환값이 반드시 존재해야 한다.
- 함수 내에서 인자를 제외한 다른 변수를 사용하면 안 된다.
- 동일 입력에 대한 동일 출력이 보장되어야 한다.
- 평가 시점이 중요하지 않아야 한다.


## 함수형 프로그래밍의 예시

### Wrong Example 1
```js
const arr = [1, 2, 3, 4, 5];
const condition = function(x) {return x % 2 === 0}
const ex = function(array) {
    return array.filter(condition);
};
ex(arr); // [2, 4]
```

ex 함수가 인자로 받지 않은 condition 변수를 사용하고 있다.

### Correct Example 1
```js
const ex = function(array, cond) {
	return array.filter(cond);
};
ex(arr, condition);
```

condition 변수를 인자로 받는 순수 함수가 되었다. 이를 통해 에러 추적이 한결 쉬웠졌다.

### Wrong Example 2
```js
let sum = 0;
for (let i = 1; i <= 10; i++) {
  sum += i;
}
```

순수함수를 만들 때엔 반복문을 쓰지 않는게 좋다.

### Correct Example 2-1
```js
function add(sum, count) {
    sum += count;
    if (count > 0) {
        return add(sum, count - 1);
    } else {
        return sum;
    }
}
add(0, 10); // 55
```

인자로 받은 sum과 count만 활용했기 때문에 순수함수이다.

### Correct Example 2-2
```js
const arr = [1,2,3,4,5,6,7,8,9,10];
const answer = arr.reduce((pre, cur) => {
	return pre + cur;
});	
console.log(answer); // 55
```

위 코드를 고차 함수인 reduce를 활용해서 간결하게 만들었다.

### Wrong Example 3
```js
let a = 0;

function increment() {
    return a += 1;
}
```

increment 함수가 외부 데이터 변수인 a에 의존하고 있다.

### Correct Example 3
```js
increment(a) {
	return a + 1;
}
```

인자로 받은 a와 상수 1만 활용했기 때문에 순수 함수이다.


## JS Collection Interface

아래의 함수들은 함수형 프로그래밍의 개념에 따라 기존 변수에 대한 부수 효과가 없도록 구현되었다.

### map
```js
const arr = ['foo', 'hello', 'diamond', 'A'];
const arr2 = arr.map((v) => v.length);
console.log(arr2) // [3, 5, 6, 1]
```

### filter
```js
const arr = [4, 15, 377, 395, 400, 1024, 3000];
const arr2 = arr.filter((v) => (v % 5 === 0));
console.log(arr2) // [15, 395, 400, 3000]
```

### reduce
```js
let arr = [9, 2, 8, 5, 7];
let sum = arr.reduce((pre, val) => pre + val);
console.log(sum) // 31
```