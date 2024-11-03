## Math.floor()
The `Math.floor()` method rounds a number DOWN to the nearest integer.
```js
let a = Math.floor(0.60); //return 0
let b = Math.floor(0.40); //return 0
let c = Math.floor(5); //return 5
let d = Math.floor(5.1); //return 5
let e = Math.floor(-5.1); //return -6
let f = Math.floor(-5.9); //return -6
```

## Math.ceil()
Math.ceil() rounds a number UP to the nearest integer:

```js
let a = Math.ceil(0.60); //return 1
let b = Math.ceil(0.40); //return 1
let c = Math.ceil(5); //return 5
let d = Math.ceil(5.1); //return 6
let e = Math.ceil(-5.1); //return -5
let f = Math.ceil(-5.9); //return -5
```
## reduce()

^d221a0

reduce() actually rounds an array and return the sum with item
```js
const items = [12, 34, 55]
items.reduce((total, item) => {
	return total + item
}, 0)
```
Here is the iteration is running up all of the array item and make a total.
Note: 0 is the initial total value. If I put a initial value 10 then the iteration will start the sum with 10.