# notes
http://dillinger.io/ - tool for editing
## Some question about js

### 1. How to write a function to object ptototype?
 ```
 make a doubler of arrays elements
 Exmpl: [1,2,3] => dosmth => [2,4,6]
 ```
 ###Answer
 ```javascript
 let arr = [1,2,3]
 Array.prototype.doubler = function() {
    return this.map(elem => 2*elem)
}
arr.doubler() => [2,4,6]
