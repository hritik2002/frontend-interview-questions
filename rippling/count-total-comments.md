You are tasked with creating a function that counts the total number of comments in a nested comment thread, similar to what you might find on platforms like Reddit, Twitter, or any discussion forum. Each comment can have multiple replies, and those replies can themselves have replies, creating a tree-like structure.


```js
Examples
const comments = {
  text: "some comment",
  replies: [
    { text: "some comment 1", replies: [] },
    { text: "some comment 2", replies: [] },
    { text: "some comment 3", replies: [
        { text: "some comment 5", replies: [] }
      ]
    }
  ]
};

// Should return 5
countComments(comments);

```

Solution:
```js
const comments = {
  text: "some comment",
  replies: [
    { text: "some comment 1", replies: [] },
    { text: "some comment 2", replies: [] },
    { text: "some comment 3", replies: [
        { text: "some comment 5", replies: [] }
      ]
    }
  ]
};

const countComments = (comments) => {
  let total = 0;
  const {replies} = comments;
  
  if(replies.length == 0) return total;
  
  replies.map(reply => {
    total += countComments(reply) + 1;
  })
  
  return total;
}

console.log(countComments(comments))
```
