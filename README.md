# notes
http://dillinger.io/ - tool for editing
## Some question about js

### 1. How to write a function to object ptototype?
 ```
 make a doubler of arrays elements
 Exmpl: [1,2,3] => dosmth => [2,4,6]
 ```
 #### Answer
 ```javascript
 let arr = [1,2,3]
 Array.prototype.doubler = function() {
    return this.map(elem => 2*elem)
}
arr.doubler() => [2,4,6]
```
### 2. Добавьте всем функциям в прототип метод defer(ms), который возвращает обёртку, откладывающую вызов функции на ms миллисекунд
```
function f(a, b) {
  alert( a + b );
}
f.defer(1000)(1, 2); // выведет 3 через 1 секунду
```
#### Answer
```
Function.prototype.defer = function(ms) {
  var f = this;
  return function() {
    var args = arguments,
      context = this;
    setTimeout(function() {
      f.apply(context, args);
    }, ms);
  }
}

// проверка
function f(a, b) {
  alert( a + b );
}

f.defer(1000)(1, 2); // выведет 3 через 1 секунду.
```
### 3. https://spin.atomicobject.com/2011/04/10/javascript-don-t-reassign-your-function-arguments/

### 4. difference between throttle and debounce in lodash
 https://css-tricks.com/debouncing-throttling-explained-examples/
