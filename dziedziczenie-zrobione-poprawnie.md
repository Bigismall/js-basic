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
        return "I'm a car of " + this.type + " have " + this.sits + " sits  and " + this.getColor() + " color";
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

Mimo iż definiowanie klas i tworzenie instancji obiektów w pokazany sposób, przypomina już rozwiązania z innych języków programowania, to bardzo szybko zauważymy rozrastanie się konstruktora, podczas definiowania kolejnych pól i metod.

Konstruktory generują duplikaty pól i metod dla każdej z instancji obiektu.

Problem można rozwiązać na kilka sposobów

* użyć wielokrotnego dziedziczenia - co spowoduje jedynie przeniesienie czy też rozproszenie na większą ilość funkcji konstruujących.  Co więcej, w JS  dziedziczenie implementuje się za pomocą prototypów, więc za chwile okaże się, że są na to lepsze sposoby
* zdefiniować funkcje statyczne `Car.describe = function() {}` ale wówczas stracimy dostęp do `this`
* wykorzystać omówione wcześniej prototypowanie  do rozszerzenia funkcji konstruującej.

### Prototypy w funkcjach konstruujących \(klasach\)

Przypiszmy wzorem poprzedniego rozdziału, funkcję `color()` i `describe()` do prototypu funkcji konstruującej, pola \(właściwości\) pozostawiając bez zmian, w konstruktorze.

```js
function Car(color, sits, type) {
    this.color = color;
    this.sits = parseInt(sits, 10);
    this.type = type;
}

Car.prototype.getColor = function () {
    return this.color;
}

Car.prototype.describe = function () {
    return "I'm a car of " + this.type + " have " + this.sits + " sits  and " + this.getColor() + " color";
}

var mercedes = new Car("silver", 5, "limousine"),
    bmw = new Car("red", 2, "coupe");


console.log(mercedes.describe());   //I'm a car of limousine have 5 sits  and silver color
console.log(bmw.describe());    //I'm a car of coupe have 2 sits  and red color
```

Dzięki powyższemu  zyskaliśmy pamięć, bo tworzone są tylko jedne egzemplarze funkcji `color()` i `describe()`, zachowując elastyczność  i indywidualność instancji obiektu.





[https://developer.mozilla.org/pl/docs/Web/JavaScript/Wprowadzenie\_do\_programowania\_obiektowego\_w\_jezyku\_JavaScript](https://www.gitbook.com/book/bigismall/js-basic/edit#)

[http://bonsaiden.github.io/JavaScript-Garden/pl/\#object.prototype](http://bonsaiden.github.io/JavaScript-Garden/pl/#object.prototype)

