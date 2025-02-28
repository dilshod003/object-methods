# object-methods
## Статический Object.keys()метод возвращает массив собственных перечислимых имен свойств заданного объекта, имеющих строковый ключ.
```
const object1 = {
  a: "somestring",
  b: 42,
  c: false,
};

console.log(Object.keys(object1));
// Expected output: Array ["a", "b", "c"]
```
## Описание
#### Object.keys()возвращает массив, элементы которого являются строками, соответствующими перечислимым строковым именам свойств, найденным непосредственно в object. Это то же самое, что и итерация с for...inциклом, за исключением того, что for...inцикл также перечисляет свойства в цепочке прототипов. Порядок возвращаемого массива Object.keys()такой же, как и у предоставленного for...inциклом.

### Использование Object.keys()
```
// Basic array
const arr = ["a", "b", "c"];
console.log(Object.keys(arr)); // ['0', '1', '2']

// Array-like object
const obj = { 0: "a", 1: "b", 2: "c" };
console.log(Object.keys(obj)); // ['0', '1', '2']

// Array-like object with random key ordering
const anObj = { 100: "a", 2: "b", 7: "c" };
console.log(Object.keys(anObj)); // ['2', '7', '100']

// getFoo is a non-enumerable property
const myObj = Object.create(
  {},
  {
    getFoo: {
      value() {
        return this.foo;
      },
    },
  },
);
myObj.foo = 1;
console.log(Object.keys(myObj)); // ['foo']
```

## Объект.values()
#### Статический Object.values()метод возвращает массив собственных перечислимых значений свойств заданного объекта, имеющих строковый ключ.
```
const object1 = {
  a: "somestring",
  b: 42,
  c: false,
};

console.log(Object.values(object1));
// Expected output: Array ["somestring", 42, false]

```
### Описание
#### Object.values()возвращает массив, элементы которого являются значениями перечислимых строковых свойств, найденных непосредственно в object. Это то же самое, что и итерация с for...inциклом, за исключением того, что for...inцикл также перечисляет свойства в цепочке прототипов. Порядок возвращаемого массива Object.values()такой же, как и у предоставляемого for...inциклом.

### Использование Object.values()
```
const obj = { foo: "bar", baz: 42 };
console.log(Object.values(obj)); // ['bar', 42]

// Array-like object
const arrayLikeObj1 = { 0: "a", 1: "b", 2: "c" };
console.log(Object.values(arrayLikeObj1)); // ['a', 'b', 'c']

// Array-like object with random key ordering
// When using numeric keys, the values are returned in the keys' numerical order
const arrayLikeObj2 = { 100: "a", 2: "b", 7: "c" };
console.log(Object.values(arrayLikeObj2)); // ['b', 'c', 'a']

// getFoo is a non-enumerable property
const myObj = Object.create(
  {},
  {
    getFoo: {
      value() {
        return this.foo;
      },
    },
  },
);
myObj.foo = "bar";
console.log(Object.values(myObj)); // ['bar']
```

## Метод call
```
func.call(context, arg1, arg2, ...)
При этом вызывается функция func, первый аргумент call становится её this, а остальные передаются «как есть».
```

Вызов func.call(context, a, b...) – то же, что обычный вызов func(a, b...), но с явно указанным this(=context).

Например, у нас есть функция showFullName, которая работает с this:
```
function showFullName() {
  alert( this.firstName + " " + this.lastName );
}
```
### Пока объекта нет, но это нормально, ведь JavaScript позволяет использовать this везде. Любая функция может в своём коде упомянуть this, каким будет это значение – выяснится в момент запуска.

Вызов showFullName.call(user) запустит функцию, установив this = user, вот так:
```
function showFullName() {
  alert( this.firstName + " " + this.lastName );
}

var user = {
  firstName: "Василий",
  lastName: "Петров"
};

// функция вызовется с this=user
showFullName.call(user) // "Василий Петров"
```

После контекста в call можно передать аргументы для функции. Вот пример с более сложным вариантом showFullName, который конструирует ответ из указанных свойств объекта:
```
var user = {
  firstName: "Василий",
  surname: "Петров",
  patronym: "Иванович"
};

function showFullName(firstPart, lastPart) {
  alert( this[firstPart] + " " + this[lastPart] );
}

// f.call(контекст, аргумент1, аргумент2, ...)
showFullName.call(user, 'firstName', 'surname') // "Василий Петров"
showFullName.call(user, 'firstName', 'patronym') // "Василий Иванович"
```

## Метод apply
#### Если нам неизвестно, с каким количеством аргументов понадобится вызвать функцию, можно использовать более мощный метод: apply.

Вызов функции при помощи func.apply работает аналогично func.call, но принимает массив аргументов вместо списка.
```
func.call(context, arg1, arg2);
// идентичен вызову
func.apply(context, [arg1, arg2]);
```

В частности, эти две строчки сработают одинаково:
```
showFullName.call(user, 'firstName', 'surname');

showFullName.apply(user, ['firstName', 'surname']);
```

```
При помощи apply мы могли бы найти максимум в произвольном массиве, вот так:

var arr = [];
arr.push(1);
arr.push(5);
arr.push(2);

// получить максимум из элементов arr
alert( Math.max.apply(null, arr) ); // 5
```
