# STACK

## WHAT IS A STACK?
A __LIFO__ data structure!  

The last element added to the stack will be the first element removed from the stack
（先頭に入り込んで先頭から抜ける）
```javascript
push(1)
push(2)
push(3)
   ⇩
[3,2,1]   


pop()
// 3
[2,1]
pop()
// 2
```

### WHERE STACKS ARE USED
- Managing function invocations
- Undo / Redo
- Routing (the history object) is treated like a stack!

## A STACK CLASS
```javascript
class Stack {
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
## PUSHING
__Add__ a value to the __top__ of the stack

### PUSHING PSEUDOCODE
- The function should accept a value
- Create a new node with that value
- If there are no nodes in the stack, set the first and last property to be the newly created node 
- If there is at least one node, create a variable that stores the current first property on the stack
- Reset the first property to be the newly created node
- Set the next property on the node to be the previously created variable
- Increment the size of the stack by 1

## POP
__Remove__ a value from the __top__ of the stack!

### POP PSEUDOCODE
- If there are no nodes in the stack, return null
- Create a temporary variable to store the first property on the stack
- If there is only 1 node, set the first and last property to be null
- If there is more than one node, set the first property to be the next property on the current first
- Decrement the size by 1
- Return the value of the node removed


```javascript
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}

class Stack {
    constructor(){
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    push(val){
        var newNode = new Node(val);
        if(!this.first){
            this.first = newNode;
            this.last = newNode;
        } else {
            var temp = this.first;
            this.first = newNode;
            this.first.next = temp;
        }
        return ++this.size;
    }
    pop(){
        if(!this.first) return null;
        var temp = this.first;
        if(this.first === this.last){
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return temp.value;
    }
}
```

## BIG O of STACKS
Insertion -   __O(1)__
Removal -   __O(1)__
Searching -   __O(N)__
Access -   __O(N)__


## RECAP
- Stacks are a __LIFO__ data structure where the last value in is always the first one out.
- Stacks are used to handle function invocations (the call stack), for operations like undo/redo, and for routing (remember pages you have visited and go back/forward) and much more!
- They are not a built in data structure in JavaScript, but are relatively simple to implement
- Insert and remove are both __O(1)__
