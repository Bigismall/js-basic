# Zmienna arguments oraz metody call\(\) i apply\(\)

## Arguments

Obiekt arguments jest zmienną lokalną dostępną wewnątrz każdej funkcji.

Do argumentów wewnątrz funkcji możesz odwołać się używając obiektu `arguments`. Obiekt ten zawiera pozycję dla każdego argumentu przekazanego funkcji, przy czym indeks pierwszego z nich ma wartość 0. Na przykład, jeśli do funkcji przekazane są trzy argumenty, można się do nich odwołać w następujący sposób:

```
arguments[0]
arguments[1]
arguments[2]
```

Argumentom mogą być również przypisywane wartości:

```
arguments[1] = 'SolwIT';
```

Obiekt arguments nie jest tablicą. Jest do niej podobny, lecz nie posiada żadnej z własności tablicy poza length.  
Obiekt arguments dostępny jest wyłącznie wewnątrz ciała funkcji. Próba dostępu do obiektu arguments spoza części deklaracyjnej funkcji zakończy się błędem.

Możesz użyć obiektu arguments, jeśli funkcja wywołana jest z większą liczbą argumentów niż zostało to zadeklarowane. Jest to użyteczne dla funkcji, które wywoływać można ze zmienną liczbą argumentów. Aby określić liczbę argumentów przekazywanych do funkcji można użyć własności arguments.length, a następnie skorzystać z każdego z argumentów używając obiektu arguments \(aby określić liczbę argumentów zadeklarowanych podczas definiowania funkcji, skorzystać można z własności Function.length\).

```js
function join(separator) {
    console.log('Ciało funkcji: ', arguments.callee);
    console.log('Nazwa funkcji: ', arguments.callee.name);                                     // join
    console.log('Ilość zadeklarowanych dla funkcji parametrów: ', arguments.callee.length);    // 1
    console.log('Ilość przekazanych parametrów: ', arguments.length);                          // 7
}

join("*", "Lorem","ipsum","dolor","sit","amet","enim.");
```

