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

Promise.all([promiseA(), promiseB()]).then(([A, B]) => {/* onSuccess */});
const [A, B] = Promise.all([promiseA(), promiseB()]);

Promise.race([promiseA(), promiseB()]).then(value => {/* onSuccess */});
const value = Promise.race([promiseA(), promiseB()]);
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