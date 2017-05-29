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



