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

Implementacja funkcji` join()`

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



## Function.prototype.call\(\)

## Function.prototype.apply\(\)



