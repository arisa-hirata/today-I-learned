# Reverse a String

Given an input, return the reversed string.

example:
Input: "hello",
Output: "olleh"

```javascript
function reverseString(words) {
  return words
    .split('')
    .reverse()
    .join('');
}
```

_Integer ver_
Input: "12300",
Output:"00123"

```javascript
function reverseString(integer) {
  return integer
    .toString()
    .split('')
    .reverse()
    .join('');
}
```
