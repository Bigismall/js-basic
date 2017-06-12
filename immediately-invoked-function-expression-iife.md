# Immediately Invoked Function Expression \(IIFE\)

## Natychmiastowo-wywoływane wyrażenie funkcyjne

Natychmiastowo-wywoływane wyrażenie funkcyjne, jest często stosowane w języku JavaScript, ponieważ w języku tym bloki nie tworzą nowego zakresu zmiennych, tak jak to ma miejsce w przypadku języka **Java **czy **C**. Stosuje się je także aby odizolować część kodu od reszty programu. Jej konstrukcja polega na zamknięciu całej funkcji w nawiasy \(może być to funkcja anonimowa\) i natychmiastowym jej wywołaniu.  Zapis taki tworzy [**domknięcie**](/closures.md).

```js
(function () {
    console.log('SolwIT');
}());
```

[https://codepen.io/Bigismall/pen/qjNOMw](https://codepen.io/Bigismall/pen/qjNOMw)

Powyższy skrypt spowoduje wypisanie w konsoli napisu "SolwIT".   Skoro wspomniano już o [domknięciu ](/closures.md)i [zakresie funkcyjnym](/scoping.md), prześledźmy kolejny skrypt.

```js
var solwIT = 'SolwIT';

(function () {
    var intel = 'Intel';
    console.log(solwIT);
    console.log(intel);
}());

try {
    console.log(solwIT);
    console.log(intel);
} catch (e) {
    console.warn(e.message);
}
```

[https://codepen.io/Bigismall/pen/QgEjZM](https://codepen.io/Bigismall/pen/QgEjZM)

w wyniku powyższego otrzymamy:

```
SolwIT
Intel
SolwIT
intel is not defined
```

**Info:** _W EcmaScript 6 zamiast tworzenia funkcji IIFE  dla powyższego przykładu, można wykorzystać  operator _`let`_ oraz nawiasy _`{ }`_._

### Parametry funkcji natychmiastowych

Do funkcji natychmiastowych można także przekazać argumenty, co przedstawia poniższy przykład.

```js
(function (message, a, b) {
    console.log(message, a + b);                //SolwIT JS Basic. And the sum is:  5
}("SolwIT JS Basic. And the sum is: ", 2, 3));
```

[https://codepen.io/Bigismall/pen/xrOwyB](https://codepen.io/Bigismall/pen/xrOwyB)

Bardzo często jako argument funkcji podaje się  [obiekt globalny](/scoping.md), by był on dostępny wewnątrz funkcji, bez potrzeby korzystania z np. nazwy  `window`. Rozwiązanie to czyni kod bardziej przenośnym, bo działa prawidłowo w środowiskach innych niż przeglądarka internetowa.

```js
(function (global) {
    if (global.hasOwnProperty('alert')) {
        console.log('Uruchamiasz mnie w przeglądarce');
    } else {
        console.log('Uruchamiasz mnie poza przeglądarką');
    }
}(this));
```

[https://codepen.io/Bigismall/pen/NgrGEg](https://codepen.io/Bigismall/pen/NgrGEg)

W przykładzie powyżej przekazano this, będącym referencją do obiektu globalnego.  W zależności od posiadania przez obiekt globalny właściwości `alert`, wyświetlony zostanie odpowiedni komunikat.

### Wartości zwracane przez funkcje natychmiastowe

Podobnie jak każda inna funkcja, także funkcja natychmiastowa może zwrócić wartość, a ta może zostać przypisana do zmiennej.

```js
var sumResult = (function (a, b) {
    return a + b;
}(2, 5));

console.log(sumResult);     //7
```

[https://codepen.io/Bigismall/pen/KqMdJZ](https://codepen.io/Bigismall/pen/KqMdJZ)

Może też zwrócić: funkcję  \([co przyda nam się w dalszych rozdziałach](/closures.md)\), obiekt lub sama być użyta w konstrukcji obiektu

```js
var sum = (function () {
    return function (a, b) {
        return a + b;
    }
}());

console.log(sum);            // [Function]
console.log(sum(2, 4));      // 6
```

[https://codepen.io/Bigismall/pen/GEqpeq](https://codepen.io/Bigismall/pen/GEqpeq)

## Zalety i zastosowanie

Wzorzec funkcji natychmiastowej stosowany jest powszechnie. Pozwala na wykonanie określonych zadań bez zaśmiecania przestrzeni globalnej zmiennymi tymczasowymi. Wszystkie zdefiniowane zmienne są lokalne względem funkcji natychmiastowej i nie wyjdą poza nią, chyba że programista zadecyduje inaczej.

Wzorzec pozwala umieścić poszczególne zestawy funkcjonalności w szczelnych modułach. Jako przykład, szkielet definicji modułu [UMD ](https://github.com/umdjs/umd/blob/master/templates/commonjsStrictGlobal.js).

```js
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['exports', 'b'], function (exports, b) {
            factory((root.commonJsStrictGlobal = exports), b);
        });
    } else if (typeof exports === 'object' && typeof exports.nodeName !== 'string') {
        // CommonJS
        factory(exports, require('b'));
    } else {
        // Browser globals
        factory((root.commonJsStrictGlobal = {}), root.b);
    }
}(this, function (exports, b) {
    //use b in some fashion.

    // attach properties to the exports object to define
    // the exported module properties.
    exports.action = function () {};
}));
```



