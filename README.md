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