[https://codepen.io/Bigismall/pen/vZKNMN](https://codepen.io/Bigismall/pen/vZKNMN)

Implementacja funkcji`join()`

```js
function join(separator) {
    var joinedString = "",
        i = 1;
    for (; i < arguments.length; i++) {
        joinedString += arguments[i] + ((i !== arguments.length - 1) ? separator : '');
    }

    return joinedString;
}
console.log(join("*", "Lorem", "ipsum", "dolor", "sit", "amet", "enim."));    //Lorem*ipsum*dolor*sit*amet*enim.
```

[https://codepen.io/Bigismall/pen/mwEeYP](https://codepen.io/Bigismall/pen/mwEeYP)

**Ważne!** Zmienna `arguments` nie jest dostępna w przypadku funkcji strzałkowych (arrow functions). Wynika to z natury tychże funkcji. Odwołanie się do `arguments` wewnątrz funkcji strzałkowej zaowocuje ReferenceError.

## Function.prototype.call\(\) i Function.prototype.apply\(\)

### Kilka faktów na temat funkcji w JavaScript

* W JavaScript funkcje są obiektami, mogą mieć one swoje własne funkcje, zwane metodami.
* Funkcja jest takim samym obiektem jak np. ciąg znaków. Posiada wbudowane metody i właściwości. Możemy także dodawać nowe funkcje i właściwości do pojedynczej funkcji jak i do każdej funkcji dzięki dziedziczeniu [prototypowemu](/prototypowanie-w-javascript.md).
* Funkcja może być także klasą znaną z innych obiektowych języków programowania a dokładnie może być konstruktorem klasy. Tak jak w innych językach do utworzenia nowego obiektu stosuje się słowo kluczowe `new`. Jeśli go nie zastosujemy, zmienną `this`, czyli tzw. **kontekstem **będzie obiekt globalny.
* Każda funkcja ma także dwa powiązane z nią elementy:
  **Kontekst **- czyli to, do czego odnosimy się za pomocą słowa kluczowego this
  **Argumenty **- lista argumentów przekazanych do funkcji w momencie jej wywołania
* To, z czego niektórzy mogą nie zdawać sobie sprawy, to fakt, iż w JavaScript każda funkcja posiada cały zestaw metod już wbudowanych \(prototypowych\), gotowych do użycia. Są to między innymi interesujące nas dzisiaj:
* [Function.prototype.apply\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
* [Function.prototype.call\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

**W JavaScript bardzo istotne jest gdzie funkcja jest wywoływana, a nie gdzie jest zdefiniowana, właśnie ze względu na kontekst.**

Metody `call()` i `apply()` wywołują funkcje z zadanym kontekstem oraz argumentami podanymi jako  tablica \( _apply_ \) lub kolejne parametry \( _call_ \).

```js
console.log("Solwit", "is", "the", "best");                 //Solwit is the best

console.log.call(this, "Solwit", "is", "the", "best");      //Solwit is the best
console.log.call(null, "Solwit", "is", "the", "best");      //Solwit is the best

console.log.apply(this, ["Solwit", "is", "the", "best"]);   //Solwit is the best
console.log.apply(null, ["Solwit", "is", "the", "best"]);   //Solwit is the best
```

[https://codepen.io/Bigismall/pen/dRXYBP](https://codepen.io/Bigismall/pen/dRXYBP)

### Praktyczne zastosowanie metod call i apply

#### Pożyczanie metod

Czasem zdarza się, że z istniejącego obiektu potrzeba jedynie jednej lub dwóch metod. Choć chcemy z nich skorzystać, nie chcemy tworzyć  związku przodek -  potomek pomiędzy obiektami \(dziedziczyć\). Zależy nam tylko na wybranych metodach, a nie na wszystkich znajdujących się  w oryginalnym obiekcie. Do skorzystania wykorzystamy oczywiście  _call i apply_.

W wywołaniu przekazujemy własny obiekt i wszystkie parametry Pożyczona metoda będzie zawierała w swoim _this_ referencję do naszego obiektu. Można powiedzieć, że na potrzeby wykonania zadania oszukujemy wołaną metodę, że _this_ to jej standardowy obiekt, choć w rzeczywistości jest inaczej. Przypomina to dziedziczenie, choć bez płacenia związanej z nim ceny \(w postaci dodatkowych parametrów i metod które nie są potrzebne\).

##### Pożyczenie metod [min](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min), [max](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max) od obiektu [Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

```js
var numbers = [5, 9, 6, 8, 2, 3, 7, 1, 4,],
    min,
    max;

min = Math.min(numbers);
max = Math.max(numbers);

console.log(min);                   //Nan
console.log(max);                   //Nan


min = Math.min.apply(null, numbers);
max = Math.max.apply(null, numbers);

console.log(min);                   //1
console.log(max);                   //9
```

[https://codepen.io/Bigismall/pen/MoeaMB](https://codepen.io/Bigismall/pen/MoeaMB)

##### Pożyczenie metody [slice ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)od obiektu [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

```js
function firstThree() {
    return Array.prototype.slice.call(arguments, 0, 3);
}

console.log(firstThree(1,2,3,4,5,6,7,8,9));
```

[https://codepen.io/Bigismall/pen/EXyVqM](https://codepen.io/Bigismall/pen/EXyVqM)

##### Konwersja kolekcji do tablicy

```js
var collection,
    collectionArray;

collection = document.querySelectorAll("p");
collectionArray = Array.prototype.slice.call(collection);

console.log(collection);
console.log(collectionArray);


try {
    collection.sort(function (a, b) {
        return a.innerText.length - b.innerText.length;
    });
    console.log(collection);

} catch (e) {
    console.warn(e.message);
}

collectionArray.sort(function (a, b) {
    return a.innerText.length - b.innerText.length;
});
console.log(collectionArray);
```

[https://codepen.io/Bigismall/pen/eRzJOQ](https://codepen.io/Bigismall/pen/eRzJOQ)

#### Pożyczanie i przypisanie

```js
var developer = {
        work: "copy-pasting, stack overflow reading",
        isDoing: function () {
            console.log("My everyday work is " + this.work);
        }
    },
    manager = {
        work: "Outlook programming"
    };

developer.isDoing();                //My everyday work is copy-pasting, stack overflow reading

try {
    manager.isDoing();
} catch (e) {
    console.warn(e.message);        //manager.isDoing is not a function
}

developer.isDoing.call(manager);    //My everyday work is Outlook programming
```

[https://codepen.io/Bigismall/pen/xrOZbo](https://codepen.io/Bigismall/pen/xrOZbo)

Mimo, iż obiekt manager nie posiada własnej funkcji `isDoing`, udało nam się z niej skorzystać. Dokonaliśmy tego "pożyczając" ją od obiektu developer poprzez metodę `call()`. Pozostało jedynie poinformować ją, z którego obiektu ma odczytać zmienne. Robimy to podając, jako jej pierwszy parametr, odpowiedni kontekst. W tym wypadku kontekstem jest obiekt, z którego zmienne chcemy odczytać, czyli _manager_.

Spróbujmy "pożyczyć" funkcję  z obiektu i wywołać ją wprost, bez przekazywania kontekstu.

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
    isDoingMethod = developer.isDoing;

developer.isDoing();            //My everyday work is copy-pasting, stack overflow reading
isDoingMethod();                //My everyday work is undefined
isDoingMethod.call(manager);    //My everyday work is Outlook programming
```

[https://codepen.io/Bigismall/pen/owLbjX](https://codepen.io/Bigismall/pen/owLbjX)

Wywołanie  `isDoingMethod`  bez podania kontekstu spowodowało uruchomienie jej w kontekście globalnym, w którym nie ma zmiennej _work _\(_this.work_\). Stąd `undefined`.

Istnieje jednak możliwość, że w obiekcie globalnym będzie istniała właściwość work,  wówczas funkcja wypisze wynik, ale prawdopodobnie z **zupełnie inną wartością od spodziewanej**.

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
    isDoingMethod = developer.isDoing,
    work = "I'm a global, i do not have to do anything";

developer.isDoing();            //My everyday work is copy-pasting, stack overflow reading
isDoingMethod();                //My everyday work is My everyday work is I'm a global, i do not have to do anything     (browser)
isDoingMethod.call(manager);    //My everyday work is Outlook programming
```

[https://codepen.io/Bigismall/pen/KqMVVe](https://codepen.io/Bigismall/pen/KqMVVe)

---

**Źródła:**

* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Function/apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Function/call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)



