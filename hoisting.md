# Hoisting

## Przenoszenie deklaracji zmiennych i funkcji

Przenoszenie  jest mechanizmem JavaScript, w którym deklaracje zmiennych i  funkcji są przenoszone na górę ich zakresu przed wykonaniem kodu. Działanie to może prowadzić do błędów logicznych polegających na tym, ze korzysta się ze zmiennej, a następnie  się  ją deklaruje.  W języku JavaScript, jeśli zmienna znajduje się w tym samym zasięgu zmiennych \(w tej samej funkcji\), jest uważana za zadeklarowaną, nawet gdy zostanie użyta przed pojawieniem się  deklaracji z instrukcją `var`.

### Przenoszenie deklaracji zmiennych

```js
companyName = "Intel";
function showCompanyName() {
    console.log(companyName);
    var companyName = "SolwIT";
    console.log(companyName);
}

showCompanyName();
```

Co tak naprawdę się wydarzyło?  Dlaczego najpierw w wyniku mamy `undefined`a potem `SolwIT`?

```
Jak JavaScript widzi powyższe?
```

```js
companyName = "Intel";
function showCompanyName() {
    var companyName;            //undefined
    console.log(companyName);
    companyName = "SolwIT";     //SolwIT
    console.log(companyName);
}

showCompanyName();
```

### Przenoszenie deklaracji funkcji

W JavaScript funkcje możemy definiować na wiele sposobów. W ogólności mamy do czynienia z

* deklaracjami funkcji
* wyrażeniami funkcyjnymi

Z przenoszeniem deklaracji nie ma problemu i jest to w zasadzie zaleta języka, bo możemy wywołać funkcję przed wystąpieniem jej deklaracji.

```js
showCompanyName();      //SolwIT

function showCompanyName() {
    var companyName = "SolwIT";
    console.log(companyName);
}
```

Jak JavaScript widzi powyższe?

```js
function showCompanyName() {
    var companyName = "SolwIT";
    console.log(companyName);
}

showCompanyName();      //SolwIT
```

Wyrażenia funkcyjne zaś obowiązuje taka sama zasada jak zmienne.

```
showCompanyName();      //Uncaught TypeError: showCompanyName is not a function

var showCompanyName = function () {
    var companyName = "SolwIT";
    console.log(companyName);
}
```

Jak JavaScript widzi powyższe?

```
var showCompanyName;        //undefined
showCompanyName();            //Uncaught TypeError: showCompanyName is not a function

showCompanyName = function () {
    var companyName = "SolwIT";
    console.log(companyName);
}
```

## Wzorzec pojedynczego var

Lekarstwem na ewentualne problemy z przenoszeniem jest wzorzec pojedynczego var. W ogólności polega to na deklaracji wszystkich zmiennych w funkcji za pomocą pojedynczego wyrażenia `var`, umieszczonego na początku funkcji. Takie działanie niejako wyprzedza działanie interpretatora języka JavaScript.

```js
function singleVar() {
    var a = 1,
        b = 2,
        sum = a + b,
        myObject = {},
        zero;    
}
```

### Stosowanie wzorca pojedynczego var

* Zapewnia jedno miejsce do poszukiwania wszystkich zmiennych lokalnych wymaganych przez funkcję.
* Zapobiega błędom logicznym polegającym na tym, że chce się skorzystać ze zmiennej przed jej zdefiniowaniem.
* Pomaga pamiętać o deklarowaniu zmiennych, więc minimalizuje ryzyko utworzenia zmiennych globalnych.



