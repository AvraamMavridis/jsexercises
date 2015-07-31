###EX 1

Description:

In order to stop too much communication from happening, your overlords declare that you are no longer allowed to use certain functionality in your code!

Disallowed functionality:

Strings
Numbers
Regular Expressions
Functions named "Hello", "World", "HelloWorld" or anything similar.
Object keys named "Hello", "World", "HelloWorld" or anything similar.
Without using the above, output the string "Hello World!" to prove that there is always a way.

My solution

```javascript
var p = (function () {
  var base = +(true);
  var ena = +(true);
  var dio = +(true) + (+(true));
  var tria = (+(true)) + (+(true)) + (+(true));
  var tessera = (+(true)) + (+(true)) + (+(true)) + (+(true));
  var pente = (+(true)) + (+(true)) + (+(true)) + (+(true)) + (+(true));
  base = ++base * ++base + (+(true)) + (+(true));
  base = base * base + (+(true)) + (+(true));
  var _ = base + (dio * tria);
  var __ = base + (tria);
  var ___ = base + (dio * pente);
  var ____ = ___ + tria;
  var _____ = ____ + tria;
  var ______ = _____ + pente;
  var _______ = base + dio;
  var H = String.fromCharCode(_);
  var E = String.fromCharCode(__);
  var L = String.fromCharCode(___);
  var O = String.fromCharCode(____);
  var W = String.fromCharCode(______);
  var R = String.fromCharCode(_____);
  var D = String.fromCharCode(_______);
  var space = String.fromCharCode(Math.floor(base/dio) - ena)
  var exclamationmark = String.fromCharCode(base/dio)
  return H + E.toLowerCase() + L.toLowerCase() + L.toLowerCase() + O.toLowerCase() + space + W + O.toLowerCase() + R.toLowerCase() + L.toLowerCase() + D.toLowerCase() + exclamationmark;
})

var helloWorld = p;

```
