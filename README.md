<h1 align="center"> JavaScript tips & tricks </h1>

<!-- logo -->
<div align="center">
  <img  src="images/logo.jpeg" height="200" width="450" />
</div>

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
  var arr = Array.from({ length: 4 }, (_, i) => i + 1);
  var arr2 = Array.from({ length: 4 }, (_, i) => i * 2);
  var arr3 = Array.from({ length: 4 }, () => Math.random());

  /* 
    result: arr = [1, 2, 3, 4]
            arr2 = [0, 2, 4, 6]
            arr3 = [0.211, 0.5123, 0.612, 0.8921]
  */
  ```

</details>

<details open="open">
  <summary>
    2. Extract Unique Values of Array
  </summary>

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

```js
var arr = [1, 2, 3, 4, 5];
arr.length = 2;

var arr2 = [1, 2, 3, 4, 5];
arr2.length = 0;

/*
  result: arr = [1, 2]
          arr2 = []
*/
```

</details>
