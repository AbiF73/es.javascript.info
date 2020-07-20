importance: 5

---

# Decorador throttle

<<<<<<< HEAD
Crea un decorador "throttling" `throttle(f, ms)` -- que devuelve un contenedor.

Cuando se llama varias veces, pasa la llamada a `f` como máximo una vez por `ms` milisegundos.
=======
Create a "throttling" decorator `throttle(f, ms)` -- that returns a wrapper.

When it's called multiple times, it passes the call to `f` at maximum once per `ms` milliseconds.

The difference with debounce is that it's completely different decorator:
- `debounce` runs the function once after the "cooldown" period. Good for processing the final result.
- `throttle` runs it not more often than given `ms` time. Good for regular updates that shouldn't be very often.
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

La diferencia con *debounce* es que es un decorador completamente diferente:
- `debounce` ejecuta la función una vez después del período de `enfriamiento`. Es bueno para procesar el resultado final.
- `throttle` lo ejecuta no más de lo que se le da en el tiempo `ms`. Es bueno para actualizaciones regulares que no deberían ser muy frecuentes.

Revisemos una aplicación de la vida real para comprender mejor ese requisito y ver de dónde proviene.

<<<<<<< HEAD
**Por ejemplo, queremos rastrear los movimientos del mouse.**

En un navegador, podemos configurar una función para que se ejecute en cada movimiento del mouse y obtener la ubicación del puntero a medida que se mueve. Durante un uso activo del mouse, esta función generalmente se ejecuta con mucha frecuencia, puede ser algo así como 100 veces por segundo (cada 10 ms).
**Nos gustaría actualizar cierta información en la página web cuando se mueve el puntero.**

...Pero la función de actualización `update()` es demasiado pesada para hacerlo en cada micro-movimiento. Tampoco tiene sentido actualizar más de una vez cada 100 ms.

Entonces lo envolveremos en el decorador: use `throttle(update, 100)` como la función para ejecutar en cada movimiento del mouse en lugar del original `update()`. Se llamará al decorador con frecuencia, pero reenviará la llamada a `update()` como máximo una vez cada 100 ms.
=======
In a browser we can setup a function to run at every mouse movement and get the pointer location as it moves. During an active mouse usage, this function usually runs very frequently, can be something like 100 times per second (every 10 ms).
**We'd like to update some information on the web-page when the pointer moves.**

...But updating function `update()` is too heavy to do it on every micro-movement. There is also no sense in updating more often than once per 100ms.

So we'll wrap it into the decorator: use `throttle(update, 100)` as the function to run on each mouse move instead of the original `update()`. The decorator will be called often, but forward the call to `update()` at maximum once per 100ms.
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

Visualmente, se verá así:

<<<<<<< HEAD
1. Para el primer movimiento del mouse, el variante decorador pasa inmediatamente la llamada a `update`. Eso es importante, el usuario ve nuestra reacción a su movimiento de inmediato
2. Luego, a medida que el mouse avanza, hasta `100ms` no sucede nada. La variante decorador ignora las llamadas.
3. Al final de`100ms` -- ocurre un `update` más con las últimas coordenadas.
4. Entonces, finalmente, el mouse se detiene en alguna parte. La variante decorador espera hasta que expire `100ms` y luego ejecuta `update` con las últimas coordenadas. Entonces, y esto es bastante importante, se procesan las coordenadas finales del mouse.
=======
1. For the first mouse movement the decorated variant immediately passes the call to `update`. That's important, the user sees our reaction to their move immediately.
2. Then as the mouse moves on, until `100ms` nothing happens. The decorated variant ignores calls.
3. At the end of `100ms` -- one more `update` happens with the last coordinates.
4. Then, finally, the mouse stops somewhere. The decorated variant waits until `100ms` expire and then runs `update` with last coordinates. So, quite important, the final mouse coordinates are processed.
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

Un código de ejemplo:

```js
function f(a) {
  console.log(a);
}

// f1000 pasa llamadas a f como máximo una vez cada 1000 ms
let f1000 = throttle(f, 1000);

f1000(1); // muestra 1
f1000(2); // (throttling, 1000ms aún no)
f1000(3); // (throttling, 1000ms aún no)

// tiempo de espera de 1000 ms ...
// ...devuelve 3, el valor intermedio 2 fue ignorado
```

P.D Los argumentos y el contexto `this` pasado a `f1000` deben pasarse a la `f` original.
