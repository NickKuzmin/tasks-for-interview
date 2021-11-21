- Console API methods (assert, count, dir, group, time, trace):
https://developer.mozilla.org/en-US/docs/Web/API/Console

*Difference of using async / await vs promises:*
- https://habr.com/ru/company/ruvds/blog/326074/

*Node.js. Event Loop:*
- https://habr.com/ru/post/479062/

- Async library: https://caolan.github.io/async/v3/
- Debounce/Throttling https://css-tricks.com/debouncing-throttling-explained-examples/

---------------------------
**Библиотеки:**
- Stampit: https://github.com/stampit-org/stampit
---------------------------
- Call Stack, Web APIs, Render Queue, Callback Queue
- 16.000 methods - callstack overvflow
---------------------------
```
function Vehicle(maxSpeed) {
    this.maxSpeed = maxSpeed;
}

Vehicle.prototype.maxSpeed = function() {
    return this.maxSpeed;
}

function Car(maxSpeed) {
    Vehicle.call(this, maxSpeed);
}

Car.prototype = new Vehicle();
```
---------------------------
```
Object.seal
Object.freeze
Object.createProperty
```
---------------------------
