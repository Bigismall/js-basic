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

Przykłady prototypów obiektów wbudowanych





https://developer.mozilla.org/pl/docs/Web/JavaScript/Wprowadzenie\_do\_programowania\_obiektowego\_w\_jezyku\_JavaScript

