Problem Statement:
Given a deeply nested array, create a function on the array, namely flatten, that when invoked returns a flat version of the original array. Function should be defined in a way that it can be invoked on existing and future arrays.

Solution:
```js
var input = [
  1, 2, 3,
   [4],
  [5, 6, [7], [8, [9, [10]]]],
  11, 12, 13,
  [14, [[[[[15, [16]]]]]]],
  17, 18,
  [19, [20, [21, [22, [23, [24, [[[[[25]]]]]]]]]]]
 ];
 
 Array.prototype.flatten = function() {
   const getFlattenArr = (arr, res = []) => {
     arr.forEach(val => {
       if(Array.isArray(val)) {
        getFlattenArr(val, res);
       } else {
         res.push(val);
       }
     })
     
     return res;
   };
   
   
   return getFlattenArr(this);
 }
  
var flatArray = input.flatten();
console.log(flatArray)
 // flatArray: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25]
```
