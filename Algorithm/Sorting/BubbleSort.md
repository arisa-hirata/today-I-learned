## BUbbleSort

A sorting algorithm where the largest values bubble up to the top!

## BubbleSort Pseducode

- Start looping from a variable called i the end of the array towards the beggining.
- Start an inner loop with a variable called j from the beggining until i -1.
- If arr[j] is greate than arr[j+1], swap those tho values.
- Return the sorted array.

```javascript
function bubbleSotr(arr) {
  for (var i = arr.length; i > 0; i--) {
    for (var j = 0; j < i - 1; j++) {
      console.log(arr, arr[j], arr[j + 1]);
      if (arr[j] > arr[j + 1]) {
        //SWAP!
        var temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
    console.log('ONE PASS COMPLETE');
  }
  return arr;
}

bubbleSort([37, 45, 29, 8, 12, 88, -3]);
```

            ⇩ES2015 ver

```javascript
function bubbleSort(arr) {
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  };

  for (let i = arr.length; i > 0; i--) {
    for (let j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        swap(arr, j, j + 1);
      }
    }
  }
  return arr;
}
```

#### Optimized with noSwaps

```javascript
function bubbleSort(arr) {
  var noSwaps;
  for (var i = arr.length; i > 0; i--) {
    noSwaps = true;
    for (var j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        var temp = arr[j];
        arr[j + 1] = temp;
        noSwaps = false;
      }
    }
    if (noSwaps) break;
  }
  return arr;
}
```
