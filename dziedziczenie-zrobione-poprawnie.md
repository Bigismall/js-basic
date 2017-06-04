# Dziedziczenie zrobione poprawnie

## Dziedziczenie w JavaScript

JavaScript nie posiada klasycznego modelu dziedziczenia. Zamiast tego dziedziczenie jest realizowane poprzez prototypy.

Choć jest to często uważane za jedną ze słabości języka JavaScript, prototypowy model dziedziczenia, jest w rzeczywistości potężniejszy od klasycznego modelu. Na przykład stworzenia klasycznego modelu na podstawie modelu prototypowego jest dość proste, podczas gdy zrobienie odwrotnego przekształcenie to o wiele trudniejsze zadanie.

Ze względu na fakt, że w JavaScript jest w zasadzie jedynym powszechnie stosowanym językiem, który posiada prototypowy model dziedziczenia, dostosowanie się do różnic pomiędzy tymi dwoma modelami wymaga trochę czasu.

### Funkcje konstruujące - klasy

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

## Dziedziczenie za pomocą łańcucha prototypów

Dziedziczenie w JavaScript odbywa się za pomocą tak zwanych łańcuchów prototypów.

```js
function Person() {
    this.weight = 100;

    this.getWeight = function () {
        return this.weight;
    };


}
function Student() {
    this.height = 180;
    this.getHeight = function () {
        return this.height;
    };
}

Student.prototype = new Person();


var student = new Student();
console.log(student.getWeight());
console.log(student.getHeight());
console.log(student instanceof Person);
console.log(student instanceof Student);
```

W powyższym przykładzie prototypem obiektów Student jest obiekt Person, dlatego instancje obiektu Student posiadają dostęp do metody `getWeight()` zdefiniowanej w obiekcie Person. Obiekty utworzone za pomocą konstruktora Student **dziedziczą **po obiekcie Person.

Prototypy tworzą łańcuch \(ang. chain\). W momencie odwołania do właściwości lub metody sprawdzane jest czy dana właściwość czy metoda dostępna jest w danym obiekcie, potem sprawdzany jest ciąg prototypów aż do obiektu Object, jeśli dana właściwość lub metoda nie zostanie znaleziona zwracana jest wartość _undefined_. W przypadku metody będzie to wyjątek że nie można wywołać funkcji która jest _undefiend_.

### Pożyczanie konstruktora

W przykładzie powyżej żadna z funkcji konstruujących nie przyjmuje parametrów, dlatego udało się  zrealizować dziedziczenie w miarę bezboleśnie. Właściwość  `student.constructor` zaś ciągle wskazuje na _Person_.  Ubogaćmy zatem ~~kulturow..~~.  klasę Person o właściwość _name_ przekazywaną jako parametr konstruktora.  Wpłynie to także na konstruktor klasy potomnej _Student_.  Przy okazji też  przypiszemy klasie student odpowiedni konstruktor.



```js

function Person(name, weight) {
    this.name = name
    this.weight = weight;

    this.getWeight = function () {
        return this.weight;
    };


}
function Student(name, weight, height) {
    Person.call(this, name, weight);

    this.height = height;
    
    this.getHeight = function () {
        return this.height;
    };
}

Student.prototype = new Person();
Student.prototype.constructor = Student;


var person = new Person('Jack Sparrow',80);
var student = new Student('Black Jack',100,185);


console.log(person.name);
console.log(person.getWeight());
console.log(person.constructor);
console.log(person instanceof Person);
console.log(person instanceof Student);


console.log(student.name);
console.log(student.getWeight());
console.log(student.getHeight());
console.log(student.constructor);
console.log(student instanceof Person);
console.log(student instanceof Student);

```









* [developer.mozilla.org/pl/docs/Web/JavaScript/Wprowadzenie\_do\_programowania\_obiektowego\_w\_jezyku\_JavaScript](https://developer.mozilla.org/pl/docs/Web/JavaScript/Wprowadzenie_do_programowania_obiektowego_w_jezyku_JavaScript)
* [http://bonsaiden.github.io/JavaScript-Garden/pl/\#object.prototype](http://bonsaiden.github.io/JavaScript-Garden/pl/#object.prototype)
* [http://jcubic.pl/2015/10/programowanie-obiektowe-w-javascript.html](http://jcubic.pl/2015/10/programowanie-obiektowe-w-javascript.html)
* [https://nafrontendzie.pl/dziedziczenie-javascript-pozyczanie-konstruktora/](https://nafrontendzie.pl/dziedziczenie-javascript-pozyczanie-konstruktora/)



