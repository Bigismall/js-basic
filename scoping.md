# Scoping

## zasięg zmiennych

JavaScript so zarządzania zasięgiem zmiennych lokalnych wykorzystuje funkcje. Zmienna zdefiniowana wewnątrz funkcji jest zmienną  **lokalną**, czyli nie jest widoczna poza ciałem funkcji. Z drugiej strony zmienna **globalna** to taka, która została zadeklarowana poza funkcją lub jest używana bez jakiejkolwiek deklaracji.

### Czym właściwie jest obiekt globalny?

Każde środowisko JavaScript zapewnia **obiekt globalny** udostępniany w momencie użycia słowa kluczowego **this** poza funkcją. Każda zmienna globalna staje się właściwością obiektu globalnego. Obiekt globalny jest specyficzny dla środowiska uruchomieniowego.  Dla przeglądarki internetowej będzie to obiekt **window**  ale już dla Node.js  będzie to bieżący moduł.

#### Uzyskiwanie obiektu globalnego

```js
var global = (function () {
    return this;
}());

console.log(global);
```

Powyższa funkcja natychmiastowa, zwraca referencję do obiektu globalnego.  W zależności od środowiska uruchomienowego będzie to odpowiednio:

##### Przeglądarka internetowa

```js
Window {stop: function, open: function, alert: function, confirm: function, prompt: function…}
alert:function alert()
applicationCache:ApplicationCache
atob:function atob()
blur:function ()
btoa:function btoa()
caches:CacheStorage
cancelAnimationFrame:function cancelAnimationFrame()
cancelIdleCallback:function cancelIdleCallback()
captureEvents:function captureEvents()
chrome:Object
clearInterval:function clearInterval()
clearTimeout:function clearTimeout()
clientInformation:Navigator
close:function ()
closed:false
confirm:function confirm()
console:Object
createImageBitmap:function createImageBitmap()
crypto:Crypto
customElements:CustomElementRegistry
defaultStatus:""
defaultstatus:""
devicePixelRatio:1
document:document
external:External
...
```

##### Node.js

```js
{ DTRACE_NET_SERVER_CONNECTION: [Function],
  DTRACE_NET_STREAM_END: [Function],
  DTRACE_HTTP_SERVER_REQUEST: [Function],
  DTRACE_HTTP_SERVER_RESPONSE: [Function],
  DTRACE_HTTP_CLIENT_REQUEST: [Function],
  DTRACE_HTTP_CLIENT_RESPONSE: [Function],
  COUNTER_NET_SERVER_CONNECTION: [Function],
  COUNTER_NET_SERVER_CONNECTION_CLOSE: [Function],
  COUNTER_HTTP_SERVER_REQUEST: [Function],
  COUNTER_HTTP_SERVER_RESPONSE: [Function],
  COUNTER_HTTP_CLIENT_REQUEST: [Function],
  COUNTER_HTTP_CLIENT_RESPONSE: [Function],
  global: [Circular],
  process:
   process {
     title: '  - node  scoping.js',
     version: 'v6.9.4',
     moduleLoadList:
      [ 'Binding contextify',
        'Binding natives',
        'NativeModule events',
        'NativeModule util',
        'Binding uv',
...
```

#### Dlaczego nie należy używać zmiennych globalnych?

Zmienne globalne są problemem, ponieważ są współdzielone przez cały kod aplikacji JavaScript lub strony WWW. Znajdują się w tej samej globalnej przestrzeni nazw, więc zawsze istnieje ryzyko kolizji nazw, czyli sytuacji gdy dwie różne części aplikacji mają zdefiniowane zmienne globalne o tej samej nazwie, ale o różnym przeznaczeniu \(np. _result_, _i_, _index_, _db, a, foo_\)

Nie bez przyczyny w jQuery  wykorzystano $ dla nazwy głównego modułu. Nie bez przyczyny też  metody [DOM ](https://developer.mozilla.org/pl/docs/DOM)mają tak rozwlekłe nazwy jak np. `getElementById()`.

### Definiowanie zmiennych globalnych

Przypadkowe utworzenie zmiennej globalnej jest wyjątkowo łatwe dzięki dwóm cechom języka JavaScript. 

1. Można w nim używać zmiennych bez ich deklarowania.
2. Istnieją tak zwane dorozumiane zmienne globalne. Polega to na tym, że dowolna zmienna, która nie zostanie jawnie zadeklarowana, staje się właściwością obiektu globalnego, i jest dostępna w podobny sposób jak zmienna globalna.

```js
myGlobal = "SolwIT";                //brak var (tu akurat nic nie zmienia)

console.log(myGlobal);              //SolwIT
console.log(window.myGlobal);       //SolwIT
console.log(window["myGlobal"]);    //SolwIT
console.log(this.myGlobal);         //SolwIT
```

```js
function sum(a, b) {
    result = a + b;                    //brak var (tutaj ma znaczenie)
    return result;
}

console.log(sum(2, 3));		//5
console.log(result);			//5
```

```js
function sum(a, b) {
    var result = a + b;        // dzięki var, result jest zmienną lokalną 
    return result;
}

console.log(sum(2, 3));         //5
console.log(result);            //Uncaught ReferenceError: result is not defined
```

### Definiowanie zmiennych lokalnych

Jak już wcześniej wspomnieliśmy zmienne w JS mają zasięg funkcyjny.  

**Składnia**_** EcmaScript 2015 **_**\(**_**ES6**_**\) pozwala na definiowanie zmiennych o zasięgu blokowym za pomocą  operatora **_**let**_**.**





