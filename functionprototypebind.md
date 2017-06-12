# Function.prototype.bind

W języku JavaScript możemy zmieniać kontekst, czyli zmienną this wewnątrz funkcji. Służą do tego trzy funkcje [_call_](/zmienna-arguments-oraz-metody-call-i-apply.md), [_apply _](/zmienna-arguments-oraz-metody-call-i-apply.md)oraz _bind_. Funkcje _call_ oraz _apply_  są bardzo podobne **wywołują **one daną funkcje, zmieniając kontekst. Do funkcji call przekazujemy listę argumentów po przecinku natomiast do funkcji apply tablicę argumentów. Natomiast funkcja bind **zwraca nową funkcję**, w której kontekst jest zmieniony.

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

[https://codepen.io/Bigismall/pen/PjzZzj](https://codepen.io/Bigismall/pen/PjzZzj)

Widzimy tu, że `isDoingMethod`  jest funkcją wiążącą metodę `isDooing()` oraz obiekt manager.

Funkcję  bind łatwo zaimplementować wykorzystując call lub apply.  O [protypowaniu ](/prototypowanie-w-javascript.md)jeszcze sobie opowiemy.

```js
if (!Function.prototype.bind) {
    Function.prototype.bind = function (thisArg) {
        var fn = this,
            args = Array.prototype.slice.call(arguments, 1);

        return function () {
            return fn.apply(thisArg, args.concat(Array.prototype.slice.call(arguments)));
        };
    };
}
```

---

**Źródła:**

* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Function/bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
* [http://jcubic.pl/2014/08/funkcje-w-javascript.html](http://jcubic.pl/2014/08/funkcje-w-javascript.html)



