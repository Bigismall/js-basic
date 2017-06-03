# Prototypowanie w JavaScript

## Prototyp

Prototyp jest obiektem \(jak większość rzeczy w JS\) i każda tworzona funkcja automatycznie uzyskuje właściwość `prototype`, która wskazuje na nowy pusty obiekt. Jest on niemalże taki sam, jak gdyby utworzyć go za pomocą składni skróconej \({}\) lub konstruktora `Object()`, ale właściwość _constructor_ wskazuje na utworzoną funkcję, a nie na wbudowany obiekt `Object()`. Do tego nowego i pustego obiektu dodaje się właściwości i funkcje, a inne obiekty dziedziczące po nim mogą z nich korzystać, tak jakby były one ich własnymi właściwościami i funkcjami.

> W języku JavaScript prototype to właściwość funkcji i obiektów, które są tworzone przez funkcje konstruktora. Prototyp funkcji jest obiektem.Znajduje podstawowe zastosowanie, gdy funkcja jest używana jako konstruktor.

```js
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

## Zastosowania prototypów

Przewijają się 2 główne zastosowania prototypów:

* modyfikowanie zdefiniowanych lub wbudowanych obiektów \(_monkey patching_\)
* [implementacja dziedziczenia](/dziedziczenie-zrobione-poprawnie.md)

### Modyfikacja obiektów

Modyfikacja właściwości _prototype_ funkcji konstruujących obiekty to wygodny i elastyczny sposób na dodawanie nowych funkcjonalności. Czasem jednak okazuje się  zbyt potężny.

Modyfikowanie prototypów obiektów wbudowanych takich jak _Object_, _Array_ lub _Function_ jest kuszące, ale w praktyce znacząco utrudni konserwację kodu, bo stanie się  on mniej przewidywalny. Inni programiści korzystający z utworzonego kodu zapewne będą oczekiwali jednolicie działających obiektów wbudowanych bez żadnych dodatków.

Co więcej, właściwości dodane do prototypu mogą pojawić się w pętlach, które nie zostały zabezpieczone testem wykorzystującym `hasOwnProperty()`, co może doprowadzić do dodatkowej konsternacji.

Z podanych powodów lepiej **nie modyfikować** wbudowanych prototypów.  Wyjątek od tej reguły stanowią sytuacje, w których spełnione zostaną  wszystkie poniższe warunki.

* Oczekuje się, ze wszystkie przyszłe wersje języka wprowadzą określoną funkcjonalność jako metodę wbudowaną, a jej implementacje będą działały identycznie. 
* Sprawdzi się, czy tworzona metoda lub właściwość już nie istnieje - być może została dodana przez inną wykorzystywaną bibliotekę lub też została udostępniona przez przeglądarkę jako część nowszego interpretera języka.
* Jasno i wyraźnie poinformujemy zespół o wprowadzeniu nowej metody

W przypadku spełnienia powyższych, można dodać własny element do prototypu, stosując następujący wzorzec:

```js
if (typeof Object.prototype.myMethod !== "function") {
    Object.prototype.myMethod = function () {

    };
}
```

lub krócej

```js
//uwaga - może istnieć właściwość myMethod
if (!Object.prototype.myMethod()) {

}
```

#### Przykłady modyfikacji obiektów wbudowanych

##### Metoda obiektu `Array` która zwraca jedynie parzyste liczby z tablicy

```js
if (typeof Array.prototype.even !== "function") {
    Array.prototype.even = function () {
        return this.filter(function (element) {
                return ( typeof element === 'number' && 0 === element % 2);
            }
        );
    };
}

var numbers = [0, 1, 2, 3, 4, 5, 6, 7, '8', 'abc', ['def'], 9, 10];

console.log(numbers.even());        //[ 0, 2, 4, 6, 10 ]
```

##### Metoda obiektu `Array` która ustawia losową kolejność elementów tablicy

```js
Array.prototype.shuffle = Array.prototype.shuffle || function () {
        return this.sort(function () {
            return 0.5 - Math.random()
        });
    }

var numbers = [0, 1, 2, 3, 4, 5, 6, 7, '8', 'abc', ['def'], 9, 10];
console.log(numbers.shuffle());
```

---

**Źródła:**

* [http://bonsaiden.github.io/JavaScript-Garden/pl/\#object.prototype](https://www.gitbook.com/book/bigismall/js-basic/edit#)



