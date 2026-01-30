Problem:
implement the function fetchWithAutoRetry(fetcher, maximumRetryCount). This function should repeatedly call the fetcher until it succeeds or the maximum retry limit is reached

Solution:
```js
let cnt = 0;

const slowAPI = () => new Promise((res, rej) => setTimeout(() => {
  if(cnt++ <= 1) return rej("reject")
  else return res("ok");
}, 1000));



function fetchWithAutoRetry(fetcher, maximumRetryCount) {
  return fetcher().then(response => {
    return response;
  }).
  catch(err => {
    if(maximumRetryCount > 0) {
      return fetchWithAutoRetry(fetcher, maximumRetryCount - 1);
    }
    
    return err;
  })
}

fetchWithAutoRetry(slowAPI, 4)
.then((result) => console.log(result))  // Expected output: { data: 'API Data' }
  .catch((error) => console.error(error));  // If retry limit is exceeded
  
  

```
