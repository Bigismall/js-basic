# JavaScript gotchas!



TimeOut Sort

```
var numbers = [38, 43, 33, 43, 27, 20, 33, 17, 49, 11, 30, 27, 35, 42, 14, 32, 44, 44, 16, 44];

numbers.forEach(function (number) {
    (function (number) {
        setTimeout(function () {
            console.log(number)
        }, number);
    }(number));

});
```



timeout sort

[http://www.jazcash.com/a-javascript-journey-with-only-six-characters/](http://www.jazcash.com/a-javascript-journey-with-only-six-characters/)

