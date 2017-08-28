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

### 5. bind and new
 ```javascript
 function foo(something) {
  this.a = something;
 }
 var obj1 = {};
 var bar = foo.bind( obj1 );
 bar( 2 );
 console.log( obj1.a ); // what's gonna be here?
 var baz = new bar( 3 );
 console.log( obj1.a ); // and here?
 console.log( baz.a ); // here? why?
 ```
 
bar жестко связан с obj1, но new bar(3) не меняет obj1.a на значение 3 что было бы ожидаемо нами. Вместо этого жестко связанный (с obj1) вызов bar(..) может быть перекрыт с new. Поскольку был применен new, обратно мы получили новый созданный объект, который мы назвали baz, и в результате видно, что в baz.a значение 3.

как перекрыть new?

использвоать полифилл:
```javascript
if (!Function.prototype.bind) {
	Function.prototype.bind = function(oThis) {
		if (typeof this !== "function") {
			// наиболее подходящая вещь в ECMAScript 5
			// внутренняя функция IsCallable
			throw new TypeError( "Function.prototype.bind - what " +
				"is trying to be bound is not callable"
			);
		}
		var aArgs = Array.prototype.slice.call( arguments, 1 ),
			fToBind = this,
			fNOP = function(){},
			fBound = function(){
				return fToBind.apply(
					(
						this instanceof fNOP &&
						oThis ? this : oThis
					),
					aArgs.concat( Array.prototype.slice.call( arguments ) )
				);
			}
		;
		fNOP.prototype = this.prototype;
		fBound.prototype = new fNOP();

		return fBound;
	};
}
 ```
