# QUEUES

## WHAT IS A QUEUE?
A __FIFO__ data structure

First In First Out

```javascript
1,2,3,4
[1,2,3,4]
[2,3,4]
[3,4]
[4]
[]
```

### A Queue Class

```javascript
class Queue {
    constructor(){
        this.first = null;
        this.last = null;
        this.size = 0;
    }
}
```
```javascript
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}
```

## Enqueue
Adding to the __beginning__ of the Queue!

### Enqueue Pseudocode
- This function accepts some value
- Create a new node using that value passed to the function
- If there are no nodes in the queue, set this node to be the first and last property of the queue
- Otherwise, set the next property on the current last to be that node, and then set the last property of the queue to be that node
- Increment the size of the queue by 1

## Dequeue
Removing from the __beginning__ of the Queue!

### Dequeue pseudocode
- If there is no first property, just return null
- Store the first property in a variable
- See if the first is the same as the last (check if there is only 1 node). If so, set the first and last to be null
- If there is more than 1 node, set the first property to be the next property of first 
- Decrement the size by 1
- Return the value of the node dequeued

```javascript
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}

class Queue {
    constructor(){
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    enqueue(val){
        var newNode = new Node(val);
        if(!this.first){
            this.first = newNode;
            this.last = newNode;
        } else {
            this.last.next = newNode;
            this.last = newNode;
        }
        return ++this.size;
    }

    dequeue(){
        if(!this.first) return null;

        var temp = this.first;
        if(this.first === this.last) {
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return temp.value;
    }
}
```
