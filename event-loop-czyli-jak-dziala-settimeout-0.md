# Event Loop, czyli jak działa setTimeout\(..., 0\)

## Event loop

Pętla zdarzeń, jak sama nazwa wskazuje, to okresowo wywoływany kod sprawdzający czy w chwili wywołania są jakieś zdarzenia do obsłużenia.  Przypomina to trochę  główną pętlę gry komputerowej, w której:

* sprawdzamy czy nie naciśnięto klawisza akcji
* obliczamy pozycję graczy
* rysujemy planszę

Podobnie jak w grze, JavaScript na bieżąco sprawdza, czy ma coś do zrobienia \(obsługa naciśniętego klawisza, przewijanie, strony, wykonanie cyklicznej instrukcji,  funkcji z kolejki\).

```
while (queue.waitForMessage()) {
  queue.processNextMessage();
}
```

JavaScript jest jednowątkowy, co oznacza, obsługa zdarzeń asynchronicznych tak naprawdę oznacza wstawienie ich na koniec kolejki i obsługę dopiero wówczas gdy będzie na to wolny zasób czasowy. Asynchroniczność jest zatem jedynie symulacją.

## setTimeOut\(\)

Do wykonania funkcji w sposób "asynchroniczny"  możemy wykorzystać [Timery](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Timers), w szczególności  funkcję`setTimeOut()`.

Funkcja `setTimeOut()` pozwala na wykonanie przekazanej funkcji opóźnione o przekazaną wartość.

```js
console.log("SolwIT");
setTimeout(function () {
    console.log("Intel");
}, 1000);
```

Powyższy kod, najpierw wypisze "SolwIT"  a sekundę  później "Intel". ~~Jest to zrozumiałe działanie, bo przecież siedzimy w SolwIT a Intel jest dużo dalej.~~

To, że "Intel" wyświetli się po sekundzie, jest jedynie naszym pobożnym życzeniem. Jeżeli kolejka zadań do realizacji będzie długa, a dodatkowo któryś z jej elementów przywiesi wątek JS, wówczas może się okazać, że napis "Intel" pojawi się nieco później.

Takie przywieszanie się  JavaScript dosyć łatwo zrealizować, przypinając kosztowną czasowo funkcję do często zachodzącego zdarzenia np `mouseMove`.

### Zero milisekund na wywołanie

Skoro wiemy już, że możemy symulować asynchroniczność, to chcielibyśmy realizować to natychmiast, pomijając jakiekolwiek opóźnienie. Ustawiamy zatem 0ms, w nadziei, że przekazana funkcja uruchomi się  "od razu".  Nawet jednak ustawienie 0ms nie zmienia sposobu działania JavaScript.  Nie jest bowiem tak, że JS porzuci wszystkie inne zadania i zajmie się  naszym. Obowiązują reguły ustawiania się w kolejce.  Nie uruchomi tez naszego zadania w osobnym wątku, bo nie potrafi.

#### Zero milisekund - przykład

```js
(function () {

    console.log('this is the start');

    setTimeout(function callBackOne() {
        console.log('this is a msg from call back one');
    });

    console.log('this is just a message');

    setTimeout(function callBackTwo() {
        console.log('this is a msg from call back two');
    }, 0);

    console.log('this is the end');
})();
```

wynik:

```
this is the start
this is just a message
this is the end
this is a msg from call back one
this is a msg from call back two
```

Jak widać mimo iż  `callBackOne()`  i `callBackTwo()` zostały wywołane z parametrem 0ms \(lub jego brakiem\), ich wykonanie zostało odłożone na koniec kolejki \(przy czym zachowana została kolejność, wynikająca z 0ms\)





**Źródła:**

[https://johnresig.com/blog/how-javascript-timers-work/](https://johnresig.com/blog/how-javascript-timers-work/)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

[https://developer.mozilla.org/pl/docs/Web/API/Window/setTimeout](https://developer.mozilla.org/pl/docs/Web/API/Window/setTimeout)

[http://altitudelabs.com/blog/what-is-the-javascript-event-loop/](http://altitudelabs.com/blog/what-is-the-javascript-event-loop/)

[https://developer.mozilla.org/en-US/Add-ons/Code\_snippets/Timers](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Timers)

[http://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/](http://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/)

[http://webroad.pl/javascript/746-synchroniczna-asynchronicznosc](http://webroad.pl/javascript/746-synchroniczna-asynchronicznosc)

[https://stackoverflow.com/questions/33955650/what-is-settimeout-doing-when-set-to-0-milliseconds/33955673](https://stackoverflow.com/questions/33955650/what-is-settimeout-doing-when-set-to-0-milliseconds/33955673)

