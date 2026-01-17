Problem: Create a polyfill for Function.prototype.bind that binds a function to a specific this context and allows pre-setting arguments. The polyfill should also handle edge cases where the bound function is used as a constructor.

Solution:
```js
const obj = {
  name: "hritik"
}

function getName(name1, name2) {
  return "my name is " + this.name + " " + name1 + " " + name2;
}

function myBind(obj, ...args1) {
  const key = Symbol();
  obj[key] = this;
  
  return (...args2) => {
    const callback = obj[key](...args1, ...args2);
    delete obj[key];
    
    return callback
  }
}

Function.prototype.myBind = myBind;

console.log(getName.myBind(obj, "hritik2")("hritik3"))
```
