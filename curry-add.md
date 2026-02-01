Problem: curry to add function:

Solution:
```js
const add = (a, b, c, d, e) => {
  return a + b + c + d + e;
};

const curry = (fn) => {
  return function curried(...args){
    if(fn.length <= args.length) {
      return fn(...args);
    }
    
    return (...nextargs) => {
      if(!nextargs.length) {
        return fn(...args);
      }
      
      return curried(...args, ...nextargs);
    }
  }
}

const curriedAdd = curry(add);

console.log(curriedAdd(1,2,3,4,5))

console.log(curriedAdd(1)(2,3,4)(4))

console.log(curriedAdd(1,2)(3,4,5))
```
