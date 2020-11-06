# Hash Tablees

## WHAT IS A HASH TABLE?
Hash tables are used to store _key-value_ pairs.  
They are like arrays, but the keys are not ordered.  
Unlike arrays, hash tables are _fast_ for all of the following operations: finding values, adding new values, and removing values!

### THE HASH PART
To implement a hash table, we'll be using an array.  
In order to look up values by key, we need a way to __convert keys into valid array indices__.  
A function that performs this task is called a _hash function_.

### WHAT MAKES A GOOD HASH?
1. Fast (i.e. constant time)
2. Doesn't cluster outputs at specific indices, but distributes uniformly
3. Deterministic (same input yields same output)

### A HashTable Class

```javascript
class HashTable {
  constructor(size=53){
    this.keyMap = new Array(size);
  }

  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96
      total = (total * WEIRD_PRIME + value) % this.keyMap.length;
    }
    return total;
  }
}
```


## BIG O of HASH TABLES
(average case)  
- Insert: O(1)
- Deletion: O(1)
- Access: O(1)

## Recap
- Hash tables are collections of key-value pairs
- Hash tables can find values quickly given a key
- Hash tables can add new key-values quickly
- Hash tables store data in a large array, and work by _hashing_ the keys
- A good hash should be fast, distribute keys uniformly, and be deterministic
- Separate chaining and linear probing are two strategies used to deal with two keys that hash to the same index
- When in doubt, use a hash table!
