Problem: You have to implement a function called race that takes an array of promises as input. It should return a promise that fulfills or rejects as soon as one of the promises in the input array fulfills or rejects, with the value or reason from that promise.


Solution: 

```js
const p1 = new Promise((res, rej) => {
  setTimeout(function() {
    res("resolved p1")
  }, 10);
})

const p2 = new Promise((res, rej) => {
  setTimeout(function() {
    res("resolved p2")
  }, 200);
})

const p3 = new Promise((res, rej) => {
  setTimeout(function() {
    rej("rejected p3")
  }, 100);
})

function race(arr) {
  return new Promise((res, rej) => {
    for(const item of arr) {
      item.then((val) => {
        res(val)
      }).catch(err => {
        rej(err)
      });
    }
  })
}

race([p1, p2, p3]).then(val => console.log("val", val)).catch(err => console.log(err))
```
