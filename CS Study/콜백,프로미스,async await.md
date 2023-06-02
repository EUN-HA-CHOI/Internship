### 콜백(callback) 함수
자바스크립트 콜백 함수를 공부하기에 앞서 동기와 비동기의 의미를 알고 가자.

### 동기와 비동기의 의미
- 동기는 하나의 요청이 오면 완료가 된 후 다음 요청을 실행하는 방식을 말하고,
- 비동기는 어떤 요청이 오면 완료가 되기 전에 다음 요청을 실행하는 방식을 말한다.
- 동기 방식은 순차적으로 로직이 수행되므로 흐름을 쉽게 예측할 수 있지만,
- 비동기 방식의 경우 여러 작업을 동시에 효율적으로 처리할 수 있는 반면에 즉시 응답을 못 받기 때문에 적절히 처리가 되지 않으면
  예상 밖의 결과가 나올 수 있으므로 주의를 기울여야 한다.

### 콜백 함수 사용 목적
비동기로 호출한 함수의 결과값이 필요할 때 콜백 함수를 사용한다. 

비동기 방식으로 작성된 함수를 동기 처리 하기 위해 주로 사용한다.

비동기 처리를 기본으로 하면서도 일부 구간에서 순차적인 처리가 필요할 수 있기 때문이다.

다르게 말하면 독립적으로 수행되는 작업도 있는 반면 응답을 받은 이후 처리되어야 하는 종속적인 작업도 있을 수 있으므로
그에 대한 대응 방법이 필요한 것이다.  


### 콜백 함수 형태  
```javascript
function mainFunc(param1, param2, callbackFunc) {
//..처리 내용 작성
callbackFunc(result);
}
```

보통 함수를 선언한 뒤에 함수 타입 파라미터를 맨 마지막에 하나 더 선언해 주는 방식으로 정의한다.
처리가 끝나면 파라미터로 전달 받은 함수를 실행한다.
필요한 경우 결과 값을 인자로 넘겨줄 수도 있다.
콜백 함수는 간단하게 다른 함수에 매개변수로 넘겨준 함수를 말한다.
매개변수로 넘겨받은 함수는 일단 넘겨받고, 때가 되면 나중에 호출(called back)한다는 것이 콜백 함수의 개념이다. 

- 예제 
```javascript
function checkGang(count, link, good) {
count < 3 ? link() : good();
}
function linkGang() {
console.log('오늘은 2번 운동 했다.');
}
function goodGang() {
console.log('오늘은 3번 운동 했다.');
}
checkGang(3, linkGang, goodGang);
```
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/86f05b95-eb84-43f2-8964-f6681abd9445)

<hr>

## 프로미스  
자바스크립트는 비동기 처리를 위한 하나의 패턴으로 콜백 함수를 사용한다. 하지만 전통적인 콜백 패턴은 콜백 헬로 인해 가독성이 나
쁘고 비동기 처리 중 발생한 에러의 처리가 곤란하며 여러 개의 비동기 처리를 한 번에 처리하는 데도 한계가 있다.

ES6 에서는 비동기 처리를 위한 또 다른 패턴으로 프로미스(promise) 를 도입했다. 프로미스는 전통적인 콜백 패턴이 가진 단점을 보완하
며 비동기 처리 시점을 명확하게 표현할 수 있는 장점이 있다. 

- 콜백 지옥 예시 
```javascript
function increaseAndPrint(n, callback) {
setTimeout(() => {
const increased = n + 1;
console.log(increased);
if (callback) {
callback(increased);
}
}, 1000);
}
increaseAndPrint(0, n => {
increaseAndPrint(n, n => {
increaseAndPrint(n, n => {
increaseAndPrint(n, n => {
increaseAndPrint(n, n => {
console.log('끝!');
});
});
});
});
});
```
이와 같이 콜백 지옥을 만나게 되면 코드 읽기가 복잡해지게 된다. 이때 프로미스를 사용하면 코드의 깊이가 깊어지는 현상을 방지 할 수
있다.


### 프로미스 만들기  
promise 는 다음과 같이 만든다.  
```
const myPromise = new Promise((resolve, reject) => {
// 구현..
})
```

promise 는 성공 할 수도 있고, 실패 할 수도 있다. 성공 할 때는 resolve 를 호출해주면 되고, 실패할 때에는 reject 를 호출해주면 된다. 지금
당장은 실패하는 상황은 고려하지 않고, 1초 뒤에 성공 시키는 상황에 대해서만 구현을 해 보겠다.

```javascript
const myPromise = new Promise((resolve, reject) => {
setTimeout(() => {
resolve(1);
}, 1000);
});
myPromise.then(n => {
console.log(n);
});
```

resolve 를 호출 할 때 특정 값을 파라미터로 넣어주면, 이 값을 작업이 끝나고 나서 사용 할 수 있다. 작업이 끝나고 나서 또 다른 작업을 해
야 할 때에는 promise 뒤에 .then(…)을 붙여서 사용하면 된다.

