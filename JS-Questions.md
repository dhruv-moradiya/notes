1. You are working on a JavaScript project where you need to create a utility function that manipulates context (this) of other functions. Your task is to implement three functions callWithContext, applyWithContext, and bindWithContext that mimic the behavior of JavaScript's built-in call, apply, and bind methods.

```js
function add(a, b) {
  return a + b;
}

const obj = {
  x: 10,
  y: 20,
  add: function (a, b) {
    return this.x + this.y + a + b;
  },
};

// Using callWithContext
console.log(callWithContext(add, null, 3, 4)); // 7
console.log(callWithContext(obj.add, { x: 1, y: 2 }, 3, 4)); // 10

// Using applyWithContext
console.log(applyWithContext(add, null, [3, 4])); // 7
console.log(applyWithContext(obj.add, { x: 1, y: 2 }, [3, 4])); // 10

// Using bindWithContext
const boundAdd = bindWithContext(add, null, 3);
console.log(boundAdd(4)); // 7

const boundObjAdd = bindWithContext(obj.add, { x: 1, y: 2 }, 3);
console.log(boundObjAdd(4)); // 10
```
