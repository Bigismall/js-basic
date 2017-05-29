# Hoisting

## Przenoszenie deklaracji zmiennych i funkcji

Przenoszenie  jest mechanizmem JavaScript, w którym deklaracje zmiennych i  funkcji są przenoszone na górę ich zakresu przed wykonaniem kodu. Działanie to może prowadzić do błędów logicznych polegających na tym, ze korzysta się ze zmiennej, a następnie  się  ją deklaruje.  W języku JavaScript, jeśli zmienna znajduje się w tym samym zasięgu zmiennych \(w tej samej funkcji\), jest uważana za zadeklarowaną, nawet gdy zostanie użyta przed pojawieniem się  deklaracji z instrukcją `var`.

```js
companyName = "Intel";
function showCompanyName() {
    console.log(companyName);
    var companyName = "SolwIT";
    console.log(companyName);
}

showCompanyName();
```

Co tak naprawdę się wydażyło?  Dlaczego najpierw w wyniku mamy `undefined `a potem `SolwIT`? 

Jak JavaScript widzi powyższe?

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



//TODO hoisting funkcji

//TODO pojedynczy var 

