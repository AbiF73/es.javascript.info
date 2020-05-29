
# Módulos, introducción

<<<<<<< HEAD
A medida que nuestra aplicación crece, queremos dividirla en múltiples archivos, llamados "módulos". Un módulo generalmente contiene una clase o una biblioteca de funciones.

Durante mucho tiempo, JavaScript existió sin una sintaxis de módulo a nivel de lenguaje. Eso no fue un problema, porque inicialmente los scripts eran pequeños y simples, por lo que no era necesario.

Pero con el tiempo los scripts se volvieron cada vez más complejos, por lo que la comunidad inventó una variedad de formas de organizar el código en módulos, bibliotecas especiales para cargar módulos a pedido.
=======
As our application grows bigger, we want to split it into multiple files, so called "modules". A module usually contains a class or a library of functions.

For a long time, JavaScript existed without a language-level module syntax. That wasn't a problem, because initially scripts were small and simple, so there was no need.

But eventually scripts became more and more complex, so the community invented a variety of ways to organize code into modules, special libraries to load modules on demand.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Por ejemplo:

<<<<<<< HEAD
- [AMD](https://es.wikipedia.org/wiki/Asynchronous_module_definition) -- uno de los sistemas de módulos más antiguos, implementado inicialmente por la biblioteca [require.js](http://requirejs.org/).
- [CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1) -- el sistema de módulos creado para el servidor Node.js.
- [UMD](https://github.com/umdjs/umd) -- un sistema de módulos más, sugerido como universal, compatible con AMD y CommonJS.

Ahora, todo esto se convierte lentamente en una parte de la historia, pero aún podemos encontrarlos en viejos scripts.
=======
- [AMD](https://en.wikipedia.org/wiki/Asynchronous_module_definition) -- one of the most ancient module systems, initially implemented by the library [require.js](http://requirejs.org/).
- [CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1) -- the module system created for Node.js server.
- [UMD](https://github.com/umdjs/umd) -- one more module system, suggested as a universal one, compatible with AMD and CommonJS.

Now all these slowly become a part of history, but we still can find them in old scripts.

The language-level module system appeared in the standard in 2015, gradually evolved since then, and is now supported by all major browsers and in Node.js. So we'll study it from now on.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

El sistema de módulos a nivel de idioma apareció en el estándar en 2015, evolucionó gradualmente desde entonces y ahora es compatible con todos los principales navegadores y en Node.js. Así que lo estudiaremos de ahora en adelante.

<<<<<<< HEAD
## Qué es un módulo?

Un módulo es solo un archivo. Un script es un módulo.

Los módulos pueden cargarse entre sí y usar directivas especiales `export` e `import` para intercambiar funcionalidad, llamar a funciones de un módulo de otro:
=======
A module is just a file. One script is one module.

Modules can load each other and use special directives `export` and `import` to interchange functionality, call functions of one module from another one:

- `export` keyword labels variables and functions that should be accessible from outside the current module.
- `import` allows the import of functionality from other modules.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

- La palabra clave `export` etiqueta las variables y funciones que deberían ser accesibles desde fuera del módulo actual.
- `import` permite importar funcionalidades desde otros módulos.

Por ejemplo, si tenemos un archivo `sayHi.js` que exporta una función:

```js
// 📁 sayHi.js
export function sayHi(user) {
  alert(`Hello, ${user}!`);
}
```

...Luego, otro archivo puede importarlo y usarlo:

```js
// 📁 main.js
import {sayHi} desde'./sayHi.js';

alert(sayHi); // function...
sayHi('John'); // Hello, John!
```

<<<<<<< HEAD
La directiva `import` carga el módulo por la ruta `./sayHi.js` relativo con el archivo actual, y asigna la función exportada `sayHi` a la variable correspondiente.

Ejecutemos el ejemplo en el navegador.

Como los módulos admiten palabras clave y características especiales, debemos decirle al navegador que un script debe tratarse como un módulo, utilizando el atributo `<script type =" module ">`.

Asi:

[codetabs src="say" height="140" current="index.html"]

El navegador busca y evalúa automáticamente el módulo importado (y sus importaciones si es necesario), y luego ejecuta el script.
=======
The `import` directive loads the module by path `./sayHi.js` relative to the current file, and assigns exported function `sayHi` to the corresponding variable.

Let's run the example in-browser.

As modules support special keywords and features, we must tell the browser that a script should be treated as a module, by using the attribute `<script type="module">`.

Like this:

[codetabs src="say" height="140" current="index.html"]

The browser automatically fetches and evaluates the imported module (and its imports if needed), and then runs the script.

```warn header="Modules work only via HTTP, not in local files"
If you try to open a web-page locally, via `file://` protocol, you'll find that `import/export` directives don't work. Use a local web-server, such as [static-server](https://www.npmjs.com/package/static-server#getting-started) or use the "live server" capability of your editor, such as VS Code [Live Server Extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) to test them.
```
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

## Características del módulo central

¿Qué hay de diferente en los módulos en comparación con los scripts "normales"?

<<<<<<< HEAD
Hay características principales, válidas tanto para el navegador como para JavaScript del lado del servidor.
=======
There are core features, valid both for browser and server-side JavaScript.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

### Siempre "use strict"

<<<<<<< HEAD
Los módulos siempre llevan `use strict` de forma predeterminada. Por ejemplo, asignar a una variable sin declarar nos dará un error.
=======
Modules always `use strict`, by default. E.g. assigning to an undeclared variable will give an error.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```html run
<script type="module">
  a = 5; // error
</script>
```

<<<<<<< HEAD
### Alcance a nivel de módulo
=======
### Module-level scope
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Cada módulo tiene su propio alcance de nivel superior. En otras palabras, las variables y funciones de nivel superior de un módulo no se ven en otros scripts.

En el siguiente ejemplo, se importan dos scripts y `hello.js` intenta usar la variable `user` declarada en `user.js`, y falla:

[codetabs src="scopes" height="140" current="index.html"]

Se espera que los módulos realicen `export` a lo que ellos quieren que esté accesible desde afuera e `import` lo que necesiten.

<<<<<<< HEAD
Por lo tanto, deberíamos importar `user.js` en `hello.js` y obtener la funcionalidad requerida en lugar de depender de variables globales.

Esta es la variante correcta:

[codetabs src="scopes-working" height="140" current="hello.js"]

En el navegador, también existe el alcance independiente de alto nivel para cada `<script type="module">`:
=======
So we should import `user.js` into `hello.js` and get the required functionality from it instead of relying on global variables.

This is the correct variant:

[codetabs src="scopes-working" height="140" current="hello.js"]

In the browser, independent top-level scope also exists for each `<script type="module">`:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```html run
<script type="module">
  // La variable sólo es visible en éste script de módulo
  let user = "John";
</script>

<script type="module">
  *!*
  alert(user); // Error: user no está definido
  */!*
</script>
```

<<<<<<< HEAD
Si realmente necesitamos hacer una variable global a nivel de ventana, podemos asignarla explícitamente a `window` y acceder como `window.user`. Pero esa es una excepción que requiere una buena razón.
=======
If we really need to make a window-level global variable, we can explicitly assign it to `window` and access as `window.user`. But that's an exception requiring a good reason.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

### Un código de módulo se evalúa solo la primera vez cuando se importa

<<<<<<< HEAD
Si el mismo módulo se importa en varios otros lugares, su código se ejecuta solo la primera vez, luego se otorgan exportaciones a todos los importadores.

Eso tiene consecuencias importantes. Echemos un vistazo usando ejemplos:
=======
If the same module is imported into multiple other places, its code is executed only the first time, then exports are given to all importers.

That has important consequences. Let's look at them using examples:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Primero, si ejecutar un código de módulo trae efectos secundarios, como mostrar un mensaje, importarlo varias veces lo activará solo una vez, la primera vez:

```js
// 📁 alert.js
alert("Módulo es evaluado!");
```

```js
// Importar el mismo módulo desde archivos distintos

// 📁 1.js
import `./alert.js`; // Módulo es evaluado!

// 📁 2.js
<<<<<<< HEAD
import `./alert.js`; // (no muestra nada)
```

En la práctica, el código del módulo de nivel superior se usa principalmente para la inicialización, la creación de estructuras de datos internas y, si queremos que algo sea reutilizable, expórtelo.
=======
import `./alert.js`; // (shows nothing)
```

In practice, top-level module code is mostly used for initialization, creation of internal data structures, and if we want something to be reusable -- export it.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Ahora, un ejemplo más avanzado.

Digamos que un módulo exporta un objeto:

```js
// 📁 admin.js
export let admin = {
  name: "John"
};
```

Si este módulo se importa desde varios archivos, el módulo solo se evalúa la primera vez, se crea el objeto `admin` y luego se pasa a todos los importadores adicionales.

Todos los importadores obtienen exactamente el único objeto `admin`:

```js
// 📁 1.js
import {admin} desde './admin.js';
admin.name = "Pete";

// 📁 2.js
import {admin} desde './admin.js';
alert(admin.name); // Pete

*!*
// Ambos 1.js y 2.js han importado el mismo objeto
// Los cambios realizados en 1.js son visibles en 2.js
*/!*
```

<<<<<<< HEAD
Entonces, reiteremos: el módulo se ejecuta solo una vez. Se generan exportaciones y luego se comparten entre los importadores, por lo que si algo cambia el objeto `admin`, otros módulos lo verán.

Tal comportamiento nos permite *configurar* módulos en la primera importación. Podemos configurar sus propiedades una vez, y luego en futuras importaciones está listo.

Por ejemplo, el módulo `admin.js` puede proporcionar cierta funcionalidad, pero espera que las credenciales entren al objeto `admin` desde afuera:
=======
So, let's reiterate -- the module is executed only once. Exports are generated, and then they are shared between importers, so if something changes the `admin` object, other modules will see that.

Such behavior allows us to *configure* modules on first import. We can setup its properties once, and then in further imports it's ready.

For instance, the `admin.js` module may provide certain functionality, but expect the credentials to come into the `admin` object from outside:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```js
// 📁 admin.js
export let admin = { };

export function sayHi() {
  alert(`Ready to serve, ${admin.name}!`);
}
```

<<<<<<< HEAD
En `init.js`, el primer script de nuestra app, establecemos `admin.name`. Luego, todos lo verán, incluyendo llamadas desde dentro de el mismo `admin.js`:
=======
In `init.js`, the first script of our app, we set `admin.name`. Then everyone will see it, including calls made from inside `admin.js` itself:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```js
// 📁 init.js
import {admin} desde './admin.js';
admin.name = "Pete";
```

<<<<<<< HEAD
Otro módulo también puede ver `admin.name`:
=======
Another module can also see `admin.name`:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```js
// 📁 other.js
import {admin, sayHi} desde './admin.js';

alert(admin.name); // *!*Pete*/!*

sayHi(); // Ready to serve, *!*Pete*/!*!
```

### import.meta

El objeto `import.meta` contiene la información sobre el módulo actual.

Su contenido depende del entorno. En el navegador, contiene la url del script, o la url de una página web actual si está dentro de HTML:

```html run height=0
<script type="module">
  alert(import.meta.url); // script url (url de la página html para un script en línea)
</script>
```

<<<<<<< HEAD
### En un módulo, "this" es indefinido (undefined).

Esa es una característica menor, pero para completar, debemos mencionarla.
=======
### In a module, "this" is undefined
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

En un módulo, el nivel superior `this` no está definido.

<<<<<<< HEAD
Compárelo con scripts que no sean módulos, donde `this` es un objeto global:
=======
In a module, top-level `this` is undefined.

Compare it to non-module scripts, where `this` is a global object:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```html run height=0
<script>
  alert(this); // window
</script>

<script type="module">
  alert(this); // undefined
</script>
```

## Funciones específicas del navegador

También hay varias diferencias de scripts específicas del navegador con `type =" module "` en comparación con las normales.

<<<<<<< HEAD
Es posible que desee omitir esta sección por ahora si está leyendo por primera vez o si no usa JavaScript en un navegador.
=======
You may want skip this section for now if you're reading for the first time, or if you don't use JavaScript in a browser.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

### Los módulos son diferidos

Los módulos están *siempre* diferidos, el mismo efecto que el atributo `defer` (descrito en el capítulo [](info:script-async-defer)), para ambos scripts externos y en línea.

<<<<<<< HEAD
En otras palabras:
- descargar módulos externo `<script type="module" src="...">` no bloquea el procesamiento de HTML, se cargan en paralelo con otros recursos.
- los módulos esperan hasta que el documento HTML esté completamente listo (incluso si son pequeños y cargan más rápido que HTML), y luego lo ejecuta.
- se mantiene el órden relativo de los scripts: los scripts que van primero en el documento, se ejecutan primero.

Como efecto secundario, los módulos siempre "ven" la página HTML completamente cargada, incluidos los elementos HTML debajo de ellos.
=======
In other words:
- downloading external module scripts `<script type="module" src="...">` doesn't block HTML processing, they load in parallel with other resources.
- module scripts wait until the HTML document is fully ready (even if they are tiny and load faster than HTML), and then run.
- relative order of scripts is maintained: scripts that go first in the document, execute first.

As a side-effect, module scripts always "see" the fully loaded HTML-page, including HTML elements below them.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Por ejemplo:

```html run
<script type="module">
*!*
  alert(typeof button); // objeto: el script puede 'ver' el botón de abajo
*/!*
  // debido que los módulos son diferidos, el script se ejecuta después de que la página entera se haya cargado
</script>

<<<<<<< HEAD
Abajo compare con un script normal:
=======
Compare to regular script below:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

<script>
*!*
  alert(typeof button); // Error: button es indefinido, el script no puede ver los elementos de abjo
*/!*
  // los scripts normales corren inmediatamente, antes que el resto de la página sea procesada
</script>

<button id="button">Button</button>
```

<<<<<<< HEAD
Tenga en cuenta: en realidad el segundo script se ejecuta antes que el primero! Entonces veremos primero `undefined`, y después `object`.

Esto se debe a que los módulos están diferidos, por lo que esperamos a que se procese el documento. El script normal se ejecuta inmediatamente, por lo que vemos su salida primero.

Al usar módulos, debemos tener en cuenta que la página HTML se muestra a medida que se carga, y los módulos JavaScript se ejecutan después de eso, por lo que el usuario puede ver la página antes de que la aplicación JavaScript esté lista. Es posible que algunas funciones aún no funcionen. Deberíamos poner "indicadores de carga", o asegurarnos de que el visitante no se confunda con eso.

### Async funciona en scripts en línea
=======
Please note: the second script actually runs before the first! So we'll see `undefined` first, and then `object`.

That's because modules are deferred, so we wait for the document to be processed. The regular script runs immediately, so we see its output first.

When using modules, we should be aware that the HTML page shows up as it loads, and JavaScript modules run after that, so the user may see the page before the JavaScript application is ready. Some functionality may not work yet. We should put "loading indicators", or otherwise ensure that the visitor won't be confused by that.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Para los scripts que no son módulos, el atributo `async` solo funciona en scripts externos. Los scripts asíncronos se ejecutan inmediatamente cuando están listos, independientemente de otros scripts o del documento HTML.

<<<<<<< HEAD
Para los scripts de módulo, también funciona en scripts en línea.

Por ejemplo, el siguiente script en línea tiene `async`, por lo que no espera nada.

Realiza la importación (extrae `./Analytics.js`) y se ejecuta cuando está listo, incluso si el documento HTML aún no está terminado o si aún hay otros scripts pendientes.
=======
For non-module scripts, the `async` attribute only works on external scripts. Async scripts run immediately when ready, independently of other scripts or the HTML document.

For module scripts, it works on inline scripts as well.

For example, the inline script below has `async`, so it doesn't wait for anything.

It performs the import (fetches `./analytics.js`) and runs when ready, even if the HTML document is not finished yet, or if other scripts are still pending.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Eso es bueno para la funcionalidad que no depende de nada, como contadores, anuncios, detectores de eventos a nivel de documento.

```html
<!-- todas las dependencias se extraen (analytics.js), y el script se ejecuta -->
<!-- no espera por el documento u otras etiquetas <script> -->
<script *!*async*/!* type="module">
  import {counter} from './analytics.js';

  counter.count();
</script>
```

### Scripts externos

<<<<<<< HEAD
Los scripts externos que tengan `type="module"` son diferentes en dos aspectos:

1. Los scripts externos con el mismo `src` sólo se ejecutan una vez:
=======
External scripts that have `type="module"` are different in two aspects:

1. External scripts with the same `src` run only once:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31
    ```html
    <!-- el script my.js se extrae y ejecuta sólo una vez -->
    <script type="module" src="my.js"></script>
    <script type="module" src="my.js"></script>
    ```

<<<<<<< HEAD
2. Los scripts externos que se buscan desde otro origen (p.ej. otra sitio web) require encabezados [CORS](mdn:Web/HTTP/CORS), como se describe en el capítulo <info:fetch-crossorigin>. En otras palabras, si un script de módulo es extraido desde otro origen, el servidor remoto debe proporcionar un encabezado `Access-Control-Allow-Origin` permitiendo la búsqueda.
=======
2. External scripts that are fetched from another origin (e.g. another site) require [CORS](mdn:Web/HTTP/CORS) headers, as described in the chapter <info:fetch-crossorigin>. In other words, if a module script is fetched from another origin, the remote server must supply a header `Access-Control-Allow-Origin` allowing the fetch.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31
    ```html
    <!-- otro-sitio-web.com debe proporcionar Access-Control-Allow-Origin -->
    <!-- si no, el script no se ejecutará -->
    <script type="module" src="*!*http://otro-sitio-web.com/otro.js*/!*"></script>
    ```

    Esto asegura mejor seguridad de forma predeterminada.

<<<<<<< HEAD
### No se permiten módulos sueltos

En el navegador, `import` debe obtener una URL relativa o absoluta. Los módulos sin ninguna ruta se denominan módulos sueltos. Dichos módulos no están permitidos en `import`.

Por ejemplo, este `import` no es válido:
=======
### No "bare" modules allowed

In the browser, `import` must get either a relative or absolute URL. Modules without any path are called "bare" modules. Such modules are not allowed in `import`.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```js
<<<<<<< HEAD
import {sayHi} from 'sayHi'; // Error, módulo suelto
// el módulo debe tener una ruta, por ejemplo './sayHi.js' o dondequiera que el módulo esté
```

Ciertos entornos, como Node.js o herramientas de paquete permiten módulos simples sin ninguna ruta, ya que tienen sus propias formas de encontrar módulos y hooks para ajustarlos. Pero los navegadores aún no admiten módulos sueltos.
=======
import {sayHi} from 'sayHi'; // Error, "bare" module
// the module must have a path, e.g. './sayHi.js' or wherever the module is
```

Certain environments, like Node.js or bundle tools allow bare modules, without any path, as they have their own ways for finding modules and hooks to fine-tune them. But browsers do not support bare modules yet.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

### Compatibilidad, "nomodule"

<<<<<<< HEAD
Los navegadores antiguos no entienden `type = "module"`. Los scripts de un tipo desconocido simplemente se ignoran. Para ellos, es posible proporcionar un respaldo utilizando el atributo `nomodule`:
=======
Old browsers do not understand `type="module"`. Scripts of an unknown type are just ignored. For them, it's possible to provide a fallback using the `nomodule` attribute:
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

```html run
<script type="module">
  alert("Ejectua en navegadores modernos");
</script>

<script nomodule>
  alert("Los navegadores modernos conocen tanto type=module como nomodule, así que omita esto")
  alert("Los navegadores antiguos ignoran la secuencia de comandos con type=module desconocido, pero ejecutan esto.");
</script>
```

<<<<<<< HEAD
## Herramientas de Ensamblaje

En la vida real, los módulos de navegador rara vez se usan en su forma "pura". Por lo general, los agrupamos con una herramienta especial como [Webpack] (https://webpack.js.org/) y los implementamos en el servidor de producción.

Uno de los beneficios de usar empaquetadores -- dan más control sobre cómo se resuelven los módulos, permitiendo módulos simples y mucho más, como los módulos CSS/HTML.
=======
## Build tools
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

Las herramientas de compilación hacen lo siguiente:

1. Toman un módulo "principal", el que se pretende colocar en `<script type="module">` en HTML.
2. Analiza sus dependencias: las importa y luego importaciones de importaciones etcétera.
3. Compila un único archivo con todos los módulos (o múltiples archivos, eso es ajustable), reemplazando los llamados nativos de `import` con funciones del empaquetador para que funcione. Los módulos de tipo "Especial" como módulos HTML/CSS también son supported.
4. Durante el proceso, otras transformaciones y optimizaciones se pueden aplicar:
    - Se elimina código inaccesible.
    - Se elimina exportaciones sin utilizar ("tree-shaking").
    - Sentencias específicas de dessarrollo tales como `console` y `debugger` se eliminan.
    - La sintaxis JavaScript moderna puede transformarse en una sintaxis más antigua con una funcionalidad similar utilizando [Babel](https://babeljs.io/).
    - El archivo resultante se minimiza. (se eliminan espacios, las variables se reemplazan con nombres cortos, etc).

Si utilizamos herramientas de ensamblaje, entonces, a medida que los scripts se agrupan en un solo archivo (o pocos archivos), las declaraciones `import/export` dentro de esos scripts se reemplazan por funciones especiales de ensamblaje. Por lo tanto, el script "empaquetado" resultante no contiene ninguna `import/export`, no requiere `type="module"`, y podemos ponerla en un script normal:

<<<<<<< HEAD
```html
<!-- Asumiendo que obtenemos bundle.js desde una herramienta como Webpack -->
=======
1. Take a "main" module, the one intended to be put in `<script type="module">` in HTML.
2. Analyze its dependencies: imports and then imports of imports etc.
3. Build a single file with all modules (or multiple files, that's tunable), replacing native `import` calls with bundler functions, so that it works. "Special" module types like HTML/CSS modules are also supported.
4. In the process, other transformations and optimizations may be applied:
    - Unreachable code removed.
    - Unused exports removed ("tree-shaking").
    - Development-specific statements like `console` and `debugger` removed.
    - Modern, bleeding-edge JavaScript syntax may be transformed to older one with similar functionality using [Babel](https://babeljs.io/).
    - The resulting file is minified (spaces removed, variables replaced with shorter names, etc).

If we use bundle tools, then as scripts are bundled together into a single file (or few files), `import/export` statements inside those scripts are replaced by special bundler functions. So the resulting "bundled" script does not contain any `import/export`, it doesn't require `type="module"`, and we can put it into a regular script:

```html
<!-- Assuming we got bundle.js from a tool like Webpack -->
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31
<script src="bundle.js"></script>
```

Dicho esto, los módulos nativos también se pueden utilizar. Por lo tanto no estaremos utilizando Webpack aquí: tú lo podrás configurar más adelante.

## Resumen

Para resumir, los conceptos centrales son:

<<<<<<< HEAD
1. Un módulo es un archivo. Para que funcione `import/export`, los navegadores necesitan `<script type="module">`. Los módulos tienen varias diferencias:
     - Diferido por defecto.
     - Async funciona en scripts en línea.
     - Para cargar scripts externos de otro origen (dominio/protocolo/puerto), se necesitan encabezados CORS.
     - Se ignoran los scripts externos duplicados.
2. Los módulos tienen su propio alcance local de alto nivel y funcionalidad de intercambio a través de 'import/export'.
3. Los módulos siempre usan `use strict`.
4. El código del módulo se ejecuta solo una vez. Las exportaciones se crean una vez y se comparten entre los importadores.

Cuando usamos módulos, cada módulo implementa la funcionalidad y la exporta. Luego usamos `import` para importarlo directamente donde sea necesario. El navegador carga y evalúa los scripts automáticamente.
=======
1. A module is a file. To make `import/export` work, browsers need `<script type="module">`. Modules have several differences:
    - Deferred by default.
    - Async works on inline scripts.
    - To load external scripts from another origin (domain/protocol/port), CORS headers are needed.
    - Duplicate external scripts are ignored.
2. Modules have their own, local top-level scope and interchange functionality via `import/export`.
3. Modules always `use strict`.
4. Module code is executed only once. Exports are created once and shared between importers.

When we use modules, each module implements the functionality and exports it. Then we use `import` to directly import it where it's needed. The browser loads and evaluates the scripts automatically.
>>>>>>> cd2c7ce3c8f033e6f7861ed1b126552e41ba3e31

En la producción, las personas a menudo usan paquetes como [Webpack] (https://webpack.js.org) para agrupar módulos por rendimiento y otras razones.

En el próximo capítulo veremos más ejemplos de módulos y cómo se pueden exportar/importar cosas.
