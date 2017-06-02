# Closures - domknięcia

## Definicje

> **Domknięcie**– w metodach realizacji [języków programowania](https://pl.wikipedia.org/wiki/J%C4%99zyk_programowania) jest to obiekt wiążący [funkcję](https://pl.wikipedia.org/wiki/Funkcja) lub referencję do funkcji oraz środowisko mające wpływ na tę funkcję w momencie jej definiowania. Środowisko przechowuje wszystkie nielokalne obiekty wykorzystywane przez funkcję. Realizacja domknięcia jest zdeterminowana przez język, jak również przez [kompilator](https://pl.wikipedia.org/wiki/Kompilator).
>
> Domknięcia występują głównie w [językach funkcyjnych](https://pl.wikipedia.org/wiki/J%C4%99zyk_funkcyjny), w których funkcje mogą zwracać inne funkcje \(tzw.[funkcje wyższego rzędu](https://pl.wikipedia.org/wiki/Funkcja_wy%C5%BCszego_rz%C4%99du)\), wykorzystujące zmienne utworzone lokalnie.



> Mówiąc najprościej, domknięcie w językach programowania jest to obiekt wiążący funkcję i środowisko, w którym funkcja pracuje. Środowisko to przechowuje wszystkie obiekty używane przez funkcję i co ważne są one **niedostępne **w globalnym zakresie widoczności.



> Domknięcie to zasięg \(obszar\) stworzony przez funkcję, który odgradza zgromadzone w nim zmienne i funkcje od reszty kodu tworząc dla nich osobne "środowisko"



> Domknięcia leksykalne \(ang. closures\) są to funkcje, wewnątrz których mamy dostęp do zmiennych, które zostały zadeklarowane na zewnątrz funkcji mimo że zakres ich istnienia się już zakończył. Istnieją one w środowisku, które jest **“doczepione” **do funkcji.



> Domknięcia to funkcje których funkcje wewnętrzne odwołują się do niezależnych \(wolnych\) zmiennych. Innymi słowy, funkcje zdeklarowane wewnątrz domknięcia 'pamiętają' środowisko w którym zostały utworzone.



> Domknięcie jest wtedy, gdy postawimy płot wokół pastwiska zamykając wewnątrz wszystkie owce, wilki i ogniste smoki, aby nie pomieszały się ze stworkami z innych pastwisk.

## Przykłady

```
var sentence = "outside of a closure";

function basicClosure() {
    var sentence = "inside a closure";
}

console.log(sentence);      //outside of a closure
basicClosure();
console.log(sentence);      //outside of a closure
```

Tak więc zdefiniowaliśmy zmienną _sentence _i ustaliliśmy jej wartość na "outside of a closure". Następnie wywołaliśmy funkcję, która zmienia wartość zmiennej _sentence _na "inside closure", tak? Nie :\) Zmienna a na zewnątrz funkcji `basicClosure()` to zupełnie inna zmienna niż zmienna a wewnątrz funkcji `basicClosure()`. Funkcja ta służy nam tutaj właśnie jako domknięcie, tworząc osobne "środowisko" dla wszystkich zmiennych w niej zawartych.

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



counter

przykład z clickami w button  lub settimeout









http://jcubic.pl/2014/08/funkcje-w-javascript.html

http://blog.nebula.us/13-javascript-closures-czyli-zrozumiec-i-wykorzystac-domkniecia

http://bonsaiden.github.io/JavaScript-Garden/pl/\#function.closures

https://pl.wikipedia.org/wiki/Domkni%C4%99cie\_\(programowanie\)

https://developer.mozilla.org/pl/docs/Web/JavaScript/Domkniecia

https://developer.mozilla.org/pl/docs/Web/JavaScript/Domkniecia









