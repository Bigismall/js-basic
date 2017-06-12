# JavaScript gotchas!

## TimeOut Sort

```js
var numbers = [38, 43, 33, 43, 27, 20, 33, 17, 49, 11, 30, 27, 35, 42, 14, 32, 44, 44, 16, 44];

numbers.forEach(function (number) {
    (function (number) {
        setTimeout(function () {
            console.log(number)
        }, number);
    }(number));
});
```

[https://codepen.io/Bigismall/pen/QgEyoY](https://codepen.io/Bigismall/pen/QgEyoY)

## Automatic type conversion

```js
console.log([1,5,20,10].sort()) //[ 1, 10, 20, 5 ]
```

[https://codepen.io/Bigismall/pen/gRMPye](https://codepen.io/Bigismall/pen/gRMPye)

## Are the numbers equal?

```js
var a = 0.1,
    b = 0.2,
    c = 0.3;

console.log((a + b) === c);    //false
```

```js
var a = 0 * 1,
    b = 0 * -1;

console.log(a, b);      //0 -0
console.log(a === b);   //true
console.log(1/a === 1/b);   //false
```

[https://codepen.io/Bigismall/pen/XgKXwb](https://codepen.io/Bigismall/pen/XgKXwb)

## To string evaluation

```js
var a = 1,
    b = "2",
    c = a + b,
    d = b + a,
    e = (b + b) * 1,
    f = a + a;

console.log(c, typeof c);   // 12 string
console.log(d, typeof d);   // 21 string
console.log(e, typeof e);   // 22 number
console.log(f, typeof f);   // 2 number
```

[https://codepen.io/Bigismall/pen/OgXMYE](https://codepen.io/Bigismall/pen/OgXMYE)

## Type of  trap

```js
typeof {} === "object" //true
typeof "" === "string" //true
typeof [] === "array"; //false
```

[https://codepen.io/Bigismall/pen/gRMPNz](https://codepen.io/Bigismall/pen/gRMPNz)

## Math min and max values

```js
console.log(Math.max()); // -Infinity
console.log(Math.min()); // Infinity
```

[https://codepen.io/Bigismall/pen/dRXGxR](https://codepen.io/Bigismall/pen/dRXGxR)

## Also

* [http://www.jazcash.com/a-javascript-journey-with-only-six-characters/](http://www.jazcash.com/a-javascript-journey-with-only-six-characters/)
* [http://js1k.com](http://js1k.com)
* [https://www.chromeexperiments.com/demoscene](https://www.chromeexperiments.com/demoscene)
* [https://aframe.io/](https://aframe.io/)
* [http://phaser.io/examples](http://phaser.io/examples)
* [https://www.nativescript.org/](https://www.nativescript.org/)
* [http://piqnt.com/planck.js/](http://piqnt.com/planck.js/)
* [http://www.geo-fs.com/](http://www.geo-fs.com/)
* [http://voxeljs.com/](http://voxeljs.com/)
* [https://www.codingame.com/start](https://www.codingame.com/start)
* [http://codeincomplete.com/games/](http://codeincomplete.com/games/)
* [https://threejs.org/](https://threejs.org/)



