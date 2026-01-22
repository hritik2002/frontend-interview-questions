Problem:Implement a method named clearAllTimeout that, when called, clears all active timeouts previously set by setTimeout.

Solution:

```js
const originalSetTimeout = window.setTimeout;
const originalClearTimeout = window.clearTimeout;
const activeTimeouts = new Set();

window.setTimeout = (fn, delay, ...args) => {
  const id = originalSetTimeout(function(...cbArgs) {
    activeTimeouts.delete(id);
    fn(...cbArgs);
  }, delay, ...args);
  activeTimeouts.add(id);
  
  return id;
}

window.clearTimeout = (id) => {
  activeTimeouts.delete(id);
  
  return originalClearTimeout(id);
}

window.clearAllTimeout = () => {
  for(const id of activeTimeouts) {
    originalClearTimeout(id);
  }
  
  activeTimeouts.clear()
}

setTimeout(() => console.log("One"), 400);
setTimeout(clearAllTimeout, 500);
setTimeout(() => console.log("Three"), 600);
setTimeout(() => console.log("Four"), 200);


```
