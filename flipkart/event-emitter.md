Problem: mplement an Event Emitter class that can be used for the publisher-subscriber mechanism in JavaScript

Solution:

```js
function Emitter() {
  const cache = new Map();
  
  const subscribe = (eventName, callbackFn) => {
    if(!cache.get(eventName)) {
      cache.set(eventName, new Set());
    }
    
    const listener = cache.get(eventName);
    listener.add(callbackFn);
    
    const release = () => {
      listener.delete(callbackFn);
      
      if(listener.size === 0) {
        cache.delete(eventName);
      }
    }
    
    return {
      release
    }
  }
  
  const emit = (eventName, ...args) => {
    if(!cache.get(eventName)) {
      return;
    }
    
    const listeners = cache.get(eventName);
    listeners.forEach((cb) => {
      cb(...args);
    });
  }
  
  return {
    subscribe,
    emit
  }
}


const emitter = new Emitter();
// Allows you to subscribe to some event

const callback1 = (arg1) => console.log("callback1", arg1)
const callback2 = (arg1, arg2) => console.log("callback2", arg1, arg2)

const sub1 = emitter.subscribe('event_name', callback1);
// you can have multiple callbacks to the same event
const sub2 = emitter.subscribe('event_name', callback2);
// You can emit the event you want with this API (you can receive 'n' number of arguments)

emitter.emit('event_name', "foo", "bar");

// And allows you to release the subscription like this (but you should be able to still emit from sub2)

sub1.release();

console.log("released")
emitter.emit('event_name', "foo", "bar");
```
