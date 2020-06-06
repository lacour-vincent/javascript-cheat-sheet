# JavaScript Cheat Sheet

## Primitive types
```javascript
const a = 1; // number
const b = "Hello World"; // string
const c = true; // boolean
const d = {}; // object
const e = null; // null
const f = undefined; // undefined
```

## Variable
```javascript
const a = "A";
let b = "B";
```

## Function
```javascript
const sum = (a, b) => {
  return a + b;
};
const sum = (a, b) => a + b;
```

## Object
```javascript
const obj = {
  a: 1,
  b: "hello",
  c: true,
  d: () => true
};
```

__Read__
```javascript
const obj = { a: 1, b: 2, c: 3 };
const a = obj.a;
const b = obj.b;
const c = obj["c"];
```

__Add__
```javascript
const foo = { a: 1, b: 2, c: 3 };
foo.d = 4;
const bar = { ...foo, d: 4 };
```

__Remove__
```javascript
const foo = { a: 1, b: 2, c: 3 };
foo.c = undefined;
const { c: _, ...bar } = foo;
```

__Copy__
```javascript
const foo = { a: 1, b: 2, c: 3 };
const bar = Object.assign({}, foo);
const baz = { ...foo };
```

__Destructuring__
```javascript
const obj = { a: 1, b: 2, c: 3 };
const { a, b, c } = obj;
```

__Keys - Values - Entries__
```javascript
const obj = { a: 1, b: 2, c: 3 };
const keys = Object.keys(obj);
const values = Object.values(obj);
const entries = Object.entries(obj);
```

__Optional__
```javascript
const hasKey = true;
const obj = { a: 1, b: 2, ...(hasKey && { c: 3 }) };
```

## Array
```javascript
const numbers = [1, 2, 3];
const strings = ["A", "B", "C"];
const booleans = [true, false, true];
const objects = [{}, {}, {}];
```

__Read__
```javascript
const arr = [1, 2, 3];
const a = arr[0];
const b = arr[1];
const c = arr[2];
```

__Add__
```javascript
const foo = [1, 2, 3];
foo.push(4);
const bar = [...foo, 4];
```

__Copy__
```javascript
const foo = [1, 2, 3];
const bar = foo.slice();
const baz = [...array];
```

__Destructuring__
```javascript
const array = [1, 2, 3];
const [first, second, third] = array;
const [head, ...tail] = array;
```

__Map - Reduce - Filter__
```javascript
const array = [1, 2, 3];
const square = array.map(e => e * e);
const sum = array.reduce((acc, val) => acc + val, 0);
const even = array.filter(e => e % 2 === 0);
```

__Sort__
```javascript
const array = [{ id: 3 }, { id: 2 }, { id: 1 }];
array.sort((a, b) => a.id - b.id);
```

__Optional__
```javascript
const hasElement = true;
const array = [1, 2, ...(hasElement ? [3] : [])];
```

## Map
```javascript
const map = new Map();
const map2 = new Map([
  ["0", 0],
  ["1", 1],
  ["2", 2],
]);
```

__Read__
```javascript
map.get("1");
map.get({});
map.get(() => {});
```

__Add__
```javascript
map.set("1", 1);
map.set({}, 2);
map.set(() => {}, 3);
```

__Has__
```javascript
map.has("1");
map.has({});
map.has(() => {});
```

__Remove__
```javascript
map.delete("1");
map.delete({});
map.delete(() => {});
map.clear();
```

__Loop__
```javascript
map.forEach((key, value) => console.log(key, value));
for (let [key, value] of map) console.log(key, value);
for (let key of map.keys()) console.log(key);
for (let value of map.values()) console.log(value);
for (let [key, value] of map.entries()) console.log(key, value);
```

## Set
```javascript
const set = new Set();
const unique = new Set([1, 1, 2, 2, 3, 3]);
const s1 = new Set([1, 2, 3]);
const s2 = new Set([2, 3, 4]);
const intersection = new Set([...s1].filter((x) => s2.has(x)));
const difference = new Set([...s1].filter((x) => !s2.has(x)));
```

__Add__
```javascript
set.add(1);
```

__Has__
```javascript
set.has(1);
```

__Remove__
```javascript
set.delete(1);
set.clear();
```

__Loop__
```javascript
set.forEach((item) => console.log(item));
for (let item of set) console.log(item);
for (let item of set.keys()) console.log(item);
for (let item of set.values()) console.log(item);
for (let [key, value] of set.entries()) console.log(key, value);
```



## Promise
```javascript
const promise = () =>
  new Promise((resolve, reject) => {
    const number = Math.random();
    if (number > 0.5) {
      resolve("Success");
    } else {
      reject("Fail");
    }
  });

promise()
  .then(() => {/* onSuccess */})
  .catch(() => {/* onError */})
  .finally(() => {/* otherwise */});
```

### All - Race
```javascript
const promiseA = Promise.resolve("A");
const promiseB = Promise.resolve("B");
const promiseC = Promise.reject("C");

Promise.all([promiseA, promiseB]).then(([A, B]) => {/* onSuccess */});
const [A, B] = await Promise.all([promiseA(), promiseB()]);

Promise.race([promiseA, promiseB]).then(value => {/* onSuccess */});
const value = await Promise.race([promiseA, promiseB]);

Promise.allSettled([promiseA, promiseC]).then(([A, C]) => {/* onSuccess or onError */});
const [A, C] = await Promise.allSettled([promiseA, promiseC]);
```

### Async Await
```javascript
const getA = Promise.resolve("A");
const getB = Promise.resolve("B");

const asyncCall = async () => {
  const A = await getA();
  const B = await getB();
};
```

## Class
```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  static distance(a, b) {
    return Math.hypot(a.x - b.x, a.y - b.y);
  }

  toString() {
    return `(${this.x},${this.y})`;
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);
const distance = Point.distance(p1, p2);
```

## Generator
```javascript
function* increment() {
  let count = 0;
  while (true) yield count++;
}

const generator = increment();
generator.next().value; // 0
generator.next().value; // 1
generator.next().value; // 2
```

## Closure
```javascript
const sayHello = () => {
  const name = "Vincent";
  return () => console.log(name);
};

const hello = sayHello();
hello();
```

## High order function
```javascript
const isGreaterThan = (n) => (x) => x > n;
const isGreaterThanFive = isGreaterThan(5);
isGreaterThanFive(1); // false
isGreaterThanFive(10); // true
```

## Bind - Call - Apply
```javascript
const obj = { num: 1 };
const arr = [2, 3, 4];
function add(a, b, c) {
  return this.num + a + b + c;
}

add(2, 3, 4); // NaN -> this.num = undefined
add.call(obj, 2, 3, 4); // 10
add.apply(obj, arr); // 10
const bound = add.bind(obj);
bound(2, 3, 4); // 10
```

## Regular Expression

### Test
```javascript
const regex = /^[A-Z]{1}[a-z]+$/;
const regExp = new RegExp(regex);

const firstname = "Vincent";
const isFirstname = regex.test(firstname);
const isFirstname = regExp.test(firstname);
```

### Match
```javascript
const regex = /[A-Z]/g;
const regExp = new RegExp(regex);

const firstname = "Vincent";
const upperCases = firstname.match(regex);
const upperCases = firstname.match(regExp);
```