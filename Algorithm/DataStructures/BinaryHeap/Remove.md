# Removing
- Remove the root
- Replace with the most recently added
- Adjust (sink down)

## REMOVING
- Swap the first value in the values property with the last one
- Pop from the values property, so you can return the value at the end.
- Have the new root "sink down" to the correct spot...​
  - Your parent index starts at 0 (the root)
  - Find the index of the left child: 2 * index + 1 (make sure its not out of bounds)
  - Find the index of the right child: 2*index + 2 (make sure its not out of bounds)
  - If the left or right child is greater than the element...swap. If both left and right children are - larger, swap with the largest child.
  - The child index you swapped to now becomes the new parent index.  
  - Keep looping and swapping until neither child is larger than the element.
  - Return the old root!

```javascript
class MaxBinaryHeap {
    constructor(){
        this.values = [];
    }
    insert(element){
        this.values.push(element);
        this.bubbleUp();
    }
    bubbleUp(){
        let idx = this.values.length - 1;
        const element = this.values[idx];
        while(idx > 0){
            let parentIdx = Math.floor((idx - 1)/2);
            let parent = this.values[parentIdx];
            if(element <= parent) break;
            this.values[parentIdx] = element;
            this.values[idx] = parent;
            idx = parentIdx;
        }
    }

    extractMax(){
        const max = this.values[0];
        const end = this.values.pop();
        if(this.values.lengs > 0){
            this.values.[0] = end;
            this.sinkDown();
        }
        return max;
    }
    sinkDown(){
      let idx = 0;
      const length = this.values.length;
      const element = this.values[0];
      while(true){
          let leftChildIdx = 2 * idx + 1;
          let rightChildIdx = 2 * idx + 2;
          let leftChild,rightChild;
          let swap = null;

          if(leftChildIdx < length){
              leftChild = this.values[leftChildIdx];
              if(leftChild > element){
                  swap = leftChildIdx;
              }
          }
          if(rightChildIdx < length){
              rightChild = this.values[rightChildIdx];
              if(
                  (swap === null && rightChild > element) ||
                  (swap !== null && rightChild > leftChiild)
              ) {
                  swap = rightChildIdx;
              }
          }
          if(swap === null) break;
          this.values[idx] = this.values[swap];
          this.values[swap] = element;
          idx = swap;
      }
    }
}

let heap = new MaxBinaryHeap();
heap.insert(41);
heap.insert(39);
heap.insert(33);
heap.insert(18);
heap.insert(27);
heap.insert(12);
heap.insert(55);



```
