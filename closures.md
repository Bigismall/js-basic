# Closures - domknięcia

## Definicje

> **Domknięcie**– w metodach realizacji [języków programowania](https://pl.wikipedia.org/wiki/Język_programowania) jest to obiekt wiążący [funkcję](https://pl.wikipedia.org/wiki/Funkcja) lub referencję do funkcji oraz środowisko mające wpływ na tę funkcję w momencie jej definiowania. Środowisko przechowuje wszystkie nielokalne obiekty wykorzystywane przez funkcję. Realizacja domknięcia jest zdeterminowana przez język, jak również przez [kompilator](https://pl.wikipedia.org/wiki/Kompilator).
>
> Domknięcia występują głównie w [językach funkcyjnych](https://pl.wikipedia.org/wiki/Język_funkcyjny), w których funkcje mogą zwracać inne funkcje \(tzw.[funkcje wyższego rzędu](https://pl.wikipedia.org/wiki/Funkcja_wyższego_rzędu)\), wykorzystujące zmienne utworzone lokalnie.
>
> Mówiąc najprościej, domknięcie w językach programowania jest to obiekt wiążący funkcję i środowisko, w którym funkcja pracuje. Środowisko to przechowuje wszystkie obiekty używane przez funkcję i co ważne są one **niedostępne **w globalnym zakresie widoczności.
>
> Domknięcie to zasięg \(obszar\) stworzony przez funkcję, który odgradza zgromadzone w nim zmienne i funkcje od reszty kodu tworząc dla nich osobne "środowisko"
>
> Domknięcia leksykalne \(ang. closures\) są to funkcje, wewnątrz których mamy dostęp do zmiennych, które zostały zadeklarowane na zewnątrz funkcji mimo że zakres ich istnienia się już zakończył. Istnieją one w środowisku, które jest **“doczepione” **do funkcji.
>
> Domknięcia to funkcje których funkcje wewnętrzne odwołują się do niezależnych \(wolnych\) zmiennych. Innymi słowy, funkcje zdeklarowane wewnątrz domknięcia 'pamiętają' środowisko w którym zostały utworzone.
>
> Domknięcie jest wtedy, gdy postawimy płot wokół pastwiska zamykając wewnątrz wszystkie owce, wilki i ogniste smoki, aby nie pomieszały się ze stworkami z innych pastwisk.

## Przykłady

```js
var sentence = "outside of a closure";

function basicClosure() {
    var sentence = "inside a closure";
}

console.log(sentence);      //outside of a closure
basicClosure();
console.log(sentence);      //outside of a closure
```

Tak więc zdefiniowaliśmy zmienną _sentence_ i ustaliliśmy jej wartość na "outside of a closure". Następnie wywołaliśmy funkcję, która zmienia wartość zmiennej _sentence_ na "inside closure", tak?

Nie :\) Zmienna a na zewnątrz funkcji `basicClosure()` to zupełnie inna zmienna niż zmienna a wewnątrz funkcji `basicClosure()`. Funkcja ta służy nam tutaj właśnie jako domknięcie, tworząc osobne "środowisko" dla wszystkich zmiennych w niej zawartych.

Gdybyśmy nie użyli `var` wewnątrz funkcji, efekt byłby odmienny.

```js
var sentence = "outside of a closure";

function basicClosure() {
    sentence = "inside a closure";
}

console.log(sentence);      //outside of a closure
basicClosure();
console.log(sentence);      //inside a closure
```

### Zmienne prywatne

JavaScript nie oferuje obsługi zmiennych prywatnych, ale jak widać na przykładzie powyżej, zmienne "domknięte" w funkcji nie mogą być modyfikowane z zewnątrz tej funkcji, są więc nijako prywatne.

```js
function displayName() {
    var name = "Solwit";
    return function () {
        console.log(name);
    }
}

var letDisplayName = displayName();
letDisplayName();
```

Jak pamiętamy, funkcje mogą zwracać funkcje. W przykładzie powyżej funkcja `displayName()` zwraca funkcję  \(anonimową\) która to wyświetla wartość zmiennej _name_.

**Co istotne**

* zwrócona funkcja anonimowa mimo iż przypisana do zmiennej _letDisplayName_ nadal ma dostęp do zmiennej _name_ spoza swojego ciała.
* funkcja anonimowa jest zwracana przez funkcję `displayName()` , ale nie następuje jej wykonanie

Mamy zatem prywatność, co możemy z tym zrobić?

```js
function counter(initialValue) {
    var privateCounter = initialValue;
    return {
        increment: function () {
            privateCounter++;
        },

        get: function () {
            return privateCounter;
        }
    }
}

var licznik = counter(150);
console.log(licznik.get());     //150
licznik.increment();
console.log(licznik.get());     //151
licznik.increment();
licznik.increment();
licznik.increment();
console.log(licznik.get());     //154
```

Funkcja `counter()` zwraca tym razem obiekt posiadający 2 metody  `increment()` oraz `get()`. Pozwalają one na manipulacje prywatną zmienną  _privateCounter_.

Co ciekawe, w powyższej funkcji `counter()` zmienna _privateCounter_ zakończyła swój żywot \(po wywołaniu `counter(150)`\) , ale jej referencja jest zamknięta wewnątrz środowiska, do którego ma dostęp funkcja anonimowa, która została zwrócona przez funkcję counter.

### Domknięcia wewnątrz pętli

Przypomnijmy, że w JavaScript zasięg jest określany przez ciało funkcji.  Częstym błędem jest założenie, że zmienne utworzone w pętli istnieją jedynie w tej pętli.  Pętla nie tworzy osobnego zasięgu!  Rozważmy przykład:

```js
for (var i = 0; i < 5; i++) {
    setTimeout(function () {
        console.log("SolwIT!", i);
    }, 500);
}
```

Prawdopodobną  intencją  było aby wyświetlić napisy "SolwIT 0", "SolwIT 1", "SolwIT 2", "SolwIT 3", "SolwIT 4" z  pół sekundowym opóźnieniem.   Stało się jednak inaczej.  Po pół sekundzie wyświetliło się:

```
SolwIT! 5
SolwIT! 5
SolwIT! 5
SolwIT! 5
SolwIT! 5
```

Stało się tak dlatego, że zmienna `i` z poza kontekstu naszej funkcji  po  500ms miała już wartość przypisaną w 5 iteracji, czyli 5!  Nasza funkcja zaś korzysta ze zmiennej `i`  spoza swojego zasięgu która to została zmodyfikowana przez działanie pętli.

> Mała dygresja na temat sposobu działania funkcji setTimeout: Pamiętaj, że funkcja setTimeout nie zatrzymuje wywoływania całego kodu na wskazany czas, a jedynie instrukcji w niej zawartych, dlatego liczby nie będą wypisywane co pół sekundy po jednej, ale po pół sekundy od razu jedna za drugą. Dla zobrazowania: Załóżmy, że jedno przejście pętli for zajmuje komputerowi 1 ms. W pierwszym przejściu widzi funkcję setTimeout i ustawia jej wykonanie za 500 ms, czyli w 501-szej milisekundzie. W drugiej milisekundzie wchodzi do pętli drugi raz, znowu napotyka setTimeout i ustawia jego wykonanie za 500 ms, czyli w 502-giej milisekundzie działania programu itd... A po przejściu całej pętli, czyli po pięciu milisekundach, wartość zmiennej i będzie już wynosiła 5 i w takim stanie poczeka na wywołania odłożone w czasie. Oczywiście jest to duże uproszczenie i nie do końca tak to działa, jednak na potrzeby zrozumienia tematu domknięć, powinno wystarczyć.

Jak już wiemy, aby prawidłowo rozwiązać to zadanie przydała by się zmienna prywatna \(analogiczna do _privateCounter_ z  poprzedniego przykładu\). Aby takową zdefiniować, musimy użyć funkcji.  Co więcej, aby nasz kod się automatycznie wykonał, musimy użyć  [funkcji natychmiastowej](/immediately-invoked-function-expression-iife.md).

```js
for (var i = 0; i < 5; i++) {
    (function (privateValue) {
        setTimeout(function () {
            console.log("SolwIT!", privateValue);
        }, 500);
    }(i));
}
```

### Zadanie

Przygotuj stronę HTML z 5 przyciskami. Każdemu z nich przypisz etykietę  od 0 do 4.  Przygotuj kod, który każdemu z przycisków przypisze funkcję wywołaną po kliknięciu w niego.  Funkcja powinna wyświetlić numer przycisku.



**Źródła:**

* [http://jcubic.pl/2014/08/funkcje-w-javascript.html](http://jcubic.pl/2014/08/funkcje-w-javascript.html)
* [http://blog.nebula.us/13-javascript-closures-czyli-zrozumiec-i-wykorzystac-domkniecia](http://blog.nebula.us/13-javascript-closures-czyli-zrozumiec-i-wykorzystac-domkniecia)
* [http://bonsaiden.github.io/JavaScript-Garden/pl/\#function.closures](http://bonsaiden.github.io/JavaScript-Garden/pl/#function.closures)
* [https://pl.wikipedia.org/wiki/Domknięcie\_\(programowanie\)](https://pl.wikipedia.org/wiki/Domknięcie_%28programowanie%29)
* [https://developer.mozilla.org/pl/docs/Web/JavaScript/Domkniecia](https://developer.mozilla.org/pl/docs/Web/JavaScript/Domkniecia)



