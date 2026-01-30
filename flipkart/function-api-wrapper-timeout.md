Problem: Implement a function that wraps the API with a 300ms response window

Solution:
```js
function callWithTimeout(fn, options) {
  const TIMEOUT_MS = 300;
  
  const attempt = (fn) => {
    let timeoutId;
    
    return new Promise.race([fn(), new Promise((res, rej) => {
      timeoutId = setTimeout(function() {
        rej("Timeout: API did not respond in time");
      }, TIMEOUT_MS);
    })]).
    finally(() => clearTimeout(timeoutId))
  }
  
  return attempt().catch((err) => {
    if(options.retry) {
      return attempt();
    }
    
    throw err;
  })
}


```
