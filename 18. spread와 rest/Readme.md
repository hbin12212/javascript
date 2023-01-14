안녕하세요🤗

> 이번시간에는 spread와 rest 문법에 대해 배워보도록 하겠습니다.

# spread

먼저 spread 연산자를 배워보겠습니다.

spread는 확산, 퍼짐, 전파라는 뜻으로 실제로 특정 객체 프로퍼티 값들을 펼치는 역할을 합니다.

## 객체

spread 연산자를 설명하기 위해 아래와 같이 여러 객체들을 작성해보겠습니다.

```js
const toy = {
    type: "bear",
    price: 15000,
};

const blueToy = {
    type: "bear",
    price: 15000,
    color: "blue",
};

const yellowToy = {
    type: "bear",
    price: 15000,
    color: "yellow",
};
```

위의 객체들을 살펴보면, 3개의 객체의 type, price 프로퍼티 값이 같은 것을 알 수 있습니다.

마찬가지로, 위의 코드에 purpleToy 라는 객체도 추가로 생성해보겠습니다.

```js
const purpleToy = {
    type: "bear",
    price: 15000,
    color: "purple",
};
```

purpleToy 라는 객체 또한, 나머지 객체들의 type, price 프로퍼티 값이 동일한 것을 볼 수 있습니다.

이렇게 비슷한 프로퍼티를 가진 객체를 생성하려면, 같은 코드를 `여러번 작성`해야되는 문제점이 생기게됩니다.

이와 같은 상황에서 우리는 `spread 연산자`를 이용합니다.

```js
const toy = {
    type: "bear",
    price: 15000,
};

const blueToy = {
    ...toy,
    color: "blue",
};

const yellowToy = {
    ...toy,
    color: "yellow",
};

const purpleToy = {
    ...toy,
    color: "purple",
};
```

spread 연산자는 `...` 키워드를 사용하여, 특정 객체가 가진 프로퍼티들을 펼쳐줍니다.

위의 코드에서 `...toy` 는 toy 객체가 가진 프로퍼티들을 모든 나머지 객체들이 가지고 있기 때문에 모든 프로퍼티들을 펼쳐서 나타냅니다.

## 배열

spread 연산자는 객체 뿐만 아니라 아래와 같이 배열에서도 사용 가능 합니다.

```js
const color1 = ["red", "orange", "yellow"];
const color2 = ["blue", "navy", "purple"];
const rainbow = [...color1, "green", ...color2];

console.log(rainbow);
```

위의 코드에서는 rainbow 배열에 spread 연산자를 이용해 color1, color2 배열의 값을 넣어줬습니다.

이렇게 spread 연산자는 순서에 상관 없이 사용 할 수 있고, 여러번 사용할 수도 있습니다.

rainbow 배열의 값을 출력하면 다음과 같이 출력되는 것을 확인할 수 있습니다.

```
["red", "orange", "yellow", "green", "blue", "navy", "purple"]
```

# rest

이번에는 rest 문법에 대해 배워보겠습니다.

rest 문법은 spread 와 비슷해보이지만, 서로 다른 역할을 하는 문법입니다.

먼저 객체에서 rest 문법이 어떻게 사용되는지 알아보도록 하겠습니다.

## 객체

```js
const purpleToy = {
    type: "bear",
    price: 15000,
    color: "purple",
};

const { type, ...other } = purpleToy;

console.log(type);
console.log(other);
```

위의 코드에서는 purpleToy 객체를 type과 other 에 할당했습니다.

```
bear
{price: 15000, color: "purple"}
```

출력 결과, `other`에는 purpleToy 객체 프로퍼티 중 type 값을 제외한 나머지 값들이 들어있는 것을 볼 수 있습니다.

이렇게 rest는 구조분해를 통해 원하는 값들을 꺼내고 나머지 값을 별도로 할당할 수 있습니다.

이번엔 type과 other의 순서를 바꿔 purpleToy 객체를 할당하는 코드를 작성해보겠습니다.

```js
const { ...other, type } = purpleToy; // SyntaxError
```

rest 문법은 spread와는 달리 rest 문법을 맨 마지막에 사용하지 않으면 에러가 나게 되므로 주의해야합니다.

위의 코드를 실행하면 다음과 같은 값이 출력됩니다.

## 배열

다음으로는 rest를 배열에서 사용하려면 어떻게 작성해야 하는지 알아보겠습니다.

