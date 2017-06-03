# Prototypowanie w JavaScript

## Prototyp

Prototyp jest obiektem \(jak większość rzeczy w JS\) i każda tworzona funkcja automatycznie uzyskuje właściwość `prototype`, która wskazuje na nowy pusty obiekt. Jest on niemalże taki sam, jak gdyby utworzyć go za pomocą składni skróconej \({}\) lub konstruktora `Object()`, ale właściwość _constructor_ wskazuje na utworzoną funkcję, a nie na wbudowany obiekt `Object()`. Do tego nowego i pustego obiektu dodaje się właściwości i funkcje, a inne obiekty dziedziczące po nim mogą z nich korzystać, tak jakby były one ich własnymi właściwościami i funkcjami.

> W języku JavaScript prototype to właściwość funkcji i obiektów, które są tworzone przez funkcje konstruktora.Prototyp funkcji jest obiektem.Znajduje podstawowe zastosowanie, gdy funkcja jest używana jako konstruktor.

```
console.log(typeof  Object.prototype);          //object
console.log(typeof  Number.prototype);          //object
console.log(typeof  String.prototype);          //object
console.log(typeof  Function.prototype);        //function - W JavaScript'cie właściwie każda funkcja jest obiektem Function.
```

### Przykłady prototypów obiektów wbudowanych

#### String

```
String.prototype.charAt()
String.prototype.charCodeAt()
String.prototype.codePointAt()
String.prototype.concat()
String.prototype.endsWith()
String.prototype.includes()
String.prototype.indexOf()
String.prototype.lastIndexOf()
String.prototype.localeCompare()
String.prototype.match()
String.prototype.normalize()
String.prototype.repeat()
String.prototype.replace()
String.prototype.search()
String.prototype.slice()
String.prototype.split()
String.prototype.startsWith()
String.prototype.substr()
String.prototype.substring()
String.prototype.toLocaleLowerCase()
String.prototype.toLocaleUpperCase()
String.prototype.toLowerCase()
String.prototype.toString()
String.prototype.toUpperCase()
String.prototype.trim()
String.prototype.trimLeft()
String.prototype.trimRight()
String.prototype.valueOf()
String.prototype[@@iterator]()
String.raw()
```

#### Object

```
Object.assign()
Object.create()
Object.defineProperties()
Object.defineProperty()
Object.entries()
Object.freeze()
Object.getNotifier()
Object.getOwnPropertyDescriptor()
Object.getOwnPropertyDescriptors()
Object.getOwnPropertyNames()
Object.getOwnPropertySymbols()
Object.getPrototypeOf()
Object.is()
Object.isExtensible()
Object.isFrozen()
Object.isSealed()
Object.keys()
Object.prototype.hasOwnProperty()
Object.prototype.isPrototypeOf()
Object.prototype.propertyIsEnumerable()
Object.prototype.toLocaleString()
Object.prototype.toSource()
Object.prototype.toString()
Object.prototype.unwatch()
Object.prototype.valueOf()
Object.prototype.watch()
Object.seal()
Object.setPrototypeOf()
Object.values()
```





[https://developer.mozilla.org/pl/docs/Web/JavaScript/Wprowadzenie\_do\_programowania\_obiektowego\_w\_jezyku\_JavaScript](https://developer.mozilla.org/pl/docs/Web/JavaScript/Wprowadzenie_do_programowania_obiektowego_w_jezyku_JavaScript)

