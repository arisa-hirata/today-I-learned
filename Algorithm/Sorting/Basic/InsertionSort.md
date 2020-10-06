## Insertion Sort

BUilds up the sort by gradually creating a larger half which is always sorted.

## Insertion Sort Pseducode

- Start by picking the second element in the array
- Now compare the second element with the one before it and swap if necessary.
- Continur to the next element and if it is in the incorrect orderm iterate through the sorted portion (i.e. the left side) to place the element in the correctb place.
- Repeat until the array is sorted.

```javascript

function insertionSort(arr) {
    for (var i = 1; i < arr.length; i++) {
        var currentVal = arr[i];
        for (var j = i - 1; j>=0 && arr[j] > currentVal; j--) {
            arr[j+1] = arr[j]            
        }
        arr[j+1] = currentVal;
        console.log("arr: ", arr); 
    }
    return arr;
}

insertionSort([2,1,9,76,4])
```
