## What is Recursion?

A **process** (a function in this case) that **calls itself**

## The call stack

- It's a **stack** data struncture
- Any time a function is invoked it is placed (**pushed**) on the top of the call stack.
- When JavaScript sees the **return** keyword or when the function ends, the compiler will remove (**pop**)

## How recursive functions work

Invoke the **same** function with a different input until you reach your base case!

## Base Case

The condition when the recursion ends.  
**This is the most important concept to understand**

## Two essential parts of a recursive function

- Base Case
- Different Input

## Where things go wrong

- No base case
- Forgetting to return or returning the wrong thing!
- Stack overflow!

```javascript
function factorial(num) {
  if (num === 1) return 1;
  return num * factorial(num);
}
```

```javascript
function factorial(num) {
  if (num === 1) console.log(1);
  return num * factorial(num - 1);
}
```

## Helper Method Recursion

```javascript
function collectOddValues(arr) {
  let result = [];

  function helper(helperInput) {
    if (helperInput.length === 0) {
      return;
    }

    if (helperInput[0] % 2 !== 0) {
      result.push(helperInput[0]);
    }

    helper(helperInput.slice(1));
  }

  helper(arr);

  return result;
}
```

## Pure Recursion Tips

- For arrays, use methods like **slice, the spread operator,** and **concat** that make copies of arrays so you do not mutate them.
- Remember that strings are immutable so you will need to use methods like **slice, substr, or substring** to make copies of strings.
- To make copies of objects use **Object.assign, or the spread operator**