```js
const color = ["red", "orange", "yellow", "green"];
const [one, two, ...other] = color;

console.log(one);
console.log(two);
console.log(other);
```

객체에서 사용했을 때와 비슷하게 구조분해 문법과 함께 사용되는 것을 볼 수 있습니다.

마찬가지로 위의 코드를 실행하면 다음과 같은 결과값이 출력됩니다.

```
red
orange
["yellow", "green"]
```

## 함수

rest는 원하는 값을 꺼내고 넣을 수 있는 문법이기 때문에, 함수 파라미터에서 유용하게 사용되기도 합니다.

```js
const print = (a, b, ...rest) => {
    console.log("a", a);
    console.log("b", b);
    console.log("rest", rest);
};

print(1, 2, 3, 4, 5, 6);
```

위의 코드를 살펴보면, print 함수의 파라미터로 a와 b, 그리고 rest 파라미터를 이용했습니다.
print 함수를 실행시키면 다음과 같은 값이 출력됩니다.

```
a 1
b 2
rest [3, 4, 5, 6]
```

a와 b 에는 각각 1과 2의 값이 할당되었고, rest에는 1과 2를 제외한 나머지 값인 [3, 4, 5, 6] 이 할당되었습니다.
이렇게 함수의 파라미터로 rest를 사용하게 되면, rest 파라미터의 값은 함수에서 받아온 파라미터들로 이루어진 배열이 들어오게 됩니다.

rest 파라미터는 함수의 파라미터가 몇 개가 될 지 모를 떄, 함수에서 받아온 파라미터들을 배열로 나타내야 될 때 유용하게 사용할 수 있는 문법입니다.

## rest 와 spread

이렇게 rest와 spread 문법을 모두 배워봤는데요, 처음 배우는 개념이다 보니 아직까지는 많이 헷갈릴 수 있습니다.

두 문법의 차이를 헷갈리지 않고 더 명확하게 하기 위해서, 함수에서 rest와 spread 문법을 모두 사용하는 코드를 살펴보겠습니다.

먼저 numbers 배열의 요소들을 print 함수의 파라미터로 넘겨, 그 요소들의 값을 출력하는 print함수를 코드로 작성해보겠습니다.

```js
const print = (a, b, c, d, e, f) => {
    console.log(a, b, c, d, e, f);
};

const numbers = [1, 2, 3, 4, 5, 6];
print(numbers[0], numbers[1], numbers[2], numbers[3], numbers[4], numbers[5]);
```

위의 코드처럼, print 함수에 인자로 numbers 배열의 모든 요소들을 넣었습니다.

만약 numbers 배열에 10개가 넘는 요소가 존재했다면, 코드를 작성하기 번거로웠을 것 같은데요,
이 print 함수의 인자 부분을 spread 문법을 이용해서 작성해보겠습니다.

```js
const print = (a, b, c, d, e, f) => {
    console.log(a, b, c, d, e, f);
};

const numbers = [1, 2, 3, 4, 5, 6];
print(...numbers); // spread
```

spread 문법을 사용하면 이렇게 훨씬 간편하게 코드를 작성할 수 있습니다.
이렇게 spread는 객체나 배열의 값들을 펼쳐서 나타내는 역할을 하는 문법입니다.

이번엔 print 함수의 파라미터 부분을 살펴보겠습니다.
numbers 배열의 요소들이 6개인 것을 알고있기 때문에 파라미터로 6개를 작성해주었는데,
이렇게 작성한다면, numbers 배열의 요소들이 늘어나거나 적어진다면 오류가 날 위험이 있습니다.

print 함수의 파라미터 부분을 rest 문법을 이용해 작성해보겠습니다.

```js
const print = (...rest) => {
    console.log(rest); // rest
};

const numbers = [1, 2, 3, 4, 5, 6];
print(...numbers); // spread
```

이렇게 rest와 spread 를 이용해 작성하면 훨씬 간단하고 깔끔한 코드를 작성해볼 수 있습니다.

---

# next

이번 시간에는 spread와 rest 문법에 대한 개념과 둘의 차이에 대해 배워보았습니다.
다음 시간에는 자바스크립트의 비동기적 처리에 대한 개념과 작업을 비동기적으로 처리할 수 있는 방법을 배워보도록 하겠습니다.

---
