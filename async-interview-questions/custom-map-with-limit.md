problem: implement a custom mapLimit function that takes 4 arguments


Solution:
```js
/** Do not delete or change any function name **/

function getUserById(id, callback) {
  // simulating async request
  const randomRequestTime = Math.floor(Math.random() * 100) + 200;
 
  setTimeout(() => {
    callback("User" + id)
  }, randomRequestTime);
}

function mapLimit(inputs, limit, iterateeFn, callback) {
  // write your solution here
  let running = 0, processedTaks = 0, totalSize = inputs.length;
  let index = 0, completed = 0;
  const allResults = Array(totalSize)

  function rec() {
    if(completed == totalSize) {
      callback(allResults);
      return;
    }
    while(running < limit && index < totalSize) {
      running++;
      const currentIndex = index;
      iterateeFn(inputs[index++], (item) => {
        allResults[currentIndex] = item;
        running--;
        completed++;
        rec()
      });
    }
  }
  
  rec()
}

mapLimit([1,2,3,4,5], 2, getUserById, (allResults) => {
  console.log('output:', allResults) // ["User1", "User2", "User3", "User4", "User5"]
})
```
