<h1 align="center"> JavaScript tips & tricks </h1>

<!-- logo -->
<div align="center">
  <img  src="images/logo.jpeg" height="200" width="450" />
</div>

# Description 😋

> This is a collection of JavaScript tips and tricks. you can refer to it and apply it to make your code more concise. **But don't overdo it**, it can make your code difficult to read and maintain. Hope everyone contributes, thanks.

<!-- table of content -->

# Table Of Content 📃

- [Description](#description)
- [Table Of Content](#table-of-content)
- [Array](#array)
- [Object](#object)
- [Destructuring](#destructuring)
- [Operator](#operator)
- [Comparison](#comparison)
- [Others](#others)

<!-- Tips for array -->

# Array

<details >
  <summary>
    1. Generate an Array
  </summary>

- Create an empty array of length **`n`**

  ```js
  var arr = new Array(3);

  // result: arr = [undefined, undefined, undefined]
  ```

- Create an empty array of length **`n`** & fill value **`x`**

  ```js
  var arr = [...Array(3).fill(1)];
  var arr2 = [...Array(5).fill(1, 0, 3)];

  /* 
    result: arr = [1, 1, 1]
            arr2 = [1, 1, 1, undefined, undefined]
  */
  ```

- Create an array containing `0...n`

  ```js
  var arr = [...Array.keys(5)];

  // result: arr = [0, 1, 2, 3, 4]
  ```

- Create an array containing `1...n`

  ```js
  var arr = [];
  for (let i = 0; arr.push(++i) < 4; );

  var arr2 = Array.from({ length: 4 }, (_, i) => i + 1);
  var arr3 = Array.from({ length: 4 }, (_, i) => i * 2);
  var arr4 = Array.from({ length: 4 }, () => Math.random());

  /* 
    result: arr =  [1, 2, 3, 4]
            arr2 = [1, 2, 3, 4]
            arr3 = [0, 2, 4, 6]
            arr4 = [0.211, 0.5123, 0.612, 0.8921]
  */
  ```

</details>

<details >
  <summary>
    2. Extract Unique Values of Array
  </summary>

<br />

```js
var arr = [1, 2, 2, 3, 5, 5, 4];
var newArr = [...new Set(arr)];

// result: newArr = [1, 2, 3, 5, 4]
```

</details>

<details >
  <summary>
    3. Shuffle Elements from Array
  </summary>

<br />

```js
var arr = [1, 2, 3, 4, 5];
var newArr = arr.sort(() => Math.random() - 0.5);

// result: newArr = [3, 1, 2, 4, 5]
```

</details>

<details >
  <summary>
    4. Flatten a Multidimensional Array
  </summary>

<br />

```js
var arr = [1, [2, 3], [4, 5, 6], 7];
var newArr = [].concat(...arr);

// result: [1, 2, 3, 4, 5, 6, 7]
```

</details>

<details >
  <summary>
    5. Resize an Array
  </summary>

> The length array isn't a read only property.

```js
var arr = [1, 2, 3, 4, 5];
arr.length = 2;

var arr2 = [1, 2, 3, 4, 5];
arr2.length = 0;

var arr3 = [1, 2, 3, 4, 5];
arr3.length = 7;

/*
  result: arr = [1, 2]
          arr2 = []
          arr3 = [1, 2, 3, 4, 5, undefined, undefined]
*/
```

</details>

<details >
  <summary>
    6. Random an Item in Array
  </summary>

<br />

```js
var arr = [2, 4, 5];
var item = arr[Math.floor(Math.random() * arr.length)];
```

</details>

<details >
  <summary>
    7. Remove an Item from Array
  </summary>

<br />

```js
var arr = [1, 2, 3];

// Not Recommended
delete arr[1]; // arr = [1, undefined, 3], length = 3

// Recommended
arr.splice(1, 1); // arr = [1, 3], length = 2
```

</details>

# Object

<details >
  <summary>
    1. Dynamic Property Name
  </summary>

  <br/>

```js
const dynamic = 'age',
	dynamicValue = 18;

var obj = {
	name: 'Dyno',
	[dynamic]: dynamicValue,
};

// result: obj = { name: 'Dyno', age: 18 }
```

</details>

<br />

<details >
  <summary>
    2. Clone an Object
  </summary>

- Shallow copy `(Not Recommended)`

  > Use the `=` operator to copy object 1 into object 2. These 2 objects point to the same memory area `(reference)`. Therefore, if we change object 1, object 2 will also change.

  ```js
  var obj1 = { a: 1, b: 2 };
  var obj2 = obj1; // obj2 = { a: 1, b: 2 }

  obj1.a = 3; // change value of a property

  console.log(obj1); // { a: 3, b: 2 }
  console.log(obj2); // { a: 3, b: 2 } => property a of obj2 changed 🙂❗
  console.log(obj3); // { a: 3, b: 2 } => property a of obj2 changed 🙂❗
  ```

- Deep copy

  > **Way 1**: Use Spread operator `{...}` or `Object.assign()` to fix "Shallow copy". **_Issue:_** `Nested objects` still have shallow copy problem.

  ```js
  var obj1 = { a: 1, b: 2, c: { nested: 3 } };
  var obj2 = { ...obj1 }; // obj2 = { a: 1, b: 2, c: { nested: 3 } }
  var obj3 = Object.assign({}, obj1); // obj3 = { a: 1, b: 2, c: { nested: 3 } }

  obj1.b = 3;
  obj1.c.nested = 4;

  console.log(obj1); // { a: 1, b: 3, c: { nested: 4 } }
  console.log(obj2); // { a: 1, b: 2, c: { nested: 4 } } 🙂
  console.log(obj3); // { a: 1, b: 2, c: { nested: 4 } } 🙂
  ```

  > **Way 2 `(Recommended)`**: Use `JSON.stringify()` & `JSON.parse()` to solve the above problems.

  ```js
  var obj1 = { a: 1, b: 2, c: { nested: 3 } };
  var obj2 = JSON.parse(JSON.stringify(obj1)); // obj2 = { a: 1, b: 2, c: { nested: 3 } }

  obj1.b = 3;
  obj1.c.nested = 4;

  console.log(obj1); // { a: 1, b: 3, c: { nested: 4 } }
  console.log(obj2); // { a: 1, b: 2, c: { nested: 3 } } 😉😘
  ```

<br />

</details>

# Destructuring (ES6+)

<details>
  <summary>
    1. With Array
  </summary>

  <br/>

```js
var [a, b] = [1, 2];
// same: var a = 1, b = 2;

var [a, b, c] = [1, 2, 3, 4, 5];
// same: var a = 1, b = 2, c = 3;

var [a, , c] = [1, 2, 3, 4, 5];
// same: var a = 1, c = 3
// ignore values

var [a, b, ...rest] = [1, 2, 3, 4, 5];
// same: var a = 1, b = 2, rest = [4, 5]
// use "rest params ES6"

var [a, b, c] = [1, 2];
// same: var a = 1, b = 2, c = undefined;

var [a, b = 0, c = 0] = [1, 2];
// same: var a = 1, b = 2, c = 0;
// declare and set default value

var [a, b, [c, d], e] = [1, 2, [3, 4], 5];
// same: var a = 1, b = 2, c = 3, d = 4, e = 5
// nested array destructuring
```

</details>

<details>
  <summary>
    2. With Object
  </summary>

  <br/>

```js
var person = { name: 'Dyno', age: 18 };

var { name, age } = person;
// same: var name = person.name, age = person.age;

var { name = 'Anonymous', age = 1, address = 'HCM city' } = person;
// same: var name = person.name, age = person.age, address: 'HCM city'
// declare and set default value

var { name: personName, age: personAge } = person;
// same: var personName =  person.name, personAge = person.age
// decleare and change variable name

console.log({ name, age });
// same: console.log({ name: name, age: age })

var person = { name: 'Dyno', age: 18, infor: { address: 'HCM', phone: '123' } };
var {
	name,
	age,
	infor: { address, phone },
} = person;
// same: name = person.name, age = person.agem, address = person.infor.address, phone = person.infor.phone
// nested object destructuring
```

</details>

# Operator

<details>
  <summary>
    1. Optional chaining (?.)
  </summary>

<br/>

> "The optional chaining operator `?.` enables you to read the value of a property located deep within a chain of connected objects without having to check that each reference in the chain is valid." [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

  <br/>

```js
const person = {
	name: 'Dyno',
	age: 18,
	sayHello: function () {
		console.log('Hello');
	},
};

// ❗ Wrong way
console.log(person.infor.address); // ❌ Uncaught TypeError: Cannot read property 'address' of undefined

// ✅ Right way (check condition)
if (person.infor) console.log(person.infor.address); // Not log

// ✅ Right way (use ?.)
console.log(person.infor?.address); // undefined

// Optional chaining with function calls
console.log(person.sayHello?.()); // Hello
console.log(person.callPhone?.()); // undefined

// A chain Optional chaining
console.log(person.infor?.address?.province?.name); // undefined
```

```js
// syntax
obj.val?.prop;
obj.val?.[expr];
obj.arr?.[index];
obj.func?.(args);
```

</details>

<details>
  <summary>
    2. Nullish coalescing operator (??)
  </summary>

  <br/>

> "The nullish coalescing operator `??` is a logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined`, and otherwise returns its left-hand side operand." [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

```js
var a = null ?? 'Default'; // a = 'Default'
var a = false ?? 'Default'; // a = false
```

</details>

<details>
  <summary>
    3. Logical OR (||)
  </summary>

```js
var a = 1,
	b = 2;

if (a > 2 || b > 1) console.log('Dyno');

// result: Dyno
```

> The OR operator `||` is a logical operator that returns its right-hand side operand when its left-hand side operand is `falsy`, and otherwise returns its left-hand side operand.

  <br/>

```js
var a = null || 'Default'; // a = 'Default'
var a = false || 'Default'; // a = 'Default'
```

</details>

<details>
  <summary>
    4. Logical AND (&&)
  </summary>

  <br/>

```js
let a = true,
	b = true,
	c = false;

if (a && b) console.log('Hello'); // Hello (a, b = true)

if (a && c) console.log('Dyno'); // not log (c = false)

// other usage
function sayHi() {
	console.log('Hi');
}

a && sayHi(); // Hi
c && sayHi(); // false
```

</details>

<details>
  <summary>
    5. Double tilde operator (~~)
  </summary>

  <br/>

```js
let num = 2.6;
console.log(~~num); // 2 = Math.floor(2)
```

</details>

<details>
  <summary>
    6. Logical Assignment Operator ES12  (||=, ??=) 
  </summary>

  <br/>

```js
a ||= b; // same a = a || b;
a ??= b; // same a = a ?? b;
```

</details>

<details>
  <summary>
    7. Numeric separator ES12 (_)
  </summary>

  <br/>

```js
const n = 1_000_000_000; // same: n = 1000000000;
```

</details>

# Comparison

<details>
  <summary>
    1. Use === instead of ==
  </summary>

<br/>

> The operator `== (!=)` will automatically cast if 2 variables are not of the same type, then compare. The `=== (!==)` operator compares the value and the type => `===` faster than `==`.

<br/>

```js
  1 == '1' // true
  1 === '1' // false

  0 == false // true
  0 === false // false

  '' == false // true
  '' === false // false

  [] == 0 // true
  [] === 0 // false

```

</details>

<details>
  <summary>
    2. The difference between isNaN() and Number.isNaN() 
  </summary>

<br/>

> The `isNaN()` method (is Not a Number ?) use to check if a variable is **a Number**. The `Number.isNaN()` (is NaN ?) method use to check if a variable is **NaN**

<br/>

```js
isNaN('string');
// true, 'string' is not Number

isNaN([]);
// true, [] is not Number

isNaN(0 / 0);
// true, 0/0 is not Number

isNaN(1);
// false, 1 is Number

Number.isNaN('string');
// false, 'string' is not NaN

Number.isNaN([]);
// false, [] is not NaN

Number.isNaN(0 / 0);
// true, 0/0 is NaN

Number.isNaN(NaN);
// true
```

</details>

# Others

<details>

  <summary>
    1. Swapping use Destructuring
  </summary>

  <br/>

```js
let a = 1,
	b = 2;

[a, b] = [b, a];

// result: a = 2, b = 1;
```

</details>

<details>
  <summary>
    2. Create function that returns only 1 object
  </summary>

  <br/>

```js
const fn = () => ({ obj: 1 });

/*
  same: const fn = () => {
    return { obj: 1 }
  }
*/
```

</details>

<details>
  <summary>
    3. Immediately Invoked Function Expression (IIFE)
  </summary>

  <br/>

> The function will execute automatically when you create it.

  <br/>

```js
  // Way 1:
  var res = ()(function(){
    // do something...
    console.log("Hello");
    return true;
  })();
  // result: Hello, res = true;

  // Way 2:
  var res = (() => {
    console.log('Hello');
    return true;
  })();
  // result: Hello, res = true;
```

</details>

<details>
  <summary>
    4. typeof vs instanceof 
  </summary>

  <br/>

> `typeof`: return a string that represents the primitive type of a variable.

> `instanceof`: check in all the prototypes chain the constructor it returns true if it’s found and false if not.

  <br/>

```js
var arr = [1, 2, 3];
console.log(typeof arr); // "object"
console.log(arr instanceof Array); // true

typeof 1; // "number"
typeof NaN; // "number"
typeof 'str'; // "string"
typeof true; // "boolean"
typeof {}; // "object"
typeof []; // "object"
typeof null; // "object"
typeof undefined; // "undefined"
typeof function name() {}; // "function"
```

</details>

<details>
  <summary>
    5. Falsy
  </summary>

  <br/>

> A `Falsy value` is a value that is considered false when encountered in a Boolean context . [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)

> Complete list of JavaScript falsy values ` false, 0, -0, 0n, "", '', ``, NaN, null, undefined, document.all`

> Falsy value bypass the if block. Ex:

<br/>

```js
if (null) {
} else {
	console.log('Falsy');
}

const a = undefined || 'Falsy';

// result: Falsy, a = "Falsy"
```

> Filter out Falsy values

<br/>

```js
const arr = [1, 'Dyno', false, 0, true, NaN, 2000];
var filteredArr = arr.filter(Boolean);

// result: filteredArr = [1, "Dyno", true, 2000]
```

</details>

<details>
  <summary>
    6. Template string `${}`
  </summary>

  <br/>

```js
const name = 'Dyno';
const hello1 = 'Hello ' + name + ', how are you?';
const hello2 = `Hello ${name}, how are you?`; // template string
```

</details>

<details>
  <summary>
    7. Rounding number to n decimal place

  </summary>

  <br/>

```js
var num = 25.0420001;
console.log(typeof num); // "number"

num = num.toFixed(2); // num = "25.04"
console.log(typeof num); // ❗ "string"
```

</details>
