Problem: implement a function customFilter that mimics the behaviour of Array.prototype.filter method


Solution:

```js
Array.prototype.customFilter = function(callbackFn){
  const arr = this;
  const res = [];
  
  if(!Array.isArray(arr)) {
    return res;
  }
  
  arr.forEach(item => {
    if(callbackFn(item)) {
      res.push(item)
    }
  });
  
  return res;
}


const numbers = [1,2,3,4,5,6];

console.log(numbers.customFilter((num) => num % 2))
```
