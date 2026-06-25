# Fundamentos
|Fundamentos| [Youtube](https://www.youtube.com/watch?v=XfekLkbqFpQ) | [Diapostivias](https://bootcamp.manz.dev/slides/fundamentos/) |

## Variables
```js
const name = "Manz";
let number = 4;

name = "ManzDev"; ❌
number = 8; ✅
```

## Comentarios
```js
// Un comentario de una sola linea

/*
  Comentarios más complejos,
  de varias lineas.
*/
```

## Tipos de datos
Tipos: Primitivos (Boolean, Number, String) y Civilizados (Object, Array, Function)
Primitivos especiales: undefined, null
Avanzado: Symbol

### Variables
```js
const isOpen = true;                  // true o false
const price = 50.25;                  // enteros o decimales
const name = "ManzDev";               // textos (carácteres o cadenas de texto)

let empty;                            // undefined
const userInRoom = null;              // ausencia (intencional)
const start = Symbol("start");        // valores únicos (identificadores)
const global = Symbol.for("start");   // valores globales

const bigNumber = 12345678901234561n; // BigInt para números grandes
const number = 4 - "hola";      // NaN (Not a Number)

Number("35");                   // 35 (es número)
Number("DHardySD");             // NaN (Not a Number)
String(4);                      // "4" (es texto)

Number.parseInt("35€");         // 35 (es número)
Number.parseFloat("35.5€");     // 35.5 (es número)
```

### Colecciones

```js
// Array
const numbers = [1, 5, 10, 15, 20];

// Objeto
const object = {
  name: "ManzDev",
  life: 95,
  numbers: [1, 5, 10, 15, 20] //importante, no poner la coma en la última propiedad
}

// Conjunto (no repetidos)
const set = new Set([ 1, 5, 10, 15 ]);

// Mapa
const map = new Map([
  ["name", "Manz"],
  ["life", 95]
]);
// ~ map = new Map(Object.entries(object));
```

### Ámbitos
```js
const name = "ManzDev";

// existe aquí
// ...
// y aquí
// ...
// ...
// y aquí
//----------------------//
// aquí no existe aún
{
  const name = "ManzDev";
  // aquí existe
  // ...
  // y aquí
}
// pero aquí no
```

## Condicionales

```js
const number = 3;

if (number < 5) {
  console.log("Malo");
} else {
  console.log("Bueno");
}

const value = number < 5 ? "Malo" : "Bueno";

// Ternarios encadenados ⚠
const value =
  number < 5 ? "Malo" :
  number == 5 ? "Decente" :
  "Bueno";

const number = 1;
switch (number) {
  case 1:
    console.log("Muy malo");
    break; // obligatorio para salir, sino ejecuta el resto de casos
  ...
  default:
    console.log("Valor no identificado");
    break;
}

// Igual se puede sustituir un switch por un diccionario
const number = 1;

const dictionary = {
  1: "Muy malo",
  2: "Malo",
  3: "Normal",
}

const value = dictionary[number];
```

## Bucles

```js
let number = 5;           // Inicialización

while (number > 0) {      // Condición
  console.log(number);
  number--;               // Incremento
}

let number = 0;

do {
  console.log(number);
  number--;
} while (number > 0);

// for(ini, cond, incr)
for (let number = 0; number <= 5; number++) {
  console.log("Number vale: ", number);
}

// Posición        0   1   2   3  4  5
const elements = [25, 20, 15, 10, 5, 1];

for (index in elements) {
  console.log(index);   // index (0, 1, 2...)
}

for (number of elements) {
  console.log(number);  // valor (25, 20...)
}
```

## Funciones

```js
// Parámetros
function mostrar(title, description = "--") {
  console.log(title + " ------------");
  console.log(description);
  return 42;
}

//Argumentos
const name = "ManzDev";
const description = "Es un streamer";
const output = mostrar(name, description);

// Formas de nombrar a las funciones
function name(a, b) {
  /* ... */
}

function (a, b) { /* ... */ }

const name = function (a, b) {
  /* ... */
}

// Funciones flecha
const name = (a, b) => {
  /* ... */
  return 42;
}

const name = (a, b) => { /* ... */ }

// return directo
const name = (a, b) => 42;
```

## Clases

```js
class Human {
  name = "NPC";
  height = 185;
  x = 0;

  walk() {
    this.x = this.x + 25;
  }
}

const npc = new Human();     // Crear humano
const manz = new Human();    // Crear humano
npc.name     // "NPC"
manz.x       // 0
manz.walk()  // (Ejecutamos función)
manz.x       // 25
npc.x        // 0
manz.name    // "NPC"

// Constructor
class Human {
  name = "NPC";
  height;
  x = 0;

  constructor(name, height = 120) {
    this.name = name;
  }
}
const npc = new Human(); // NPC, 1'20
const manz = new Human("ManzDev", 185); // ManzDev, 1'85
const bot = new Human("CyberManzDev"); // CyberManzDev, 1'20

manz.name     // "ManzDev"

// Getters y Setters
class Human {
  #name = "NPC"; // Privada

  info() { return this.#name }
}

const npc = new Human();
npc.name    // undefined
npc.#name   // ❌ no desde fuera de clase
npc.info()  // ✅ si desde dentro de clase

class Human {
  /* ... */

  get name() {
    return "Mi nombre es: " + this.#name;
  }

  set name(name) { this.#name = name }
}

// Propiedades / Métodos
class God {
  static name = "Jordi Hurtado";
  static height;
  static x = Infinity;

  static talk() {
    console.log("Hi!");
  }
}

Human.name    // "Jordi Hurtado"
Human.x       // Infinity
Human.talk()  // Muestra "Hi!"

Human.name = "Manz";
Human.name    // "Manz"
```

## Clases Herencia
```js
class Cat {
  constructor() { /* ... */ }

  meow() {
    console.log("Meow!");
  }
}

const cat = new Cat();
cat.meow(); ✅
cat.fly();  ❌

class SuperCat extends Cat {
  constructor() {
    super();
  }

  fly() { /* ... */ }
}

const supercat = new SuperCat();
supercat.meow(); ✅
supercat.fly();  ✅
```
