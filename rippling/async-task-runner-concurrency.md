Problem: Design and implement an TaskRunner utility that processes asynchronous tasks with a maximum concurrency limit. The utility should ensure that at most a defined number of tasks (concurrency) are running at any given time. If more tasks are pushed into the queue when the limit is reached, they should wait until at least one running task is completed before execution.

Solution:
```js
class TaskRunner {
  
  constructor(limit) {
    this.limit = limit;
    this.queue = []
    this.running = 0;
  }
  
  async push(cb) {
    this.queue.push(cb);
    this._run();
  }
  
  async _run() {
    while(this.running < this.limit && this.queue.length > 0) {
      const task = this.queue.shift();
      this.running++;
      
      Promise.resolve()
      .then(task)
      .finally(() => {
        this.running--;
        this._run();
      })
    }
    
    
  }
}

const ex = new TaskRunner(3);

const delay = async (timeMs) => new Promise((res) => setTimeout(res, timeMs));

// Simulated async tasks
const t1 = async () => { console.log('t1 started'); await delay(2000); console.log('t1 finished'); };
const t2 = async () => { console.log('t2 started'); await delay(1000); console.log('t2 finished'); };
const t3 = async () => { console.log('t3 started'); await delay(1500); console.log('t3 finished'); };
const t4 = async () => { console.log('t4 started'); await delay(1000); console.log('t4 finished'); };
const t5 = async () => { console.log('t5 started'); await delay(500); console.log('t5 finished'); };

// Add tasks to the executor
ex.push(t1);  // Starts immediately
ex.push(t2);  // Starts immediately
ex.push(t3);  // Starts immediately
ex.push(t4);  // Waits until at least one task finishes
ex.push(t5);  // Waits until another task finishes

// Expected Output (with assumed time delay):

// t1 started
// t2 started
// t3 started
// t2 finished
// t4 started
// t3 finished
// t5 started
// t1 finished
// t5 finished
// t4 finished
```
