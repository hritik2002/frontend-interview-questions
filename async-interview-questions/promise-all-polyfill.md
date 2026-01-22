Problem: Write a polyfill of promise

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
    res("resolve p3")
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

function all(arr) {
  return new Promise((res, rej) => {
    const result = new Array(arr.length);
    let len = 0;

    for(const [index, item] of arr.entries()) {
      item.then((val) => {
        result[index] = val;
        len++;
        
        if(len === arr.length) {
          res(result)
        }
      }).catch(err => {
        rej(err);
      });
    }
    
    
  })
}

all([p1, p2, p3]).then(res => console.log("results ", res)).catch(err => console.log(err))
```
