# Function.prototype.bind

W języku JavaScript możemy zmieniać kontekst, czyli zmienną this wewnątrz funkcji. Służą do tego trzy funkcje [_call_](/zmienna-arguments-oraz-metody-call-i-apply.md), [_apply _](/zmienna-arguments-oraz-metody-call-i-apply.md)oraz _bind_. Funkcje _call _oraz _apply _są bardzo podobne **wywołują **one daną funkcje, zmieniając kontekst. Do funkcji call przekazujemy listę argumentów po przecinku natomiast do funkcji apply tablicę argumentów. Natomiast funkcja bind **zwraca nową funkcję**, w której kontekst jest zmieniony.

Nawiązując do przykładu z poprzedniego rozdziału, zamiast pożyczać funkcję i próbować ja wywołać, zbindujmy ją kontekstem _manager_.

```js
var developer = {
        work: "copy-pasting, stack overflow reading",
        isDoing: function () {
            console.log("My everyday work is " + this.work);
        }
    },
    manager = {
        work: "Outlook programming"
    },
    isDoingMethod = developer.isDoing.bind(manager); //binging z kontekstem manager

developer.isDoing();                                //My everyday work is copy-pasting, stack overflow reading
isDoingMethod();                                    //My everyday work is Outlook programming
```



