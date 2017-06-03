# Dziedziczenie zrobione poprawnie

Zanim przejdziemy do tematu dziedziczenia i jego przykładowych implementacji, przypomnijmy sposób realizacji klas w języku JavaScript.  Przypomnijmy wzorzec konstruktora.

Pierwszy krok to wybór nazwy klasy, która staje się nazwą  konstruktora. Tradycyjnie nazwa ta zaczyna się od wielkiej litery, dla wskazania iż chodzi o funkcję  konstruującą.  

```js
function Car(color, sits, type) {
    this.color = color;
    this.sits = parseInt(sits, 10);
    this.type = type;

    this.getColor = function () {
        return this.color;
    }

    this.describe = function () {
        return "I'm a car of " + this.type + " have " + this.sits + " sits  and " + this.color + " color";
    }
}
```

Zauważmy, że funkcja konstruująca \(konstruktor\) niczego nie zwraca, metody i pola \(właściwości\) są zaś przypisywane za pomocą operatora `this`. Kiedy konstruktor zostanie wywołany operatorem `new`, obiekt będzie stworzony, zanim jeszcze dojdzie do wykonania pierwszego kodu konstruktora. Dostęp do tego obiektu \(w tym momencie\) możliwy jest tylko poprzez `this`. Możliwe jest więc przypisywanie bezpośrednio do this  właściwości które zostaną domyślnie zwrócone jako wartość funkcji \(bez konieczności używania operatora `return`\)

```js

var mercedes = new Car("silver", 5, "limousine"),
    bmw = new Car("red", 2, "coupe");


console.log(mercedes.describe());   //I'm a car of limousine have 5 sits  and silver color
console.log(bmw.describe());    //I'm a car of coupe have 2 sits  and red color

```

### 

### Prototypy w funkcjach konstruujących \(klasach\)

Język JavaScript do niedawna pozbawiony był obsługi tworzenia prawdziwych klas. Choć standard ECMAScript 2015 zapewnia klasom lukier składniowy \(syntactic sugar\), bazowy system obiektowy w dalszym ciągu pozostał bez zmian, dlatego nadal warto dowiedzieć się[ jak obiekty zostały by utworzone bez tego lukru](http://www.typescriptlang.org/play/index.html).

Rozważmy przykład prostej funkcji konstruującej.

[https://developer.mozilla.org/pl/docs/Web/JavaScript/Wprowadzenie\_do\_programowania\_obiektowego\_w\_jezyku\_JavaScript](https://www.gitbook.com/book/bigismall/js-basic/edit#)

[http://bonsaiden.github.io/JavaScript-Garden/pl/\#object.prototype](http://bonsaiden.github.io/JavaScript-Garden/pl/#object.prototype)

