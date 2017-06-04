# Event Loop, czyli jak działa setTimeout\(..., 0\)

Pętla zdarzeń, jak sama nazwa wskazuje, to okresowo wywoływany kod sprawdzający czy w chwili wywołania są jakieś zdarzenia do obsłużenia.  Przypomina to trochę  główną pętlę gry komputerowej, w której:

* sprawdzamy czy nie naciśnięto klawisza akcji
* obliczamy pozycję graczy
* rysujemy planszę

Podobnie jak w grze, JavaScript na bieżąco sprawdza, czy ma coś do zrobienia \(obsługa naciśniętego klawisza, przewijanie, strony, wykonanie cyklicznej instrukcji,  funkcji z kolejki\)

W ogólności schemat działania silnika JS można przedstawić jak poniżej:

![](/assets/event_loop.svg)













**Źródła:**

[https://johnresig.com/blog/how-javascript-timers-work/](https://johnresig.com/blog/how-javascript-timers-work/)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

[https://developer.mozilla.org/pl/docs/Web/API/Window/setTimeout](https://developer.mozilla.org/pl/docs/Web/API/Window/setTimeout)

[http://altitudelabs.com/blog/what-is-the-javascript-event-loop/](http://altitudelabs.com/blog/what-is-the-javascript-event-loop/)

[https://developer.mozilla.org/en-US/Add-ons/Code\_snippets/Timers](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Timers)

[http://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/](http://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/)

[http://webroad.pl/javascript/746-synchroniczna-asynchronicznosc](http://webroad.pl/javascript/746-synchroniczna-asynchronicznosc)

[https://stackoverflow.com/questions/33955650/what-is-settimeout-doing-when-set-to-0-milliseconds/33955673](https://stackoverflow.com/questions/33955650/what-is-settimeout-doing-when-set-to-0-milliseconds/33955673)

