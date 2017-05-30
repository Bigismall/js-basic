# Immediately Invoked Function Expression \(IIFE\)

## Natychmiastowo-wywoływane wyrażenie funkcyjne

Natychmiastowo-wywoływane wyrażenie funkcyjne, jest często stosowane w języku JavaScript, ponieważ w języku tym bloki nie tworzą nowego zakresu zmiennych, tak jak to ma miejsce w przypadku języka **Java **czy **C**. Stosuje się je także aby odizolować część kodu od reszty programu. Jej konstrukcja polega na zamknięciu całej funkcji w nawiasy \(może być to funkcja anonimowa\) i natychmiastowym jej wywołaniu.  Zapis taki tworzy [**domknięcie**](/closures.md).

```js
(function () {
    console.log('SolwIT');
}());
```

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

W przykładzie powyżej przekazano this, będącym referencją do obiektu globalnego.  W zależności od posiadania przez obiekt globalny właściwości `alert`, wyświetlony zostanie odpowiedni komunikat.

### Wartości zwracane przez funkcje natychmiastowe

Podobnie jak każda inna funkcja, także funkcja natychmiastowa może zwrócić wartość, a ta może zostać przypisana do zmiennej.

```js
var sumResult = (function (a, b) {
    return a + b;
}(2, 5));

console.log(sumResult);     //7
```

Może też zwrócić funkcję  \([co przyda nam się w dalszych rozdziałach](/closures.md)\)

```
var sum = (function () {
    return function (a, b) {
        return a + b;
    }
}());
    
console.log(sum);            // [Function]
console.log(sum(2, 4));      // 6
```

Lub obiekt - co bywa stosowane przy okazji tworzenia modułów, lub np. obiektów inicjujących pewne dane

```

```



