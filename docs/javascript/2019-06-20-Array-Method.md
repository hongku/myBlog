# Array Method
---
알고는 있고 사용하면 매우 유용함에도 익숙하지않아 자꾸 `for`문으로만 사용하는 습관을 버리기위해 하나씩 살펴보면서 익숙해져보도록 해야겠다

> 이 글에서 Array의 모든 Method를 다루지는 않습니다

- Array.forEach
- Araay.map
- Array.reduce

## Array.forEach

> forEach() 메서드는 주어진 함수를 배열 요소 각각에 대해 실행합니다 [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

```javascript
arr.forEach(callback[, thisArg]);
```
- 배열을 순회하며 element마다 특정 함수(callback)를 실행하려고할때 유용할듯
- **IMMUTABLE**함수. 하지만 callback이 배열을 변형시킬 수는 있음
- callback의 parameter은 `currentValue, index, array`순서대로 받음
  - `currentValue` 현재 순회중인 element
  - `index` 현재 index
  - `array` 배열 자체
- return value: 없음(undefined)

`for`문을 사용하면
```javascript
let arr = ['hello', 'My name is', 'Good bye'];

function addName(str) {
  return str + ' hongku';
}

for (let i = 0; i < arr.length; i++) {
  arr[i] = addName(arr[i]);
}
```
`forEach`를 사용하면
```javascript
let arr = ['hello', 'My name is', 'Good bye'];

function addName(str) {
  return str + ' hongku';
}

arr.forEach((currentElement, index, array) => {
  array[index] = addName(currentElement);
});
```

## Array.map

> map() 메셔드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다.[MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

```javascript
arr.map(callback(currentValue[, index[, array]])[, thisArg])
```

- 기존 배열과 동일한 길이를 갖고, 각 element에 특정 함수를 사용해 변형된 값을 모은 새로운 배열을 얻고자 할때 유용할듯
- **IMMUTABLE**함수
- callback의 parameter은 `currentValue, index, array`순서대로 받음
  - `currentValue` 현재 순회중인 element
  - `index` 현재 index
  - `array` 배열 자체
- callback 내에서 return 필요함
- return value: callback이 실행되면서 return하는 값들을 모은 새로운 배열

`for`문을 사용하면
```javascript
let arr = [1, 2, 3, 4, 5];
let newArr = [];

function multiply(num) {
  return num * 2;
}

for (let i = 0; i < arr.length; i++) {
  newArr.push(multiply(arr[i]));
}

console.log(newArr); // [2, 4, 6, 8, 10]
```
`map`을 사용하면
```javascript
let arr = [1, 2, 3, 4, 5];

function multiply(num) {
  return num * 2;
}

let newArr = arr.map((currentItem, index, array) => {
  return multiply(currentItem);
});

console.log(newArr); // [2, 4, 6, 8, 10]
```

## Array.reduce

> reduce() 메서드는 배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과값을 반환합니다.[MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

```javascript
arr.reduce(callback[, initialValue])
```

- 각 element를 순회하며 이전 element의 리턴값을 넘겨받아 누적 값으로 사용할 경우 유용할 듯
- **IMMUTABLE**함수
- callback의 parameter은 `accumulator, currentValue, index, array`순서대로 받음
  - `accumulator` 누적 값
  - `currentValue` 현재 순회중인 element
  - `index` 현재 index
  - `array` 배열 자체
- callback뒤 parameter(initialValue)로 누적값의 초기 값을 넘겨줄 수 있음(첫 element순회시 사용될 누적 값)
- return value: 최종 누적 값

`for`문을 사용하면
```javascript
let arr = [1, 2, 3, 4, 5];
let result = 0;

for (let i = 0; i < arr.length; i++) {
  result += arr[i];
}

console.log(result); // 15
```
`reduce`를 사용하면
```javascript
let arr = [1, 2, 3, 4, 5];
const initialValue = 0;

let result = arr.reduce((accumulator, currentValue, index, array) => {
  return accumulator + currentValue;
}, initialValue);

console.log(result); // 15
```