이번에는, 1초 뒤에 실패되게끔 해보자.
```javascript
const myPromise = new Promise((resolve,reject) => {
settTimeout(() => {
reject(new Error());
},1000)
});
myPromise.then(n => {
console.log(n);
})
.catch(error => {
console.log(error);
});
```

실패하는 상황에서는 reject 를 사용하고, .catch를 통하여 실패했을시 수행 할 작업을 설정 할 수 있다.


이제 promise 를 만드는 함수를 작성 해 보자.

```javascript
function increaseAndPrint(n) {
return new Promise((resolve, reject) => {
setTimeout(() => {
const value = n + 1;
if (value === 5) {
const error = new Error();
error.name = 'ValueIsFiveError'
reject(error);
return;
}
console.log(value);
resolve(value);
},1000);
}
increaseAndPrint(0).then((n) => {
console.log('result: ', n);
)}
```

여기까지만 보면, 결국 함수를 전달하는건데, 뭐가 다르지 싶을수도 있다. 하지만, Promise 의 속성 중에는, 만약 then 내부에 넣은 함수에
서 또 Promise 를 리턴하게 된다면, 연달아서 사용 할 수 있다.

```javascript
function increaseAndPrint(n) {
return new Promise((resolve, reject) => {
setTimeout(() => {
const value = n + 1;
if (value === 5) {
const error = new Error();
error.name = 'ValueIsFiveError';
reject(error);
return;
}
console.log(value);
resolve(value);
}, 1000);
});
}

increaseAndPrint(0)
.then(n => {
return increaseAndPrint(n);
})
.then(n => {
return increaseAndPrint(n);
})
.then(n => {
return increaseAndPrint(n);
})
.then(n => {
return increaseAndPrint(n);
})
.then(n => {
return increaseAndPrint(n);
})
.catch(e => {
console.error(e);
});
```

- 코드는 이렇게 정리할 수 있다. 
```javascript
function increaseAndPrint(n) {
return new Promise((resolve, reject) => {
setTimeout(() => {
const value = n + 1;
if (value === 5) {
const error = new Error();
error.name = 'ValueIsFiveError';
reject(error);
return;
}
console.log(value);
resolve(value);
}, 1000);
});
}
increaseAndPrint(0)
.then(increaseAndPrint)
.then(increaseAndPrint)
.then(increaseAndPrint)
.then(increaseAndPrint)
.then(increaseAndPrint)
.catch(e => {
console.error(e);
});
```

Promise 를 사용하면, 비동기 작업의 개수가 많아져도 코드의 깊이가 깊어지지 않게 된다.
하지만, 이것도 불편한 점이 있긴 하다. 에러를 잡을 때 몇 번째에서 발생했는지 알아내기도 어렵고 특정 조건에 따라 분기를 나누는 작업
도 어렵고, 특정 값을 공유해가면서 작업을 처리하기도 까다롭다.
async/await 을 사용하면, 이러한 문제점을 깔끔하게 해결 할 수 있다.

## async/await

프로미스에 비해서 가독성이 좋고, 에러 위치를 찾기가 쉽다.
Promise 를 더욱 쉽게 사용 할 수 있게 해준다.

기본적인 사용법을 알아보자.
```javascript
function sleep(ms) {
return new Promise(resolve => setTimeout(resolve, ms));
}
async function process() {
console.log('안녕하세요!');
await sleep(1000); // 1초쉬고
console.log('반갑습니다!');
}
process();
```
async/await 문법을 사용할 때에는, 함수를 선언 할 때 함수의 앞부분에 async 키워드를 붙여준다. 그리고 promise 의 앞부분에 await 을 넣
어주면 해당 프로미스가 끝날 때까지 기다렸다가 다음 작업을 수행 할 수 있다.
위 코드에서는 sleep 이라는 함수를 만들어서 파라미터로 넣어준 시간 만큼 시다리는 promise 를 만들고, 이를 process 함수에서 사용해주
었다.
함수에서 async 를 사용하면, 해당 함수는 결과값으로 promise 를 반환하게 된다. 따라서 다음과 같이 코드를 작성 할 수 있다.

```javascript
function sleep(ms) {
return new Promise(resolve => setTimeout(resolve, ms));
}
async function process() {
console.log('안녕하세요!');
await sleep(1000); // 1초쉬고
console.log('반갑습니다!');
}
process().then(() => {
console.log('작업이 끝났어요!');
});
```

async 함수에서 에러를 발생 시킬때에는 throw 를 사용하고, 에러를 잡아낼 때에는 try/catch 문을 사용한다.
```javascript
function sleep(ms) {
return new Promise(resolve => setTimeout(resolve, ms));
}
async function makeError() {
await sleep(1000);
const error = new Error();
throw error;
}
async function process() {
try{
await makeError();
} catch(e) {
console.error(e);
}
}
process();
```
function sleep(ms) {
