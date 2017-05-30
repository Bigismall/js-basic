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





