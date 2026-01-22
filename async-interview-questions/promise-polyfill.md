problem: Polyfill of promise.

Solution:

```js
class MPromise {
  STATUS = {
    PENDING: "PENDING",
    FULFILLED: "FULFILLED",
    REJECTED: "REJECTED"
  }
  fulFilledHandlers = [];
  rejectedHandlers = [];
  value = undefined;
  error = undefined;
  status = this.STATUS.PENDING;
  
  constructor(exec) {
    exec((val) => this._promiseResolver(val), (err) => this._promiseRejected(err))
  }
  
  then(thenHandler) {
    if(this.status === this.STATUS.FULFILLED) thenHandler(this.value);
    else this.fulFilledHandlers.push(thenHandler);
    
    return this;
  }
  
  catch(catchHandler) {
    if(this.status === this.STATUS.REJECTED) catchHandler(this.error);
    else this.rejectedHandlers.push(thenHandler);
    
    return this;
  }
  
  _promiseResolver(val) {
    this.status = this.STATUS.FULFILLED;
    this.value = val;
    this.fulFilledHandlers.reduce((acc, fn) => fn(acc), val);
  }
  
  _promiseRejected(err) {
    this.status = this.STATUS.FULFILLED;
    this.error = err;
    this.rejectedHandlers.reduce((acc, fn) => fn(acc), err);
  }
}

const p1 = new MPromise((res, rej) => {
  console.log("inside p1");
  
  setTimeout(function() {
    res("p1 resolved");
  }, (1000));
})

p1.then(val => {
  console.log(val);
  return val + "then 1";
})
.then(val => {
  console.log(val);
  return val + "then 2"
})
.then(val => console.log(val))
```
