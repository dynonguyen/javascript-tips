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
- [Compairsion](#compairsion)
- [Function](#function)
- [Math](#math)
- [Others](#others)

<!-- Tips for array -->

# Array

<details open="open">
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

<details open="open">
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

<details open="open">
  <summary>
    3. Shuffle Elements from Array
  </summary>

<br />

```js
var arr = [1, 2, 3, 4, 5];
var newArr = arr.sort(() => Math.random() - 0.5);

// result: newArr = [3, 1, 2, 4, 1]
```

</details>

<details open="open">
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

<details open="open">
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

<details open="open">
  <summary>
    6. Random an Item in Array
  </summary>

<br />

```js
var arr = [2, 4, 5];
var item = arr[Math.floor(Math.random() * arr.length)];
```

</details>

<details open="open">
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

<details open="open">
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

<details open="open">
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

  obj1.a = 3;
  obj1.c.nested = 4;

  console.log(obj1); // { a: 1, b: 3, c: { nested: 4 } }
  console.log(obj2); // { a: 1, b: 2, c: { nested: 4 } } 🙂
  console.log(obj3); // { a: 1, b: 2, c: { nested: 4 } } 🙂
  ```

  > **Way 2 `(Recommended)`**: Use `JSON.stringify()` & `JSON.parse()` to solve the above problems

  ```js
  var obj1 = { a: 1, b: 2, c: { nested: 3 } };
  var obj2 = JSON.parse(JSON.stringify(obj1)); // obj2 = { a: 1, b: 2, c: { nested: 4 } }

  obj1.a = 3;
  obj1.c.nested = 4;

  console.log(obj1); // { a: 1, b: 3, c: { nested: 4 } }
  console.log(obj2); // { a: 1, b: 2, c: { nested: 3 } } 😉😘
  ```

<br />

</details>

# Destructuring

# Operator

# Compairsion

# Function

# Math

# Others
